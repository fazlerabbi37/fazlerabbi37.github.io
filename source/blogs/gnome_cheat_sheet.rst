GNOME
=====
A quick reference to Gnome.

make sure you have gnome-tweak-tool installed. ``sudo apt install gnome-tweak-tool``

run .sh file by double clicking on them
=======================================
::

    #using gsettings (source: http://askubuntu.com/a/378473/502875)
    gsettings set org.gnome.nautilus.preferences executable-text-activation ask
    #using dconf (source: http://askubuntu.com/a/421537/502875)
    dconf write /org/gnome/nautilus/preferences/executable-text-activation "'launch'"

Ubunut side panel pin or favourite (source: http://askubuntu.com/a/171723/502875)
=================================================================================
::

    #remove all pin
    gsettings set com.canonical.Unity.Launcher favorites "[]"
    #pin allpication
    gsettings set com.canonical.Unity.Launcher favorites "['application://firefox.desktop', 'unity://running-apps', 'application://evolution.desktop', 'unity://devices']"
    #get pin item
    gsettings get com.canonical.Unity.Launcher favorites

Additional Workspaces in Gnome (source: http://askubuntu.com/a/370048/502875)
=============================================================================
::

    #get n workspaces vertically
    gsettings set org.compiz.core:/org/compiz/profiles/unity/plugins/core/ vsize n
    #get n workspaces horizontally
    gsettings set org.compiz.core:/org/compiz/profiles/unity/plugins/core/ hsize n

remove Workspace Switcher launcher icon from the Unity launcher (source: https://askubuntu.com/a/286344/502875)
===============================================================================================================
::

    gsettings get com.canonical.Unity.Launcher favorites
    #should returen something like
    #['application://nautilus.desktop', 'application://chromium-browser.desktop', 'application://ubuntu-software-center.desktop', 'application://ubuntuone-installer.desktop', 'application://ubuntu-amazon-default.desktop', 'application://UbuntuOneMusiconeubuntucom.desktop', 'application://gnome-control-center.desktop', 'unity://running-apps', 'unity://expo-icon', 'unity://devices']
    #copy the whole string and remove 'unity://expo-icon' and give the following command, don't forget the ""
    gsettings set com.canonical.Unity.Launcher favorites "['application://nautilus.desktop', 'application://chromium-browser.desktop', 'application://ubuntu-software-center.desktop', 'application://ubuntuone-installer.desktop', 'application://ubuntu-amazon-default.desktop', 'application://UbuntuOneMusiconeubuntucom.desktop', 'application://gnome-control-center.desktop', 'unity://running-apps', 'unity://devices']"

always show menu items in Unity
===============================
::

    #switch on:
    gsettings set com.canonical.Unity always-show-menus true
    #switch off:
    gsettings set com.canonical.Unity always-show-menus false

remove the switch user account option in Unity
==============================================
::

    gsettings set com.canonical.indicator.session user-show-menu false

lock screen
===========

#gnome gnome-screensaver-command -l #xfce xflock4

chnage background picture
=========================
::

    #gnome
    gsettings set org.gnome.desktop.background picture-uri "file:///location/file.extension"

see month and date on main title bar
====================================
::
    gsettings set org.gnome.desktop.interface clock-show-date true

`উবুন্টু বাংলাদেশ [Ubuntu Bangladesh] <https://www.facebook.com/groups/ubuntubd/permalink/10156552582077217/>`_
hide user from gear button
==========================
::

    gsettings set com.canonical.indicator.session user-show-menu false