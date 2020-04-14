GNOME Cheat Sheet
=================
`< Blog <../blog.html>`_

A quick reference to GNOME.

Created on: 2019-03-19

Tag: `cheat_sheet <tag_cheat_sheet.html>`_

.. warning:: under heavy construction and not well organized

make sure you have gnome-tweak-tool installed. ``sudo apt install gnome-tweak-tool``

run .sh file by double clicking on them
---------------------------------------
::

    #using gsettings (source: http://askubuntu.com/a/378473/502875)
    gsettings set org.gnome.nautilus.preferences executable-text-activation ask
    #using dconf (source: http://askubuntu.com/a/421537/502875)
    dconf write /org/gnome/nautilus/preferences/executable-text-activation "'launch'"

Ubunut side panel pin or favourite
----------------------------------
::

    #get pin item
    gsettings get com.canonical.Unity.Launcher favorites

    #pin allpication(s)
    gsettings set com.canonical.Unity.Launcher favorites "['application://firefox.desktop', 'unity://running-apps', 'application://evolution.desktop', 'unity://devices']"

    #remove all pin
    gsettings set com.canonical.Unity.Launcher favorites "[]"


(source: http://askubuntu.com/a/171723)

OR::

    #get pin item
    dconf read /org/gnome/shell/favorite-apps

    #pin allpication(s)
    dconf write /org/gnome/shell/favorite-apps "['org.gnome.Nautilus.desktop', 'chromium-browser.desktop']"

    #remove all pin
    dconf write /org/gnome/shell/favorite-apps "[]"

source: https://askubuntu.com/a/1082279

Additional Workspaces in GNOME
------------------------------
::

    #get n workspaces vertically
    gsettings set org.compiz.core:/org/compiz/profiles/unity/plugins/core/ vsize n
    #get n workspaces horizontally
    gsettings set org.compiz.core:/org/compiz/profiles/unity/plugins/core/ hsize n

(source: http://askubuntu.com/a/370048)

remove Workspace Switcher launcher icon from the Unity launcher
---------------------------------------------------------------
::

    gsettings get com.canonical.Unity.Launcher favorites
    #should returen something like
    #['application://nautilus.desktop', 'application://chromium-browser.desktop', 'application://ubuntu-software-center.desktop', 'application://ubuntuone-installer.desktop', 'application://ubuntu-amazon-default.desktop', 'application://UbuntuOneMusiconeubuntucom.desktop', 'application://gnome-control-center.desktop', 'unity://running-apps', 'unity://expo-icon', 'unity://devices']

    #copy the whole string and remove 'unity://expo-icon' and give the following command, don't forget the ""
    gsettings set com.canonical.Unity.Launcher favorites "['application://nautilus.desktop', 'application://chromium-browser.desktop', 'application://ubuntu-software-center.desktop', 'application://ubuntuone-installer.desktop', 'application://ubuntu-amazon-default.desktop', 'application://UbuntuOneMusiconeubuntucom.desktop', 'application://gnome-control-center.desktop', 'unity://running-apps', 'unity://devices']"


(source: https://askubuntu.com/a/286344)

always show menu items in Unity
-------------------------------
::

    #switch on:
    gsettings set com.canonical.Unity always-show-menus true
    #switch off:
    gsettings set com.canonical.Unity always-show-menus false

remove the switch user account option in Unity
----------------------------------------------
::

    gsettings set com.canonical.indicator.session user-show-menu false


lock screen
-----------
#gnome gnome-screensaver-command -l #xfce xflock4

chnage background picture
-------------------------
::

    gsettings set org.gnome.desktop.background picture-uri "file:///location/file.extension"

see month and date on main title bar
------------------------------------
::
    gsettings set org.gnome.desktop.interface clock-show-date true

`উবুন্টু বাংলাদেশ [Ubuntu Bangladesh] <https://www.facebook.com/groups/ubuntubd/permalink/10156552582077217/>`_

hide user from gear button
--------------------------
::

    gsettings set com.canonical.indicator.session user-show-menu false

disable screen lock
-------------------
To disable screen lock::

    gsettings set org.gnome.desktop.lockdown disable-lock-screen true

To enable::

    gsettings set org.gnome.desktop.lockdown disable-lock-screen false

(source: https://askubuntu.com/a/1000458)


logout a user
-------------
for 11.10 and above run::

    gnome-session-quit

in 60 seconds the user will be logged out. https://askubuntu.com/a/15796

However, if you are in a ssh connection this will not work so use::

    sudo pkill -u $username

https://askubuntu.com/a/132351


blank screen delay
------------------
::

    gsettings set org.gnome.desktop.session idle-delay $DELAY_IN_SECONDS

source: https://askubuntu.com/a/1042685

see all option for gsettings
----------------------------
::

    gsettings range $SCHEMA $KEY

source: https://askubuntu.com/a/1030558


take screenshot
---------------
::

    gnome-screenshot -d 10

This would take a screenshot with 10 seconds delay.

source: https://askubuntu.com/a/194470

Ubuntu 18.04 touchpad right click not working
---------------------------------------------
Ubuntu 18.04 touchpad right click doesn't not working when the right touchpad button is clicked because the default behavior is changed to two-finger click (just tap anywhere with two fingers). To change this to right touchpad button::

    gsettings set org.gnome.desktop.peripherals.touchpad click-method areas

source: https://askubuntu.com/a/1029445 --> https://www.omgubuntu.co.uk/2018/04/things-to-do-after-installing-ubuntu-18-04 [step 5]

see the changes done with Gnome Tweak Tool or Tweaks
----------------------------------------------------
to see the changes done with Gnome Tweak Tool or Tweaks::

    dconf watch /

Now changes done in Tweaks will be show in the terminal.

source: https://askubuntu.com/a/971577




Source
------
