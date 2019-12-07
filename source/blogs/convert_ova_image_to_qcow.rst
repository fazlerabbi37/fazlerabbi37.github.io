Convert OVA image to QCOW
=========================
`< Blog <../blog.html>`_

Converting VirtualBox or VMware favoured OVA image to KVM or QEMU favoured QCOW image.

Created on: 2018-10-28

At first, we need to install ``qemu-utils``, which we can do by this command::

     sudo apt-get install qemu-utils


Then we will extract the ``.ova`` file using ``tar`` command::

    tar -xvf $image.ova

Put your image name in the place of $image. We should see ``$image.mf``, ``$image.ovf`` and ``$image.vmdk`` or ``$image.vdi`` files. The tool we are using ``qemu-img`` supports both ``.vmdk`` and ``.vdi`` file. To verify supported files list use the following command::

    qemu-img -h | tail -n1

Finally, we will use the ``qemu-img`` to convert the ``$image.vmdk`` or ``$image.vdi`` file into ``$image.qcow2`` or ``$image.img`` format. For ``.vdi`` image::

    qemu-img convert -O qcow2 $image.vdi $image.qcow2

Or ::

    qemu-img convert -O qcow2 $image.vdi $image.imag

For ``.vmdk`` image::

    qemu-img convert -O qcow2 $image.vmdk $image.qcow2

Or ::

    qemu-img convert -O qcow2 $image.vmdk $image.img

Source
------
- `How to convert OVA image to QCOW2 format on Linux <http://ask.xmodulo.com/convert-ova-to-qcow2-linux.html>`_
