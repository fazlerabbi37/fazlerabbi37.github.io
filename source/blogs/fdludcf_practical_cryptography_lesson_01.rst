fDLuDCf's Practical Cryptography: Lesson 01
===========================================
`< Blog <../blog.html>`_

fDLuDCf's Practical Cryptography DLC: Introduction to Cryptography

Created on: 2020-02-03

Tag: `cryptography <blogs/tag_cryptography.html>`_

.. warning:: This is my class-note for `fDLuDCf's Practical Cryptography DLC <https://dle.asiaconnect.bdren.net.bd/upcoming_event/practical-cryptography>`_. I typed out what I thought to be importent and note worthy from the lecture and the slides. This is by no means guilde or complete reference for the course.

.. warning:: this note has numeras spelling mistakes and not yet fixed.


Class Slides
------------
The slides for Lesson 01 is available `here <https://dle.asiaconnect.bdren.net.bd/DLE-3/L1(IntroCrypto).pdf>`_.


Class Video
-----------
The video for all lessons are available in the `video page <https://dle.asiaconnect.bdren.net.bd/dle-course-3-practical-cryptography/>`_


Notes
-----
- cryptography: the art or science of secret writing, hiding plain-text
- cryptanalysis: the art or science of retrieving plain-text from code without secret or key
- cryptology = cryptography + cryptanalysis
- objective is to know the principal, means and methods of distinguishing information to ensure it's integrity, confidentiality, authenticity and non-repudiation.
- type of crypto
    - symmetric (single key)
    - asymmetric (public key)
    - hybrid (used multiple)
- plain-text -> encipher -> cipher text -> decipher -> plain-text
- encryption/encipher: process of converting plain-text to cipher text with key
- decryption/decipher: process of converting cipher text to plain-text with appropriate key
- why crypto?
    - protect stored data
    - protect data in trisection
- plain-text: intelligible data
- Kerchoff's principal (19th century): a cryptiosystem should be secure even if everything about the system except the key is public knowledge as opposite of security through obscurity.
- cryptography in business:
    - detect 
    
- goal of cryptography
    - integrity
    - confidentiality
    - authenticity
    - non-repudiation
- history of cryoto: Egyptian scribe (Hieroglyphs), Caesar cipher, Kama Sutra, one-time pad and xor, enigma, public key (Diffie Hellman), piratical PKC like RSA, Rijndael as AES
- monoalphabetic cipher works by simpally substuting one latter for another like Caesar cipher, Kama Sutra.
- monoalphabetic cipher are volunrable to frequency analisys attack
- to solve the frequency analisys attack polyalphabetic cipher came where same latter may can be substutied by diffreent latter. for example depending on the even and odd possition of latter we can use two substitution table. 
- one time pad/ vernam cipher is a stream cipher that takes same ammount of key and plain-text, then performs a XOR function. 
    - key is used once thus the name one time pad and the key is a set of random non repeting characters.
    - each key and plain-text is added and after a module of 26 for english is taken and then converted to a latter.
    - not pratcical for large ammount of data.
    - unbreakale by bruteforce
- random numbers
    - true: book, cd, videos
    - pseudo: linear congruential random number generator which has some fix values that are called seeds.
        - sometime repeats 
        - attack possible 
- columnar transposition cipher (https://www.geeksforgeeks.org/columnar-transposition-cipher/). block cipher
- enchipher mode:
    - stream cipher
    - block cipher
- stream cipher advantages are:
    - speed of transformation is fast, as it is done one at a time
    - low error propegaion, as it will only affect the errored char
- stream cipher advantages are:
    - low diffusion
    - possible to incert mailcious data or modify as it is very easy to identify
- block cipher advantages are:
    - high diffusion
    - not possible to incert mailcious data or modify as the entire block gets courrupted
- block cipher advantages are:
    - speed of transformation is slow, as it has to wait for a block to finish
    - high error propegaion, as it will affect the entire block 
- stream cipher are used in real time comms
- block cipher are used in financial tansection
- Shannon characteristics/ characteristics of good cipher [see slide page 29]
- Kerchoff's principal [see slide page 30]
- confusion: attacker must not be able to predicte the change in cipher text caused by change in plain-text. we can achive it by defusion where a block cipher is used and plain-text is distributed all over the cipher text
- reduncency helps in confusing the attacker
- brute forece attack. now recommanded to use key size larger the 156.
- uncindutuinal security is secure given unlimited resouces
- computationally security is secure given limited resouces



Source
------

