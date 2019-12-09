TigerVNC starter guilde
=======================
`< Blog <../blog.html>`_

This is a getting started guide with TigerVNC. 

Created on: 2019-12-04

.. role:: kbd



Installing TigerVNC Server
--------------------------
To install TigerVNC run the following::

    sudo apt install tigervnc-standalone-server tigervnc-common -y

If our desktop environment is GNOME this additional package needs to install::

    sudo apt install tigervnc-xorg-extension -y

Run TigerVNC Server
-------------------
To run TigerVNC Server::

    vncserver

We will see the following output::

    You will require a password to access your desktops.

    Password:
    Verify:
    Would you like to enter a view-only password (y/n)? n
    /usr/bin/xauth:  file /home/user/.Xauthority does not exist

    New 'hostname:1 (user)' desktop at :1 on machine hostname

    Starting applications specified in /etc/X11/Xvnc-session
    Log file is /home/user/.vnc/debian9.localdomain:1.log

    Use xtigervncviewer -SecurityTypes VncAuth -passwd /home/user/.vnc/passwd :1 to connect to the VNC server.


Configuring GNOME Desktop environment
-------------------------------------
For this we need to create a file name `~/.vnc/xstartup`. Let's start by open a file with favourite our text editor. I am using vim::

    vim ~/.vnc/xstartup

Now paste the following code::

    #!/bin/bash
    # Start Gnome Desktop 
    [ -x /etc/vnc/xstartup ] && exec /etc/vnc/xstartup
    [ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources
    vncconfig -iconic &
    dbus-launch --exit-with-session gnome-session &

.. note:: If we see `dbus-launch` error, we need to install `dbus-x11` package. In ubuntu we can do this with `sudo apt install dbus-x11 -y`

.. warning:: 
	If this script is not used we may see the following error::

		server: Failed command '/etc/X11/Xvnc-session': 256!

		=================== tail -15 /$USER/.vnc/$HOST:1.log ===================
		See http://www.tigervnc.org for information on TigerVNC.
		Underlying X server release 12004000, The X.Org Foundation


		Fri Jan  5 71:03:23 2091
		 vncext:      VNC extension running!
		 vncext:      Listening for VNC connections on local interface(s), port 5901
		 vncext:      created VNC server for screen 0
		XIO:  fatal IO error 11 (Resource temporarily unavailable) on X server ":1"
		      after 173 requests (173 known processed) with 0 events remaining.

		Fri Jan  5 71:03:33 2091
		 ComparingUpdateTracker: 0 pixels in / 0 pixels out
		 ComparingUpdateTracker: (1:-nan ratio)
		Killing Xtigervnc process ID 5137... which seems to be deadlocked. Using SIGKILL!

		======================================================================

		Starting applications specified in /etc/X11/Xvnc-session has failed.
		Maybe try something simple first, e.g.,
			tigervncserver -xstartup /usr/bin/xterm



VNC is not an encrypted protocol and can be subject to packet sniffing. So is by default when it starts it only accept connections from the localhost interface. We will need to use SSH tunnel to connect to the remote host. We will how to do that later in `View from local host`_ section.

But if you are not concern about security like you are running a VM on local network then and sure about security then you can allow accepting connections from all interfaces by runnnig::

    vncserver -localhost no


.. warning:: as of Today(2019-12-09) the systemd is not working. please skip it until I fix it.

Creating a Systemd unit file
----------------------------
The systemd unit file will allow us to easily start, stop, and restart the VNC service as needed. Now we need to open a file with favourite our text editor. I am using vim::

    sudo vim /etc/systemd/system/vncserver@.service

PS: if we are using vim it would be a good time to enable paste mode with :kbd:`Esc` then :kbd:`:` the type `set paste`

Now paste the following lines in that file::

    [Unit]
    Description=Remote desktop service (VNC)
    After=syslog.target network.target

    [Service]
    Type=simple
    User=$USER
    PAMName=login
    PIDFile=/home/%u/.vnc/%H%i.pid
    ExecStartPre=/bin/bash -c '/usr/bin/vncserver -kill :%i > /dev/null 2>&1 || :'
    # this start vncserver to accept connection from localhost only so need to use SSH tunnel
    ExecStart=/usr/bin/vncserver :%i -geometry 1440x900 -autokill
    # this start vncserver to accept connection from all interface so this is insecure. only use this if you know what you are doing
    # ExecStart=/usr/bin/vncserver :%i -localhost no -geometry 1440x900 -autokill
    ExecStop=/usr/bin/vncserver -kill :%i

    [Install]
    WantedBy=multi-user.target

.. note:: maybe we should move the config like -geometry, -autokill and -localhost to config file

If we notice the code for the systemd file we will see: 

- In line 6 we have a `$USER` variable. We need to replace that to our user name.
- In line 11 we have used the `vncserver` command to start the vncserver to only accept connections from localhost interface. This is recommended and used by default. To connect from remote host we must use SSH tunnel mentioned in the previous section. 
- In line 13 we have used the `vncserver` command to start the vncserver to only accept connections from all interfaces. This is NOT recommended and thus commented out. If you want to use it comment out line 11 and uncomment this (13) line. We mast run `sudo systemctl daemon-reload` to see the effect of our change in vncserver@.service.

Now let's proceed to using the systemd file. First save the file and then run::

    sudo systemctl daemon-reload

Next, enable the service::

    sudo systemctl enable vncserver@1.service

The number `1` after the `@` sign defines the display port on which the VNC service will run. As we discussed in the previous section since we are using `1` the VNC server will listen on port `5901`

Start the VNC service by executing::

    sudo systemctl start vncserver@1.service

Verify that the service is successfully started with::

    sudo systemctl status vncserver@1.service


View from local host
--------------------
The recommended approach is to create an `SSH tunnel <https://linuxize.com/post/how-to-setup-ssh-tunneling/>`_ that will securely forwards traffic from our local host on port 5901 to the server on the same port. To setup port forwarding run::

    ssh -L 5901:127.0.0.1:5901 -N -f -l $USERNAME $SERVER_IP_ADDRESS


Now we will install a VNC viwer in our local host::

    sudo apt install tigervnc-viewer -y

Or you can use the `Remmina <https://remmina.org/>`_ if you are in Ubuntu.

If you used port forwarding then put `127.0.0.1:5901` in and connect.

If you used `-localhost no` the put the ip address of the remote host and connect.


Source
------
- `How to Install and Configure VNC on Debian 9 <https://linuxize.com/post/how-to-install-and-configure-vnc-on-debian-9/>`_
- `Install and Configure TigerVNC server on Ubuntu 18.04 <https://www.cyberciti.biz/faq/install-and-configure-tigervnc-server-on-ubuntu-18-04/>`_
- `Unable to connect through VNC <https://askubuntu.com/a/1159514/502875>`_
- `How to Install and Configure VNC on Ubuntu 18.04 <https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-vnc-on-ubuntu-18-04>`_
- https://bbs.archlinux.org/viewtopic.php?pid=1648878#p1648878
- https://wiki.archlinux.org/index.php/TigerVNC
