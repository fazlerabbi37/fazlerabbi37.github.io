Turn on desktop sharing over SSH in Ubuntu
==========================================
`Blog <../blog.html>`__

Turing on desktop sharing in Ubuntu over SSH 

Created on: 2020-03-11

Tag: `useless_rnd <tag_useless_rnd.html>`_

Discovery/Query/Idea
--------------------
Idea: How can we turn on desktop sharing in Ubuntu over SSH.

Primary Goal
------------
Do it from terminal first.

Trail 01
--------
Research
````````
From `Official Ubuntu Documentation: Share your desktop <https://help.ubuntu.com/stable/ubuntu-help/sharing-desktop.html>`_ we get that it usages `Vino <https://wiki.gnome.org/Projects/Vino>`_.  We should be able to manipulate setting from terminal with `gsettings`_. 


Development
```````````
Let's try that and see desktop share (Vino) status::

    sudo gsettings list-recursively org.gnome.Vino

If we check the disabled state::

    org.gnome.Vino notify-on-connect true
    org.gnome.Vino alternative-port uint16 5900
    org.gnome.Vino disable-background false
    org.gnome.Vino use-alternative-port false
    org.gnome.Vino icon-visibility 'client'
    org.gnome.Vino use-upnp false
    org.gnome.Vino view-only true
    org.gnome.Vino prompt-enabled true
    org.gnome.Vino disable-xdamage false
    org.gnome.Vino authentication-methods ['none']
    org.gnome.Vino network-interface ''
    org.gnome.Vino require-encryption false
    org.gnome.Vino mailto ''
    org.gnome.Vino lock-screen-on-disconnect false
    org.gnome.Vino vnc-password '1234'


In enabled state::

    org.gnome.Vino notify-on-connect true
    org.gnome.Vino alternative-port uint16 5900
    org.gnome.Vino disable-background false
    org.gnome.Vino use-alternative-port false
    org.gnome.Vino icon-visibility 'client'
    org.gnome.Vino use-upnp false
    org.gnome.Vino view-only false
    org.gnome.Vino prompt-enabled false
    org.gnome.Vino disable-xdamage false
    org.gnome.Vino authentication-methods ['vnc']
    org.gnome.Vino network-interface ''
    org.gnome.Vino require-encryption false
    org.gnome.Vino mailto ''
    org.gnome.Vino lock-screen-on-disconnect false
    org.gnome.Vino vnc-password '1234'

Let's find the difference with `diff`_ between disabled enabled::

    7,8c7,8
    < org.gnome.Vino view-only true
    < org.gnome.Vino prompt-enabled true
    ---
    > org.gnome.Vino view-only false
    > org.gnome.Vino prompt-enabled false
    10c10
    < org.gnome.Vino authentication-methods ['none']
    ---
    > org.gnome.Vino authentication-methods ['vnc']

So in theory to enable we need to do the following::

    sudo gsettings set org.gnome.Vino notify-on-connect false
    sudo gsettings set org.gnome.Vino view-only false
    sudo gsettings set org.gnome.Vino prompt-enabled false
    sudo gsettings set org.gnome.Vino authentication-methods "['vnc']"
    sudo gsettings set org.gnome.Vino vnc-password '1234'

It doesn't change the settings, more over `gsettings`_ over ssh don't work: https://stackoverflow.com/a/58222395. work around!?::

    sudo su $USER -s /bin/bash -c 'XDG_RUNTIME_DIR=/run/user/$UID DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/$UID/bus gsettings set org.gnome.Vino notify-on-connect false'
    sudo su $USER -s /bin/bash -c 'XDG_RUNTIME_DIR=/run/user/$UID DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/$UID/bus gsettings set org.gnome.Vino view-only false'
    sudo su $USER -s /bin/bash -c 'XDG_RUNTIME_DIR=/run/user/$UID DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/$UID/bus gsettings set org.gnome.Vino prompt-enabled false'
    sudo su $USER -s /bin/bash -c 'XDG_RUNTIME_DIR=/run/user/$UID DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/$UID/bus gsettings set org.gnome.Vino authentication-methods "['vnc']"' //errors out
    sudo su $USER -s /bin/bash -c 'XDG_RUNTIME_DIR=/run/user/$UID DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/$UID/bus gsettings set org.gnome.Vino vnc-password '1234''

This errors out at 4th command. Let's pause for today!

----


**Update:** Apr 24, 2020


Trail 02
--------
Development
```````````
We will pick up from where we left. To fix the error in the 4th command do::

    sudo su $USER -s /bin/bash -c 'XDG_RUNTIME_DIR=/run/user/$UID DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/$UID/bus gsettings set org.gnome.Vino authentication-methods [\"vnc\"]'

Yes! We can change the setting from terminal over SSH. The commands above has changed the `Screen Share` setting to **put a check mark** on `Allow connections to control the screen` and toggled the radio button from `New connections must ask for access` to `Require a password` but the password field is empty. 🤦‍♂️  So this somewhat works but need more work. Maybe we confues the command with nesed ``'`` and the begaining of the password with ``'`` ended the command and took a empty password. Let's encode the password with and ``"`` and escape the ``"`` with ``\``::

    sudo su $USER -s /bin/bash -c 'XDG_RUNTIME_DIR=/run/user/$UID DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/$UID/bus gsettings set org.gnome.Vino vnc-password \"1234\"'

This doesn't work as well nor ``"`` without ``\`` and just the text ``1234``. While reading more on it I found this: https://askubuntu.com/a/12195 where it say the **password is base64 encoded**. Let's test this with simple base64 encoded password, ``1234``. We can encode the password, ``1234`` with the `base64`_ tool like this::

    echo -n 1234 | base64

The output is::

    MTIzNA==

Now if we replace ``1234`` with the base64 encoded string, we get::

    udo su $USER -s /bin/bash -c 'XDG_RUNTIME_DIR=/run/user/$UID DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/$UID/bus gsettings set org.gnome.Vino vnc-password MTIzNA=='

This works!! Let's automate the base64 encoding and reduce one step::

    sudo su $USER -s /bin/bash -c 'XDG_RUNTIME_DIR=/run/user/$UID DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/$UID/bus gsettings set org.gnome.Vino vnc-password $(echo -n 1234 | base64)'

Now if we change the password all we have to do is replace the ``1234`` in this command. We are one step closer to finish this. Now all we need is to toggle the ``Screen Sharing`` button on. 

After spending a long time in web search and reading forum post I get to the conclusion that that is not meant to be done via CLI and settled for a solution that came with the answer regarding password (https://askubuntu.com/a/12195) which is running the Vino server manually from the terminal::

    /usr/lib/vino/vino-server

If we are using SSH, the ``-X`` flag of `openssh-client`_ must be used which **Enables X11 forwarding** or we will the following error::

    Unable to init server: Could not connect: Connection refused
    Cannot open display: 
    Run 'vino-server --help' to see a full list of available command line options

Now let's try to connet to our remote machine with `Remmina`_. We will do the following:

- open Remmina
- click the plus button at the top left
- give a identifiable name in the `Name` field
- select `VNC - Virtual Network Computing` from `Protocol` drop down list
- put remove machine IP address in the `Server` field
- optionally, put the password in clear text ie. ``1234`` in `User password` field, if not it would we will be prompted for password every time we connect.
- now click on `Save and Connect`

It is surely taking a bit time to connect. We can see the log in our remote machine terminal where we start the Vino server. After a while we see it connect but what is this? We are seeing the client machine screen not the remote one! I am guessing this is problem with the X Server ``DISPLAY`` variable. Let's export this and try to start the server again::

    export DISPLAY=:0

Now we can see our remote machine's desktop screen.

We still have one caveat that is when we connect to the remote machine it shows a notification::

    Another user is controlling your desktop
    A user on the computer '$IP' is remotely controlling your desktop.

We can reset all changes done with `gsettings`_ with::

    sudo su $USER -s /bin/bash -c 'XDG_RUNTIME_DIR=/run/user/$UID DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/$UID/bus gsettings reset-recursively org.gnome.Vino' 


Result
------
As of Apr 24, 2020, We can access remote machine with one problem: notification on remote machine. Here is how we do it::

    ssh -X user2@remote-machine-ip

    sudo -v

    sudo su $USER -s /bin/bash -c 'XDG_RUNTIME_DIR=/run/user/$UID DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/$UID/bus gsettings set org.gnome.Vino notify-on-connect false'
    sudo su $USER -s /bin/bash -c 'XDG_RUNTIME_DIR=/run/user/$UID DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/$UID/bus gsettings set org.gnome.Vino view-only false'
    sudo su $USER -s /bin/bash -c 'XDG_RUNTIME_DIR=/run/user/$UID DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/$UID/bus gsettings set org.gnome.Vino prompt-enabled false'
    sudo su $USER -s /bin/bash -c 'XDG_RUNTIME_DIR=/run/user/$UID DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/$UID/bus gsettings set org.gnome.Vino authentication-methods [\"vnc\"]'
    sudo su $USER -s /bin/bash -c 'XDG_RUNTIME_DIR=/run/user/$UID DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/$UID/bus gsettings set org.gnome.Vino vnc-password $(echo -n 1234 | base64)'

    export DISPLAY=:0
    /usr/lib/vino/vino-server

Be sure to change the password form ``1234`` to something to suit your need. When we are done, it would be recommended to reset the settings::

    sudo su $USER -s /bin/bash -c 'XDG_RUNTIME_DIR=/run/user/$UID DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/$UID/bus gsettings reset-recursively org.gnome.Vino' 


    

Mislenious
----------
Source
``````
- `GNOME Wiki!: Using GSettings: <https://developer.gnome.org/GSettings/>`_

- https://askubuntu.com/questions/304017/how-to-set-up-remote-desktop-sharing-through-ssh
- https://www.howtogeek.com/429190/how-to-set-up-remote-desktop-on-ubuntu/
- https://askubuntu.com/questions/4474/enable-remote-vnc-from-the-commandline#22354
- https://help.ubuntu.com/community/VNC/Servers
- https://askubuntu.com/questions/4474/enable-remote-vnc-from-the-commandline
- https://wiki.archlinux.org/index.php/Vino

.. _gsettings: https://manpages.ubuntu.com/manpages/xenial/en/man1/gsettings.1.html
.. _base64: https://linux.die.net/man/1/base64
.. _openssh-client: https://linux.die.net/man/1/ssh
.. _diff: https://linux.die.net/man/1/diff
.. _Remmina: https://remmina.org/
