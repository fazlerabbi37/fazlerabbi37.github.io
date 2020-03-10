Mysterious TP-Link SSH server
=============================
`Blog <../blog.html>`__

Why there is an SSH server running on a home router?

Created on: 2019-09-04

Tag: `useless_rnd <tag_useless_rnd.html>`_

Discovery/Query/Idea
--------------------
**Discovery:** First found with a random port search with `Port Authority <https://f-droid.org/packages/com.aaronjwood.portauthority/>`_ port scanner.

-  brand: TP-Link
-  Hardware Version: WR841N v11 00000000
-  Firmware Version: 3.16.9 Build 151021 Rel.76995n

Primary Goal
------------
Can we get shell access with SSH!?

Research
--------
-  `Nmap <https://nmap.org>`_ scan shows it usages Dropbear ``sshd``::

    # Nmap 7.60 scan initiated Wed Sep  4 03:04:09 2019 as: nmap -sC -sV -oA wr841N_v11/wr841N_v11 192.168.0.1
    Nmap scan report for _gateway (192.168.0.1)
    Host is up (0.0062s latency).
    Not shown: 996 closed ports
    PORT      STATE SERVICE VERSION
    22/tcp    open  ssh     Dropbear sshd 2012.55 (protocol 2.0)
    | ssh-hostkey: 
    |   1024 d2:b1:fa:6c:de:58:d9:17:f7:e5:dd:ba:44:37:39:d4 (DSA)
    |_  1040 f8:cc:5b:03:94:db:0c:3f:04:56:d4:76:29:51:5b:0d (RSA)
    80/tcp    open  http    TP-LINK WR841N WAP http config
    |_http-title: TL-WR841N
    1900/tcp  open  upnp    ipOS upnpd (TP-LINK TL-WR841N WAP 11.0; UPnP 1.0)
    49152/tcp open  http    Huawei HG8245T modem http config
    |_http-title: Site doesn't have a title.
    MAC Address: 84:16:F9:FC:9B:CC (Tp-link Technologies)
    Service Info: OSs: Linux, ipOS 7.0; Devices: WAP, broadband router; CPE: cpe:/o:linux:linux_kernel, cpe:/h:tp-link:wr841n, cpe:/h:tp-link:tl-wr841n, cpe:/o:ubicom:ipos:7.0, cpe:/h:huawei:hg8245t

    Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
    # Nmap done at Tue Mar  3 13:57:03 2020 -- 1 IP address (1 host up) scanned in 154.57 seconds


- If we try to log in with the router's web interface login credentials it gives the following error::

    bobcat@what-the-ssh:~/fr37/temp$ ssh admin@192.168.10.1
    admin@192.168.10.1's password: 
    PTY allocation request failed on channel 0
    shell request failed on channel 0
    bobcat@what-the-ssh:~/fr37/temp$ 

-  search with the error `dropbear ssh pty allocation request failed tplink <https://www.google.com/search?hl=en&q=dropbear%20ssh%20pty%20allocation%20request%20failed%20tplink>`_ in Google; we get this `forum post <https://community.tp-link.com/en/home/forum/topic/98265>`_ leading use to the officail `support faq <https://www.tp-link.com/en/support/faq/2462/>`_ which say it is for the usage of their `officail android app's <https://play.google.com/store/apps/developer?id=TP-LINK+Technologies+Co.,+Ltd.>`_ like `Tether <https://play.google.com/store/apps/details?id=com.tplink.tether>`_ and more.

**Update**: Mar 03, 2020

Same behaviour found with Archer C60

    -  brand: TP-Link
    -  Hardware Version: Archer C60 v2.0
    -  Firmware Version: 2.0.0 Build 20161206 rel.65407er 

**Update**: Mar 08, 2020

Surprise! Surprise! I found one router in the wild with Telnet port open. It asked for authentication which is nice, at least it is not open for all. And guess what happened when I tried the web interface login credentials. Ladies and gentleman we are dropped into the configure terminal of the router. Due to lack to time and not being very efficient with termux I neither got to collect the hardware and firmware version nor any screenshot. Will try to update soon!

Development
-----------

Result
------

From primary recon it seems the shell access is blocked so **NO** direct access to shell is possible.

Miscellaneous
-------------
- see how the ssh is denying the shell access ei. block shell access on ssh

