fDLuDCf's Practical Cryptography: Lesson 02
===========================================
`< Blog <../blog.html>`_

fDLuDCf's Practical Cryptography DLC: Hash and Message Authentication Code

Created on: 2020-02-03

.. warning:: This is my class-note for `fDLuDCf's Practical Cryptography DLC <https://dle.asiaconnect.bdren.net.bd/upcoming_event/practical-cryptography>`_. I typed out what I thought to be importent and note worthy from the lecture and the slides. This is by no means guilde or complete reference for the course.

.. warning:: this note has numeras spelling mistakes and not yet fixed.


Class Slides
------------
The slides for Lesson 01 is available `here <https://dle.asiaconnect.bdren.net.bd/DLE-3/L2(MAC).pdf>`_.


Class Video
-----------
The video for all lessons are available in the `video page <https://dle.asiaconnect.bdren.net.bd/dle-course-3-practical-cryptography/>`_


Notes
-----
- Hash and Message Auth Code. Objecttive is to provide data intrigity through hash.
- Hash functions:
    - condences arbitery messages to fixed size aka fingerprinting 
    - normally hash function is public and no key is used
    - detect change in message 
    - password verification, digital signature
- hash function tryies to match infnite message space to a finite hash space when two message have same hash we get a hash colission. generally the hash domain is made large enough so that attacker can't find the collision with limited resources.
- hash functions are one way, meaning you should get the same hash for same message but you should never be able to get the message from hash.
- XOR/vernam cipher is a simple has algo but not a very good one.
- Reuiremens for hash algo:
    - can take any size of message/data/plain-text
    - produce to a fix leghth output
    - easy to compute the hash function
    - one way funtion so given the hash one should not be able to find the the message.
    - weak collision resistant so two diffreent message should not produce same hash
    - strong collision resistant so two diffreent hash should not produce same message
- MD5 (message-digest algorithm 5)
    - designed by Ronald Rivest
    - latest of MD2, MD4
    - produces 128 bit hash 
    - most used until recentelly
    - number of steps: 80 (4 rounds of 20)
- How MD5 works:
    1. takes a chunk of 512 bit data so the full data length should be a multipule of 512 bit, if not add padding to make a multipule
    2. the take the first 512 bit chunk and feed it to the hash function with a 128 bit vector/seed
    3. the output would be a 128 bit value
    4. use the 128 bit value from previous step and the next 512 bit check and feed it to the hashing alog and continue
    5. the operation on final check will also output a 128 bit value which is the hash aka the fingerprint.
- MD5 collision:
    - https://www.mscs.dal.ca/~selinger/md5collision/
    - more at slide
- SHA-1
    - works same as MD5 only diff is that seed and output is 160 bit
    - number of steps: 64 (4 rounds of 16)
- Basic/reudementery password verificaiton protocol (without hash, plain-text!?):
    - user name and pass is saved to server in file or data 
    - user gives password
    - server matches stored one and the given one and allow access if matches
    - this is a problem as anyone with access to server can see the password
    - encrypting the password is not a good idea either as the server need to know the decryption key and the previous problem persisit
    - soulution? here comes HASH!!!
- Hash based password verification:
    - the user gives password, the server calculates the hash of the given password
    - if the hash match with the saved hash allow access
    - as hash is a one way function, even if someone get's the hash they will never get the password in plain text
    - but it still has some problem like:
        - if two users are using same password there hash would be same so knwoing one user pass would compromise the other user. 
        - prone to dictionary attack
    - to solve dictionary attack problem we use salt
- Salt
    - save salt in the table for each user
    - use the salt and password to calculate the hash
    - recommanded salt length is 64 bit
    - attack is still possible using rainbow table
- Authenticate the evidence
    - proves the nobody has tempered with the evidence. ei. a video by person A is not modified by someone before presenting it to the court.
- Hash reverse lookup
    - searches the pre-calculated hash value
    - http://reverse-hash-lookup.online-domain-tools.com/
- Linux tools for calculating hash
    - MD5: md5sum
    - SHA-1: sha1sum
- md5sum has -c flag that checks hash againest a file
- Message Auth Code:
    - checks the intrigrity of message
- How Message Auth Code works:
    - takes a variable length message and key 
    - outputs fix length MAC
    - appends the MAC with the original messahe
    - transmite to the reciver
    - reciver performs the same operation so must know the key used by sender
    - comapres the MAC
    - as attacker doesn't know the key any modification to message will change the MAC
- HMAC:
    - hash based MAC
    - used beacuse: they are fast, not limited by export controls like block cipher and already includes a key with message
    - usages a hashing function
    - input in key and message
    - many to one function, so many message may have same MAC but finding this needs to be difficult
- HMAC Design Criteria [see slide 29]
- HMAC attack:
    - brute force attack
    - birthday attack 
- Birthday Paradox:
    - how many people on a same room has same birthday?
    - given we have n people, in 2^n/2 people there is 50% change that 2 people would have same birthday
- Birthday attack on HMAC:
    - collects many message and hash pair 
    - for 128 bit block it will take 2^64 setps to perferm a birthday attack (find collision, not specifici value)
- Java Cryptography Architecture (JCA):
    - it is a provider class
    - it provides crypto and hasing functions as engines
- Message Digest with JCA:
    - Message Digest Class
    - Message Digest Stream Class
- using Message Digest Class:
    - get the diest algo using getInstance() method
    - feed binary data using update() method
    - calculate digest using digest() method
    - to verify pervious step are performed at reciver end and use an isEqual() method to compare

Source
------

