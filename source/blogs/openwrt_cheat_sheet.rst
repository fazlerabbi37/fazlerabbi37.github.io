OpenWrt Cheat Sheet
=====================================
`< Blog <../blog.html>`_

A quick reference to OpenWrt

Created on: 2019-12-08

.. role:: kbd

Install
-------
Given we have a supported hardware, installing OpenWrt is very simple. Head over to `Table of Hardware <https://openwrt.org/toh/start>`_ and check if our hardware is supported. We can search by putting our device's Brand and Model on the white input box and pressing enter. We must make sure to match the version number. If we see our device on the list, we should also see a Device Page on the 5th column. The link on the device page would have detailed instruction on how to install OpenWrt on that device. The general steps would be:

- Taking a backup of the router
- Downloading the firmware
- Resetting the router
- Powering up the router
- Connecting to the router via LAN cable
- Going to the routers web management portal
- Going to System Tools -> Firmware Upgrade section from the menu
- Uploading the firmware 
- Waiting for the router to reboot
- The either Telnet to 192.168.1.1 and set a root password, or browse to http://192.168.1.1 if LuCI is installed.
- And we are done!

Building from source
--------------------
In Ubuntu 18.04, to build OpenWrt from source we need to follow this steps:

1. Installing the necessary packages::

    sudo apt install subversion g++ zlib1g-dev build-essential git python python3 libncurses5-dev gawk gettext unzip file libssl-dev \
                     wget libelf-dev ecj fastjar java-propose-classpath build-essential libncursesw5-dev python unzip -y


2. Getting the OpenWrt source code::

    git clone https://github.com/openwrt/openwrt.git

3. Going inside the directory and running the scripts to update and install feeds::

    cd openwrt
    ./scripts/feeds update -a
    ./scripts/feeds install -a

4. Making the configuration::

    make menuconfig

This will open a menu for us to select our router configuration. For example, if we want to build images for the "TL-WR841N v11" Wifi-Router, the options will be 

- Target System = Atheros AR7xxx/AR9xxx
- Subtarget = Devices with small flash
- Target Profile = TP-LINK TL-WR841N/ND v11

We can get most of the info in the Device Page column ofn `Table of Hardware <https://openwrt.org/toh/start>`_.

5. Building the firmware::

    make

Afterwards, we can get the images in ./bin/targets/$SYSTEM/generic directory.


Building from source with Docker
--------------------------------
For convenience of not installing a lot of dependency in the system, I put together a Dockerfile for building the firmware from source. The process is similar to the `Building from source`_.

1. First we need to get the OpenWrt source code::

    git clone https://github.com/openwrt/openwrt.git

2. We need to change our directory to openwrt::

    cd openwrt

3. Then we will open a file named Dockerfile with our favourite editor. I would be using vim::

    vim Dockerfile

P.S. Enable paste mode if you are also using vim with :kbd:`Esc` th :kbd:`:` and type `set paste`

4. Then we will paste the following::

	FROM ubuntu:18.04

	RUN apt update
    
    RUN apt install subversion g++ zlib1g-dev build-essential git python python3 libncurses5-dev gawk gettext unzip file libssl-dev \
                     wget libelf-dev ecj fastjar java-propose-classpath build-essential libncursesw5-dev python unzip -y

	ARG USER_ID
	ARG GROUP_ID

	USER $USER_ID:$GROUP_ID

	WORKDIR /app

	COPY --chown=$USER_ID:$GROUP_ID . .


5. Building the OpenWrt Docker image::

    sudo docker build --build-arg USER_ID=$(id -u) --build-arg GROUP_ID=$(id -g) -t openwrt .


6. Running the scripts to update and install the feeds::

	sudo docker run -it -v $(pwd):/app -eUSER_ID=$(id -u) -e GROUP_ID=$(id -g) openwrt ./scripts/feeds update -a
	sudo docker run -it -v $(pwd):/app -eUSER_ID=$(id -u) -e GROUP_ID=$(id -g) openwrt ./scripts/feeds install -a


7. Making the configuration is same as manual build::

    sudo docker run -it -v $(pwd):/app -eUSER_ID=$(id -u) -e GROUP_ID=$(id -g)  openwrt make menuconfig

This will open a menu for us to select our router configuration. For example, if we want to build images for the "TL-WR841N v11" Wifi-Router, the options will be 

- Target System = Atheros AR7xxx/AR9xxx
- Subtarget = Devices with small flash
- Target Profile = TP-LINK TL-WR841N/ND v11

We can get most of the info in the Device Page column ofn `Table of Hardware <https://openwrt.org/toh/start>`_.

8. Building the firmware::

    sudo docker run -it -v $(pwd):/app -eUSER_ID=$(id -u) -e GROUP_ID=$(id -g) openwrt make

Afterwards, we can get the images in ./bin/targets/$SYSTEM/generic directory.


revert back to original firmware
--------------------------------
::

    dd if=orig.bin of=tplink.bin skip=257 bs=512
    mtd -r write /tmp/tplink.bin firmware


- https://forum.archive.openwrt.org/viewtopic.php?id=50608
- https://oldwiki.archive.openwrt.org/toh/tp-link/tl-wr741nd#back.to.original.firmware
- https://openwrt.org/docs/guide-user/installation/generic.uninstall


enable wifi by default
----------------------
- https://forum.openwrt.org/t/solved-enable-wi-fi-and-connect-to-a-network-on-first-boot/47399/31




Source
------
- `Quick Image Building Guide <https://openwrt.org/docs/guide-developer/quickstart-build-images>`_

.. - `How to enable WIFI on first firmware boot by default? <https://forum.openwrt.org/t/how-to-enable-wifi-on-first-firmware-boot-by-default/6568>`_
.. - `OpenWrt build system – Usage:Custom files <https://oldwiki.archive.openwrt.org/doc/howto/build#custom_files>`_
.. - `Wi-Fi /etc/config/wireless <https://openwrt.org/docs/guide-user/network/wifi/basic>`_
