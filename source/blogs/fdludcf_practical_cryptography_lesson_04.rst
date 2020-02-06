fDLuDCf's Practical Cryptography: Lesson 04
===========================================
`< Blog <../blog.html>`_

fDLuDCf's Practical Cryptography DLC: Block Cipher Operation Modes

Created on: 2020-02-05

.. warning:: This is my class-note for `fDLuDCf's Practical Cryptography DLC <https://dle.asiaconnect.bdren.net.bd/upcoming_event/practical-cryptography>`_. I typed out what I thought to be importent and note worthy from the lecture and the slides. This is by no means guilde or complete reference for the course.

.. warning:: this note has numeras spelling mistakes and not yet fixed.


Class Slides
------------
The slides for Lesson 01 is available `here <https://dle.asiaconnect.bdren.net.bd/DLE-3/L4(CryptoModes).pdf>`_.


Class Video
-----------
The video for all lessons are available in the `video page <https://dle.asiaconnect.bdren.net.bd/dle-course-3-practical-cryptography/>`_


Notes
-----
- review of last class
- the following converts block cipher to stream cipher 
    - Cipher feedback (CFB)
    - Output Feed Back(OFB) 
    - Counter (CTR)
- Cipher feed back (CFB)
    - couldn't understand from lecture so watched this: https://youtu.be/Xm37066R38E
- Output Feed Back(OFB)
    - not clearly understooed
- Counter (CTR)
    - use use counter that starts for a number and increases by one
    - each counter is enctypted with the key
    - the encrypted counter and plain text is XOR-ed to produce ciphertext
    - it goes on until finished
- advantage of (CTR)
    - can do parallal process
- GCM block mode
    - advantage is that we can check the intrigity of the message
- how GCM works
    - take an initial value (IV), do XOR (speculating as not clear from lecture) with counter 0 value
    - enctypt the XOR-ed value
    - increase counter 
    - use the value of first step as next steps IV do XOR (speculating as not clear from lecture) with counter 1 and then encrypt it.
    - XOR the encrypted value and plain text to get the ciphertext
    - now again XOR the ciphertext with Auth data which will be used as the Auth data for next step
    - in the final round we XOR Auth data, length of the key and enctypted the XOR-ed value of second step to produce an Auth Tag
- Use of GCM
    - used in networking with AES so called AES-GCM Authinticated Encryption
    - Galios hash function [see more at slide 28]
    - for a network packet with header, sequence and data, AES-GCM usages the header as Additional Auth data, sequence as IV and data as plain-text and produces a new packet with same header, sequence and encrypted ciphertext and a new auth tag as ICV
- IDEA
- Blowfish
- RC5
    - was used by WAP
- Cast-128
- Demo in Java
- Key Escrow Standerd
    - devide the key in two part and put one to escrow agency and another to govt
    - never got implemented due to public opposition
- advantage and disadvantage [see slide]

Source
------

