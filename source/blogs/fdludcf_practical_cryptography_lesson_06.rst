fDLuDCf's Practical Cryptography: Lesson 06
===========================================
`< Blog <../blog.html>`_

fDLuDCf's Practical Cryptography DLC: Public Key Cryptography Part 2 

Created on: 2020-02-23

Tag: `cryptography <blogs/tag_cryptography.html>`_


.. warning:: This is my class-note for `fDLuDCf's Practical Cryptography DLC <https://dle.asiaconnect.bdren.net.bd/upcoming_event/practical-cryptography>`_. I typed out what I thought to be importent and note worthy from the lecture and the slides. This is by no means guilde or complete reference for the course.

.. warning:: this note has numeras spelling mistakes and not yet fixed.


Class Slides
------------
The slides for Lesson 06 is available `here <https://dle.asiaconnect.bdren.net.bd/DLE-3/L6(PublicKey).pdf>`_.


Class Video
-----------
The video for all lessons are available in the `video page <https://dle.asiaconnect.bdren.net.bd/dle-course-3-practical-cryptography/>`_


Notes
-----

- previous lacture reivew
    - it is possible to do a man in the middle attack in diffie-hellman algo
- RSA encryption
    - see previous lacture for how it works
    - need to get 4 number p,q,e and d
    - lets assume p=11, q=17, e=7 and d=23, so n=187
    - the sender knows e=7 and n=187 and the plain-text to encrypt, P=88 which is less n
    - the sender will encrypt plain-text P using the equation 
        - C = P :sup:`e` mod n
          => 88 :sup:`7` mod 187
          => [(88 :sup:`4` mod 187) x (88 :sup:`2` mod 187) x (88 :sup:`1` mod 187)] mod 187
        - C = 11 [more details on slide 15]
    - the reciepient knows d=23 and n=187 and the cipher-text to decrypt, C=11
        - P = C :sup:`d` mod n
          => 11 :sup:`23` mod 187
          => [(11 :sup:`1` mod 187) x (11 :sup:`2` mod 187) x (11 :sup:`4` mod 187) x (11 :sup:`8` mod 187) x (11 :sup:`8` mod 187)] mod 187
        - P = 88 [more details on slide 16]
- RSA signature
    - signature works almost same as encryption
    - need to get 4 number p,q,e and d
    - get n from p and q
    - signing [more details on slide 22]
        - now instead of encryption with the public key e we encryption with the private key d. so the equation becomes S = P :sup:`d` mod n, where S is the signature.
        - now we sent both P and S indecating that P is the message and S is the signature.
    - verify [more details on slide 23]
        - recives P and S
        - get the public key of sender e and n
        - S :sup:`e` mod n
        - if the result of above step is equal to P conferms the signatory
- Typical Digital Signature
    - sender
        - has a document or data
        - calculates the hash of document or data
        - then hash is signed using RSA 
        - the signed has is attached to document or data which becomes signed document or data
        - then that signed document or data is transmited to the reciver
    - reciver
        - receives signed document or data
        - seperaed the signed hash and document or data
        - get's the public key of sender
        - verifies the signed hash using the publick key of sender
        - calculates the hash of the document or data
        - if the calculated has and the verified hash matches the signature is valid
- Factoring a product of two large primes
    - see slide 25
- Quantum Computing algo for prime factoring
    - Shor algo
    - Peter Shor
    - 1994
    - this shows that prime factoring can be done in seconds on a quantum computer
    - so if quantum computer can start workign efficeintelly RSA would become volnurable
- Demo Code
- Elliptic Curve Cryptography (ECC)
    - an elliptic curve is a set of solution to the equation y :sup:`2` = x :sup:`3` + ax :sup:`2` + bx + c
    - the curve is not an ellipse but it is called elliptic because of historical reason
    - EC usage
        - number theory
        - modern physics: string theory
        - cryptography
    - in ECC we defind 2 primitive operations called point adition and point multiplication
    - in point addition we take two points P and Q in the curve, draw a straight line through them until it intersectes the curve a point -R. then we take the reflection of the point -R on x asix and we get R which is equal to P+Q. [see more at slide 36]
    - in point doubbling we take a point P and draw a tanget on the point which intersects the curve a point -R. then we take the reflection of the point -R on x asix and we get R which is equal to 2P. [see more at slide 37]
    - scalar multiplication [see more at slide 38]
        - to multipluy P, d times we could add P d times which is the intutive approch and requires d-1 point addition
        - or we can double P, the double that previous result and so on. If d is even then number of times we need to double is squire root of d, if d is odd the the number is squire root of d-1 and 1 addition
        - for eaample to compute 17P we would strat with 2P and double that and that two more times and finaly add P so 17P=2(2(2(2P)))+P. which is 4 point dboules and one point addition
- ECC is used in crypto
    - key exchange: EC Diffie-Hellman (ECDH)
    - Digital Signature: EC Digital Signature Algo (ECDSA)
    - this are standed
    - encryption and decryption is possible but not very common
- trapdoor function of ECC
    - for Diffie-Hellman we used to compute y = g :sup:`x` (mod p) where x is a random number and private key and y is the public key.
    - here we do B = kA where A=g=generator point, k=x=randome intiger thus the private key and B=y=public key
    - they may see different but they both are same in complexity and with point addition, point doubling and scalar multiplication it is easy to generate public key but infeasable to do the reverse.
- ECDH
    - assuming two party A and B and a common generator P
    - A has a private key n :sub:`A` and public key Q :sub:`A` = n :sub:`A` x P
    - B has a private key n :sub:`B` and public key Q :sub:`B` = n :sub:`B` x P
    - they exchange their public key Q :sub:`A` and Q :sub:`B`
    - If they do a shared key computation
        - for A K = n :sub:`A` x Q :sub:`B`
        - for B K = n :sub:`B` x Q :sub:`A`
    - now the shared key is consistent because
        => K = n :sub:`A` x Q :sub:`B` = n :sub:`A` x n :sub:`B` x P = n :sub:`B` x Q :sub:`A`
    - volnurable to man in the middle attack
- ECDH example with small number
    - curve used y :sup:`2` = x :sup:`3` + 2x + 2
    - generator point G(5,1) [see more at slide 43]
    - for user A and B the agree on the curve used, generator point G, and n
    - user A picks a private key x=9 and generates xG=9G=(7,6)=X where X is the public key
    - user B picks a private key y=3 and generates yG=3G=(10,6)=Y where Y is the public key
    - shared key K for A is 9 x Y = 9 x 3G = 27G = (13,7)
    - shared key K for B is 3 x X = 3 x 9G = 27G = (13,7)
- ECDSA
    - skiped because of complexity [see more at slide 45]
- ECC compared
    - ECC is strong 
- TLS usages ECDSA with curve P-256 and X25519 being the most popular



Source
------

