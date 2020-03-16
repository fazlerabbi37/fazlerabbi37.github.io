Rebooting consumer router using CLI
===================================
`< Blog <../blog.html>`_

Don't want to use the Web Interface to reboot router? Let's see the CLI ways.

Created on: 2019-05-09

Tag: `useless_rnd <tag_useless_rnd.html>`_

Consumer router ie. TPLink, D-Link, Netgear, comes with their proprietary firmware and most of them doesn't support a CLI. I needed a way to reboot my router without using the web GUI. So here we will look at different ways to access those router and reboot them.

Telnet
------
The most common way to access a router is to use ``telnet`` client if the router supports it. [1]_::

    telnet $ip_address

Type ``username`` and ``password`` to login. Type ``help`` or ``help system`` to see all available commands. We should find a ``reboot`` command on that list of commands. We can use it to reboot the device.::

    system reboot

To reboot using telnet without user interaction (non-interactive) mode we can use the following command::

    (sleep 3;echo $username;sleep 3;echo $password;sleep 3;echo system reboot;sleep 3;) | telnet $ip

If we are using Windows, we need to go to `Control Panel` > `Turn Windows features on or off` and then enable `Telnet Client`. Then open the CMD and use the following code::

    Option explicit
    Dim oShell
    set oShell= Wscript.CreateObject("WScript.Shell")
    oShell.Run "telnet"
    WScript.Sleep 3000
    oShell.Sendkeys "open 192.168.1.1~"
    WScript.Sleep 3000
    oShell.Sendkeys "admin~"
    WScript.Sleep 3000
    oShell.Sendkeys "mypassword~"
    WScript.Sleep 3000
    oShell.Sendkeys "system reboot~"
    WScript.Sleep 3000
    oShell.Sendkeys "~"
    Wscript.Quit

We can save the code as ``.vbs`` file and use as in executable file.

If you don't have telnet enable by default, for example in Netgear search for `Netgear Telnet Enabler` or see `NTE - A Portable Program to Enable Telnet Access on Netgear Routers <http://antinode.info/nte/>`_, `NetgearTelnetEnable <https://github.com/insanid/NetgearTelnetEnable>`_ and `Unlocking the Netgear Telnet Console <https://openwrt.org/toh/netgear/telnet.console>`_.

cURL
----
We can use cURL command to reboot router. 

For TP-Link [2]_::

    curl -D -s --header "Authorization:Basic ABCdef123456" --header "Referer: http://$ip:$port/userRpm/SysRebootRpm.htm" -u "$username:$password" "http://$ip:$port/userRpm/SysRebootRpm.htm?Reboot=Reboot"

Netgear debug
-------------
While trying to figure this out I found that Netgear has a web debug page which can be access at this address: ``http://$ip/debug.htm``. [3]_   

Source
------
.. [1] `How to Automatically Reboot Your Router the Geeky Way <https://www.howtogeek.com/206620/how-to-automatically-reboot-your-router-the-geeky-way/>`_
.. [2] `Reboot TP-Link Router TL-WA7510N using Curl <https://tricksty.com/coding/reboot-tp-link-router-tl-wa7510n-using-curl>`_
.. [3] `Can I enable telnet on my R8000? <https://community.netgear.com/t5/Nighthawk-WiFi-Routers/Can-I-enable-telnet-on-my-R8000/m-p/1637900/highlight/true#M104722>`_
