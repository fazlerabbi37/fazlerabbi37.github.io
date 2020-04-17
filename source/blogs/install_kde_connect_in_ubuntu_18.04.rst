Install KDE Connect in Ubuntu 18.04
===================================
`< Blog <../blog.html>`_

Installing KDE Connect in Ubuntu 18.04 LTS.

Created on: 2018-08-29

What is KDE Connect?
`Answer from KDE community Wiki <https://community.kde.org/KDEConnect#What_is_KDE_Connect.3F>`_ ::

    KDE Connect is a project to communicate across all your devices. For example, with KDE Connect you can receive your phone notifications on your
    desktop computer, control music playing on your desktop from your phone, or use your phone as a remote control for your desktop.

* Implements a secure communication protocol over the network, and allows any developer to create plugins on top of it.
* Has a component that you install on your desktop.
* Has a KDE Connect client app you run on your phone.

This YouTube `video <https://www.youtube.com/watch?v=KkCFngNmsh0>`_ from 2013 demonstrates some other cool features.

I have been using KDE Connect for a while now. It is very useful for sending files from PC to Android and vice versa but I have found it most useful while copying text in PC and pasting it on the Phone. 

On Ubuntu 18.04 LTS we can install KDE Connect using the following command::

    sudo apt install kdeconnect

We need to install the KDE Connect app on Android using `F-Droid <https://f-droid.org/en/packages/org.kde.kdeconnect_tp>`_ or `Google Play <https://play.google.com/store/apps/details?id=org.kde.kdeconnect_tp>`_.

Coming back to PC, we will search for KDE and we should see two app with same icon one named ``KDE Connect Indicator`` and another ``KDE Connect Settings``. Click on ``KDE Connect Settings`` and refresh the list. Now we should see the Android phone with KDE Connect installed on it. After paring it we are ready to go.

Plugin: Run commands
--------------------
The run commands plugin allows user to execute console commands remotely. Some useful ones that I use::

    Name            Command
    ----            -------
    Lock screen     loginctl lock-session
    Reboot          systemctl reboot
    Shutdown        systemctl poweroff
    Suspend         systemctl suspend
    Unlock screen   loginctl unlock-session
    Kill App        xkill

To use this, open KDE Connect Settings, select the device and scroll down in the Available plugins and find Run commands plugin. Next, click the while box on the right of the plugin to configure it. This will show a box of with two columns Name and Command. Double click in the empty field and start writing. When finished click OK to save. See more at: `KDE Connect Tutorials: Adding commands <https://userbase.kde.org/KDE_Connect/Tutorials/Adding_commands>`_ and `KDE Connect Tutorials:Useful commands <https://userbase.kde.org/KDE_Connect/Tutorials/Useful_commands>`_

**Update: Mar 08, 2020**

I was curious to know if there was a ``config`` file where this commands are being stored. A quick tour of ``~/.config/`` directory and we see that the commands are saved as `ByteArray` inside the ``~/.config/kdeconnect/$UNIQUE_DEVICE_ID/kdeconnect_runcommand/config`` file.
