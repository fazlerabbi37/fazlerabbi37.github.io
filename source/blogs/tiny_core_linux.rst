Tiny Core Linux
===============
Playing around with Tiny Core Linux, a small (11MB) Linux destro.

Created on: 2018-08-08

Install with KVM
----------------
sudo virt-install --virt-type=kvm --name core --ram 512 --vcpus=1 --hvm --network=bridge:br0 --cdrom=Core-current.iso --disk core.img,size=10

Enable SSH
----------
Download and install OpenSSH::

    tce-load -wi openssh
    
Check SSH Config file::

    ls /usr/local/etc/ssh/

If you see ``ssh_config`` file skip to next step or make a copy from ``ssh_config.example``::

    sudo cp /usr/local/etc/ssh/ssh_config.example /usr/local/etc/ssh/ssh_config

Start the SSH Service::

    sudo /usr/local/etc/init.d/openssh start

Check for status of SSH Service::

    sudo /usr/local/etc/init.d/openssh status

Returns::

    OpneSSH daemon is running


Change User Password
--------------------
To change the “tc” User Password::

    passwrd

Now type a password and hit enter; we will be asked to type the password again so type the password and hit enter again.

Source
------
 - `Configure SSH Server on Tiny Core Linux using openSSH <https://iotbytes.wordpress.com/configure-ssh-server-on-microcore-tiny-linux/>`_
