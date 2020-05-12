ADB Cheat Sheet
===============
`< Blog <../blog.html>`_

A quick reference to `ADB <https://developer.android.com/studio/command-line/adb>`_.

Created on: 2019-02-03

Tag: `cheat_sheet <tag_cheat_sheet.html>`_

see devices
-----------
To see the list of all connected devices::

     adb devices -l
     
source: `Query for devices <https://developer.android.com/studio/command-line/adb#devicestatus>`_

list all packages
-----------------
To see the list of all packages::

    adb shell 'pm list packages'

source: `Android: ADB – List Installed Package Names <https://stackpointer.io/mobile/android-adb-list-installed-package-names/416/>`_

uninstall an app
----------------
To uninstall an app::

    adb uninstall -k --user 0 $package

source: `How to uninstall a system app using adb uninstall command (NOT remove via rm or any other way) <https://android.stackexchange.com/a/186586>`_

backup system and app data
--------------------------
To backup system and app data but not the apps::

    adb backup -all

By default it saves device data to the platform-tools folder as ``backup.ab``

source: `How to Backup Your Entire Android Device to PC <https://www.technipages.com/how-to-backup-your-entire-android-device>`_

backup system and app data to a file
------------------------------------
To backup system and app data to a file but not the apps::

    adb backup -all -f $path_to_backup_file.ab

source: `How to Backup Your Entire Android Device to PC <https://www.technipages.com/how-to-backup-your-entire-android-device>`_

restore data
------------
To restore data::

    adb restore $path_to_backup_file.ab

source: `How to Backup Your Entire Android Device to PC <https://www.technipages.com/how-to-backup-your-entire-android-device>`_

backup, modify and restore a specific app
-----------------------------------------
to backup and restore a specific app, first list all the packages with::

    adb shell pm list packages

Now backup the specific package with::

    adb backup -f com.whatsapp.ab -noapk com.whatsapp

The command above indicates that we want to backup ``com.whatsapp`` package to ``com.whatsapp.ab`` file as indicated with the ``-f`` flag. The `.ab` says it is an `Adroid Backup` file. The ``-noapk`` flag indicates that we don't want the ``.apk`` file to be backed up. Now we should see a confirmation dialog prompt to start the backup. The backup will not start until we press **Back up my data**.

We can convert the ADB backup file to a TAR archive. First we need to stripe the 24-bite header and the use `openssl`_ to decompress the raw zlib data::

    dd if=com.whatsapp.ab ibs=24 skip=1 | openssl zlib -d > com.whatsapp.tar

Or we can use `tail`_ command instead of `dd`_::

    tail -c +25 com.whatsapp.ab | openssl zlib -d > com.whatsapp.tar

Now it is plain simple decompress with `tar`_::

    tar xvf com.whatsapp.tar

To restore just do::

    adb restore com.whatsapp.ab

But we have to take one more step to add 24-bite header to the ``.ab`` file if we changed the contains. For this we will also need the original ``.ab`` file.::

    dd if=com.whatsapp.ab ibs=24 count=1 of=com.whatsapp-restore.ab ; openssl zlib -in com.whatsapp.tar >> com.whatsapp-restore.ab

We can also use the `head`_ command to do that as well::

    head -c +24 com.whatsapp.ab > com.whatsapp-restore.ab ; openssl zlib -in com.whatsapp.tar >> com.whatsapp-restore.ab

Now restore it like before::

    adb restore com.whatsapp-restore.ab

source: https://stackpointer.io/mobile/android-adb-backup-extract-restore-repack/372/ and https://forum.xda-developers.com/showthread.php?t=2011811


get current activity
--------------------
TO see the current activity::

    adb shell dumpsys window windows | grep -E 'mCurrentFocus|mFocusedApp'

source: `ADB - Android - Getting the name of the current activity <https://stackoverflow.com/a/13212310>`_

start an application
--------------------
To start an application aka an activity of an application::

    adb shell am start -n com.package.name/com.package.name.ActivityName

source: `How to start an application using android ADB tools? <https://stackoverflow.com/a/4567928>`_

scroll screen
--------------
To scroll up and down::

    adb shell input swipe 300 300 500 1000 #up

    adb shell input swipe 500 1000 300 300 #down

source: `How can I scroll an application using adb? <https://stackoverflow.com/a/39190185>`_

send text
---------
To send text using virtual keyboard::

    adb shell input text "Hello World"

source: `ADB Shell Input Events: answered by Rene Barbosa <https://stackoverflow.com/a/28969112>`_

send keyevent
-------------
To send keyevent as physical keyboard::

    adb shell input keyevent 66 #66 is key_code for enter

List of all `key_code <https://developer.android.com/reference/android/view/KeyEvent>`_

source: `ADB Shell Input Events: answered by LionCoder <https://stackoverflow.com/a/8483797>`_

send tap
--------
To tap aka click on screen::

    adb shell input tap x y

source: `How to use ADB to send touch events to device using sendevent command? <https://stackoverflow.com/a/5392547>`_

see log of a package
--------------------
to see log of a specific package ::

    adb shell 'logcat --pid=$(pidof -s <package_name>)'

source: `adb shell Logcat with Package Name <https://stackoverflow.com/a/32737594/5350059>`_

adb over wifi
-------------
we can use adb over wifi or specifically with a tcp connection. To use adb over wifi, first connect the phone via usb and enable usb debug. then list all device::

    adb devices

this should give a output like this::

    device_id    device

now check the ip of the android device with::

    adb shell ifconfig

output::

    wlan0     Link encap:UNSPEC    Driver icnss
              inet addr:XXX.XXX.X.XX  Bcast:XXX.XXX.X.XXX

take note of the ip address after ``inet addr``. we will need it later. now restart tcpip at some port with::

    adb tcpip $port
    
for example 5555::

    adb tcpip 5555

you can disconnect the use now. to connect to the device now just give the following command::

    adb connect $ip:$port

like::

    adb connect 192.168.1.4:5555

source: `How can I connect to Android with ADB over TCP? <https://stackoverflow.com/a/58334911/5350059>`_ and `Android Debug Bridge (adb) | Android Developers: Connect to a device over Wi-Fi <https://developer.android.com/studio/command-line/adb#wireless>`_

take a screenshot
-----------------
to take a screenshot::

    adb exec-out screencap -p > screen.png

https://stackoverflow.com/a/37191719/5350059

or save it in phone then pull::

    adb shell /system/bin/screencap -p /sdcard/screenshot.png
    adb pull /sdcard/screenshot.png screenshot.png

source: `which commands line are used to take a screenshot on android device (except screencap) <https://stackoverflow.com/a/32883890/5350059>`_

change setting with adb
-----------------------
changes are divided into 3 namespace: system, secure, global. we can `get`, `put`, `delete` individual keys and `list` all in a namespace. to `list` all in system::

    adb shell settings --user 0 list system

`get`, `put` and `delete` the same::

    adb shell settings --user 0 get $namespace $key
    adb shell settings --user 0 put $namespace $key $value
    adb shell settings --user 0 delete $namespace $key

source: `adb command to open settings and change them <https://stackoverflow.com/a/53319647/5350059>`_

limit the number of connected devices in hotspot
------------------------------------------------
::

    adb shell settings --user 0 put system hotspot_max_station_num $num # num=0-6 where 0 is unlimited

turn on WIFI
------------
::

    adb shell su -c 'svc wifi enable'

turn off WIFI
-------------
::

    adb shell su -c 'svc wifi disable'


source: https://stackoverflow.com/a/10038568

.. note:: both of this requires root access

specify device among multiple devices
-------------------------------------
to specify particular device among multiple devices::

    adb -s device_id shell

source: https://stackoverflow.com/a/14655015
source: https://developer.android.com/studio/command-line/adb#directingcommands

copy files to/from a device
---------------------------
to copy files to a device::

    adb push local remote

to copy files from a device::

    adb push local remote

source: https://developer.android.com/studio/command-line/adb#copyfiles

launch fragments
----------------
to launch fragments::

    adb shell am start -n com.android.settings/com.android.settings.SubSettings -e :android:show_fragment com.android.settings.users.UserSettings

The `-e :android:show_fragment` part is important here.

source: https://stackoverflow.com/a/21844594

get events
----------
to get events::

    adb shell su -- getevent -lt /dev/input/event1

source: `Getevent | Android Open Source Project <https://source.android.com/devices/input/getevent.html>`_

https://github.com/spion/adbfs-rootless

Source
------

.. _openssl: https://linux.die.net/man/1/openssl
.. _tail: https://linux.die.net/man/1/tail
.. _dd: https://linux.die.net/man/1/dd
.. _tar: https://linux.die.net/man/1/tar
.. _head: https://linux.die.net/man/1/head
