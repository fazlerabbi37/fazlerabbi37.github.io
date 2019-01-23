KVM Cheat Sheet
===============
A quick reference of KVM.

Make guest from ISO
-------------------
To create a new guest instance from ISO, run the following::

    sudo virt-install --virt-type=kvm --name $name --ram $ram_size_in_mb --vcpus=2 --hvm --network=bridge:$bridge_name --cdrom=$iso_location --disk $img_file_location,size=$disk_size_in_gb

Make guest from a ``.img`` file
-------------------------------
To make a guest from an existing ``.img`` file, run the following::

    sudo virt-install --virt-type=kvm --name $name --ram 512 --vcpus=1 --hvm --network=bridge:$bridge_name --import --disk $new_img_file_location

This makes possible to make one base image and then copy the image and spun a new guest. For example, let's consider we have a base image name ``ubuntu_1604_server.img`` to make a new ``$name`` guest, we do:: 

    sudo cp ubuntu_1604_server.img $name.img
    sudo virt-install --virt-type=kvm --name $name --ram 1024 --vcpus=1 --hvm --import --disk $name.img

Make a Widnows guest from ISO
-----------------------------
To make a Windows guest from ISO, run this::

    virt-install --name=windows10 --ram=4048 --vcpus=4 --os-type=windows --os-variant=win8.1 --network=bridge:br0 --cdrom=Windows_10.iso --disk windows10,size=40

Make an ``.img`` file
---------------------
We will use ``qemu-img`` to create a new ``.img`` file of 2 GB::

    qemu-img create -f qcow2 $name.img 2g

See info of an ``.img`` file
----------------------------
We can see the information of an existing ``.img`` file using ``qemu-img``::

    qemu-img info $name

Source
------
