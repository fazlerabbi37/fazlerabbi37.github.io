fDLuDCf's Practical Cryptography: Lesson 05
===========================================
`< Blog <../blog.html>`_

fDLuDCf's Practical Cryptography DLC: Public Key Cryptography Part 1

Created on: 2020-02-21

.. warning:: This is my class-note for `fDLuDCf's Practical Cryptography DLC <https://dle.asiaconnect.bdren.net.bd/upcoming_event/practical-cryptography>`_. I typed out what I thought to be importent and note worthy from the lecture and the slides. This is by no means guilde or complete reference for the course.

.. warning:: this note has numeras spelling mistakes and not yet fixed.


Class Slides
------------
The slides for Lesson 01 is available `here <https://dle.asiaconnect.bdren.net.bd/DLE-3/L5(PublicKey).pdf>`_.


Class Video
-----------
The video for all lessons are available in the `video page <https://dle.asiaconnect.bdren.net.bd/dle-course-3-practical-cryptography/>`_


Notes
-----

- previous class preview
    - difference between CBC-MAC and CBC-Enc
    - combining MAC and Enc (slide 12 of this lecture)
        - MAC-AND-Enc (SSH)
        - MAC-then-Enc (SSL)
        - Enc-then-MAC (IPsec)
    - WPA2 DOSE NOT USAGES GCM, it usages Counter mode (CRT) for encryption,  Cipher Block Chaining Message Authentication Code (CBCMAC) is for integrity and CCM = CTR + CBC-MAC for confidentiality and integrity

- Why do we need public key cryptography?
    - solves the key distribution problem of private key cryptography
    - solves the scalability problem of private key cryptography
    - usages a digital signature to verify
- components of the public key cryptography
    - plain-text
    - encryption algo
    - public and private key
    - cipher-text
    - decryption alog
- generally the encryption and decryption algo are different and encryption works with public key and decryption works with private key
- how it works:
    - everyone has two key public and private 
    - sender usages the recipient's public key to encrypt the message and sent that encrypted message to recipient
    - recipient decrypts the message with his/her privet key
- *** video's that helped me understand public key cryptography [The Internet: Encryption & Public Keys](https://youtu.be/ZghMPWGXexs), [Public Key Cryptography - Computerphile](https://youtu.be/GSIDS_lvRv4)
- encryption with private key and decryption with public key is also possible but it is not secure as anyone with public key can decrypt the message. This feature can be used for message authentication. If user A encrypts a messages with his private key and If we can decrypt it with user A's public key then we can verify that it is from user A. This process is call signing. 
- use case for public key cryptography:
    - encryption and decryption: encrypt with public key
    - digital signature: encrypt with private key
    - key exchange: exchange key for symmetric encryption between two party to solve the key distribution problem
- requirements for public key cryptography:
    - computationally easy to generate public and private key
    - easy for sender encrypt message with public key 
    - easy for receiver to decrypt message with private key 
    - computationally infeasible to generate private key with known public key
    - computationally infeasible to recover message with known public key and cipher-text
    - either of the two key can be used for encryption and the other for decryption 
- popular public key cryptography algo:
    - Diffie-Hellman
    - RSA
    - ECC
- trapdoor function
    - easy to compute in one direction 
    - difficult to compute in reverse
    - Discrete Logarithms satisfies the criteria of a trapdoor function
- Discrete Logarithms
    - not clear
- Diffie-Hellman
    - published 1976, first public key algo
    - generates g, prime number p and q a prime divisor of p-1
    - randomly selects x from 1 to q-1
    - compute y = g^x (mod p)
    - not very clear
- RSA
    - dominant alog
    - all use case are possible
    - takes two prime number p and q and generates n which is the product of p and q.
    - n is public and p ad q is obtained by prime factorisation
- Relatively Prime Numbers & GCD
    - if two prime don't have common divisor except for 1, we call them relatively prime numbers
    - we can determine the greatest common divisor(GCD) of of two prime by comparing their prime factors and their lowest powers 
- Euclidean Algorithm
    - the GCD of any two large prime number can be simplified in a short time using Euclidean Algorithm
    - if a and b is divided by x then x also divides a-(k*b) for every k [proof on slide 33]
    - this process simplifies finding GCD. for example: GCD(1970,1066)
        - 1970 = 1 x 1066 + 904 so we can write GCD(1970,904)
        - this can be smplified to write GCD(2,0) meaning if we canculate GCD(2,0) we will get the GCD(1970,1066).
- Primality Testing (how do we know if a number is prime?)
    - in crypto large primes are needed, so they are generated randomly and the we check if they are prime
    - traditionally the trial division is used where the randomly generated number is divided by a range of number starting from 2 to p-1 and checking if the result is 0. if the result is 0 the number is not a prime number. but this is hard to do for large number.
    - we can use GCD to solve the problem. If we generate a random number p and what to check it's primality, we again randomly generate a number r which is less then p and find it's GCD. If the GCD is greater then 1, the number p and r has a common factor thus the number p is not prime.
    - if the GCD is 1 p and r are relatively prime which DOESN'T mean p is prime
    - if we take r2 and do the same and got the GCD equal 1 p is still a relative prime of r and r2.
    - if we repeat the process 100000 times with 100000 different r then there is a high probability that p is prime
    - Jacobi function can also test primality of a number
    - this are ways to find a prime in a statistical method 
- How RSA works
    - generate two large (100 digit = 512 bits) prime number p and q
    - calculate the product of p and q which is equal n and nearly 200 digit 
        - if we can retrive p and q from n, then RSA will be broken which still has no happaned
    - select a large integer e that is a relative prime of p-1 and q-1
    - then select d which satisfies this equation: e*d mod (p-1)*(q-1) = 1
    - encryption, C = P^e mod n
    - decryption, P = C^d mod n
    - this means e is public key and d is the private key


Source
------

