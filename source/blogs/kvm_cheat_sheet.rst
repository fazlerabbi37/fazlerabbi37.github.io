KVM Cheat Sheet
===============
`< Blog <../blog.html>`_

A quick reference to KVM.

Created on: 2019-01-22

Tag: `cheat_sheet <blogs/tag_cheat_sheet.html>`_

install kvm in ubuntu
---------------------
pre-installation check
``````````````````````
Check that our CPU supports hardware virtualization [1]_::

    egrep -c '(vmx|svm)' /proc/cpuinfo

if it is more 0 then your hardware doesn't support virtualization. If it is more then 0 then we are good to go. Alternatively we can use::

    egrep -c ' lm ' /proc/cpuinfo

which will give similar result.

installation
````````````
to install KVM in Ubuntu [2]_::

    sudo apt-get install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils virt-manager -y

post-installation
`````````````````
on post-installation we need to configure the network. Here I will only give the example of bridged networking in DHCP.[3]_. First make backup of your netowrk configuration::

	sudo cp /etc/network/interfaces /etc/network/interfaces.bak


.. warning:: Unfortunately, the draw back of this method is that, on next boot it disables the network manager. If we use this we need to run `sudo /etc/init.d/networking restart` everytime to bring the bridge interface up.

Now open `/etc/network/interfaces` file with your choice of editor and paste the following::

    iface eth0 inet manual #  change eth0 to your ethernet adapter name

    auto lo
    iface lo inet loopback

    auto br0
    iface br0 inet dhcp
        bridge_ports eth0 # change eth0 to your ethernet adapter name
        bridge_stp off
        bridge_fd 0
        bridge_maxwait 0

Also, edit ``/etc/sysctl.conf`` to uncomment::

    net.ipv4.ip_forward=1

Got it from this source: https://askubuntu.com/a/1134422

Now restart the network adapter::

	sudo systemctl restart networking.service


uninstall kvm
-------------
::

    sudo apt-get remove --purge qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils virt-manager -y

also check and remove this::

    sudo rm -rf /etc/kvm
    sudo rm -rf /etc/udev/rules.d/45-kvm.rules
    sudo rm -rf /etc/init.d/kvm

source: https://askubuntu.com/a/385358

I normally do this::

    sudo rm -rf /etc/apparmor.d/libvirt
    sudo rm -rf /etc/libvirt
    sudo rm -rf /usr/lib/libvirt
    sudo rm -rf /usr/lib/qemu
    sudo rm -rf /usr/lib/x86_64-linux-gnu/qemu/
    sudo rm -rf /usr/share/libvirt
    sudo rm -rf /var/lib/libvirt



Make guest from ISO
-------------------
To create a new guest instance from ISO, run the following::

    sudo virt-install --virt-type=kvm --name $name --ram $ram_size_in_mb --vcpus=2 --hvm --network=bridge:$bridge_name --cdrom=$iso_location --disk $img_file_location,size=$disk_size_in_gb

Make guest from a ``.img`` file
-------------------------------
To make a guest from an existing ``.img`` file, run the following::

    sudo virt-install --virt-type=kvm --name $name --ram 512 --vcpus=1 --hvm --network=bridge:$bridge_name --import --disk $new_img_file_location

This makes possible to make one base image and then copy the image and spun a new guest. For example, let's consider we have a base image name ``ubuntu_1604_server.img`` to make a new ``$name`` guest, we do:: 

    sudo cp ubuntu_1604_server.img $name.img
    sudo virt-install --virt-type=kvm --name $name --ram 1024 --vcpus=1 --hvm --import --disk $name.img

Make a Widnows guest from ISO
-----------------------------
To make a Windows guest from ISO, run this::

    virt-install --name=windows10 --ram=4048 --vcpus=4 --os-type=windows --os-variant=win8.1 --network=bridge:br0 --cdrom=Windows_10.iso --disk windows10,size=40

Make an ``.img`` file
---------------------
We will use ``qemu-img`` to create a new ``.img`` file of 2 GB::

    qemu-img create -f qcow2 $name.img 2g

See info of an ``.img`` file
----------------------------
We can see the information of an existing ``.img`` file using ``qemu-img``::

    qemu-img info $name

Source
------
.. [1] `KVM/Installation - Pre-installation checklist <https://help.ubuntu.com/community/KVM/Installation#Pre-installation_checklist>`_
.. [2] `KVM/Installation - Installation of KVM <https://help.ubuntu.com/community/KVM/Installation#Installation_of_KVM>`_
.. [3] `KVM/Networking - Bridged Networking <https://help.ubuntu.com/community/KVM/Networking#Bridged_Networking>`_
