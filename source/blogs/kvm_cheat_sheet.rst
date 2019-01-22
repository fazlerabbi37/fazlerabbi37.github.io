KVM Cheat Sheet
===============
A quick reference of KVM.

create a .img file of 2GB fo qcow2 format
qemu-img create -f qcow2 test.img 2g

#install a domain with ISO file
sudo virt-install --virt-type=kvm --name $name --ram $ram_size_in_mb --vcpus=2 --hvm --network=bridge:$bridge_name --cdrom=$iso_location --disk $img_file_location,size=$disk_size_in_gb

#make a domain form a exising disk image (.img) file
#make a copy of a $old_img and give it a different name $new_img
sudo virt-install --virt-type=kvm --name $name --ram 512 --vcpus=1 --hvm --network=bridge:$bridge_name --import --disk $new_img_file_location

#make guest from linux base
sudo cp ubuntu_1604_server.img $name.img;sudo virt-install --virt-type=kvm --name $name --ram 1024 --vcpus=1 --hvm --import --disk $name.img

#install windows 10 in KVM
virt-install --name=windows10 --ram=4048 --vcpus=4 --os-type=windows --os-variant=win8.1 --network=bridge:br0 --cdrom=Windows_10.iso --disk windows10,size=40

#make guest from win base
sudo cp windows10.img $name.img;sudo virt-install --name $name --ram 4048 --vcpus=4 --hvm --import --disk $name.img
