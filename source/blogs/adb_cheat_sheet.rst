ADB Cheat Sheet
===============
A quick reference to `ADB <https://developer.android.com/studio/command-line/adb>`_.


see devices
-----------
To see the list of all connected devices [1]_::

     adb devices -l

list all packages
-----------------
To see the list of all packages [2]_::

    adb shell 'pm list packages'

uninstall an app
----------------
To uninstall an app [3]_::

    adb uninstall -k --user 0 $package

backup system and app data
--------------------------
To backup system and app data but not the apps [4]_::

    adb backup -all

By default it saves device data to the platform-tools folder as ``backup.ab``

backup system and app data to a file
------------------------------------
To backup system and app data to a file but not the apps [4]_::

    adb backup -all -f $path_to_backup_file.ab

restore data
------------
To restore data [4]_::

    adb restore $path_to_backup_file.ab

get current activity
--------------------
TO see the current activity [5]_::

    adb shell dumpsys window windows | grep -E 'mCurrentFocus|mFocusedApp'

start an application
--------------------
To start an application aka an activity of an application [6]_::

    adb shell am start -n com.package.name/com.package.name.ActivityName

scroll screen
--------------
To scroll up and down [7]_::

    adb shell input swipe 300 300 500 1000 #up

    adb shell input swipe 500 1000 300 300 #down


send text
---------
To send text using virtual keyboard [8]_::

    adb shell input text "Hello World"

send keyevent
-------------
To send keyevent as physical keyboard [9]_::

    adb shell input keyevent 66 #66 is key_code for enter

List of all `key_code <https://developer.android.com/reference/android/view/KeyEvent>`_

send tap
--------
To tap aka click on screen [10]_::

    adb shell input tap x y

see log of a package
--------------------
to see log of a specific package [11]_::

    adb shell "logcat --pid=$(pidof -s <package_name>)"


adb over wifi
-------------
we can use adb over wifi or specifically with a tcp connection [12]_ .to use adb over wifi, first connect the phone via usb and enable usb debug. then list all device::

    adb devices

this should give a output like this::

    device_name    some_number

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




Source
------
.. [1] `Query for devices <https://developer.android.com/studio/command-line/adb#devicestatus>`_
.. [2] `Android: ADB – List Installed Package Names <https://stackpointer.io/mobile/android-adb-list-installed-package-names/416/>`_
.. [3] `How to uninstall a system app using adb uninstall command (NOT remove via rm or any other way) <https://android.stackexchange.com/a/186586>`_
.. [4] `How to Backup Your Entire Android Device to PC <https://www.technipages.com/how-to-backup-your-entire-android-device>`_
.. [5] `ADB - Android - Getting the name of the current activity <https://stackoverflow.com/a/13212310>`_
.. [6] `How to start an application using android ADB tools? <https://stackoverflow.com/a/4567928>`_
.. [7] `How can I scroll an application using adb? <https://stackoverflow.com/a/39190185>`_
.. [8] `ADB Shell Input Events: answered by Rene Barbosa <https://stackoverflow.com/a/28969112>`_
.. [9] `ADB Shell Input Events: answered by LionCoder <https://stackoverflow.com/a/8483797>`_
.. [10] `How to use ADB to send touch events to device using sendevent command? <https://stackoverflow.com/a/5392547>`_
.. [11] `adb shell Logcat with Package Name <https://stackoverflow.com/a/32737594/5350059>`_
.. [12] `How can I connect to Android with ADB over TCP? <https://stackoverflow.com/a/58334911/5350059>`_
