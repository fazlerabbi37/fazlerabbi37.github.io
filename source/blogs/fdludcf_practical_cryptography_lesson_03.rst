fDLuDCf's Practical Cryptography: Lesson 03
===========================================
`< Blog <../blog.html>`_

fDLuDCf's Practical Cryptography DLC: Symmetric Key Cryptography

Created on: 2020-02-05

Tag: `cryptography <blogs/tag_cryptography.html>`_

.. warning:: This is my class-note for `fDLuDCf's Practical Cryptography DLC <https://dle.asiaconnect.bdren.net.bd/upcoming_event/practical-cryptography>`_. I typed out what I thought to be importent and note worthy from the lecture and the slides. This is by no means guilde or complete reference for the course.

.. warning:: this note has numeras spelling mistakes and not yet fixed.


Class Slides
------------
The slides for Lesson 03 is available `here <https://dle.asiaconnect.bdren.net.bd/DLE-3/L3(Crypto).pdf>`_.


Class Video
-----------
The video for all lessons are available in the `video page <https://dle.asiaconnect.bdren.net.bd/dle-course-3-practical-cryptography/>`_


Notes
-----
- types of cryptography: [more at slide 2 and 3]
- symmetric key cryptography is the system where one key is used for both encryption and decryption
- symmetric key cryptography strength:
    - fast and effecient them asymmetric
    - hard to break with brute force if a large enough key is used
    - ideal for bulk encryption and decryption
- symmetric key cryptography weakness:
    - poor key distrubution as in how the decrytor gets the key in a secure way
    - poor key management and scalablity as in each user pair needs a seperate key if all are same there is no secret
    - can't provide authenticity and non-repudiation only confedentiality
- black cipher:
    - block size: it waroks with blocks of data
    - key size: the larger the key, the larger the confusion and defustion 
    - number of rounds: it runs many internal operation before producing the output
    - encryption modes: how messages larger then block size is encrypted
- Feistel Network:
    - proposed by Feistel in 1973
    - used by several blck cipher like: DES, IDEA, RC5 but not used in AES
- how Feistel Network works:
    - block size n is devided into 2 half: left and right
    - for encryption if we take right, then encryption function is ran on the right half of the data
    - then it is XOR-ed with the left half 
    - the result of the XOR function is now the new right half
    - this goes on till number of round, d 
    - see more at slide 9
- Data Encryption Standerd (DES):
    - adopted in 1977 by NBS/NIST as FIPS PUB 46
    - encrypts 64 bit data with 56 bit key
    - possible to brute force now
- DES features:
    - key size is 56 but becomes 64 with aditional 8 parity bits
    - number of rounds 16
    - same round number (16) of internal key is generated each with 8 bits
- how DES works:
    - after taking input does initial permutation
    - does all the steps of Feistel Network
    - after finishing the work does a inverse initial permutation
- Tripple DES/3DES:
    - takes one plain-text and 3 seperate key
    - assuming the keys are K1,K2 and K3
    - plain-text is encrypted with DES using K1, then that output data is again encrypted with DES using K2, then that output data is again encrypted with DES using K3.
    - The decryption usages key in reverse order K3 -> K2 -> K1
    
- 3DES with 2 Key:
    - same as 3DES but K1 and K3 are same
- 3DES backward compatablity:
    - if K1 and K2 are same we are doing encrypon in first round and then decryption of the same data in second round 
    - thus 3DES becomes DES
- DES to AES
    - DES was breakable in theory
    - 3DES is slow
    - so NIST calls for chipher in 1997
    - 15 candidate accepted in June 1998
    - 5 candidate short listed in Aug 1999
    - Rijandael was slected as AES in Oct 2000
    - issued in Nov 2001 by NBS/NIST as FIPS PUB 197
- Rijandael/AES:
    - block size in duble then DES: 128 bit
    - default key size in 128 bit but can support 192 bit and 256 bit (now recommanded)
    - Faster and stronger the DES
    - active life of 20-30 
- AES shortlist:
    - MARS
    - RC6
    - Rijandael
    - Serpent
    - Twofish
- Cryptographic cycles:
    - encryption which is less like encrypting a disk one time
    - decryption which is more like accessing that encrypted a disk on every boot
- Why Rijandael was choosen for AES?
    - as we can see decryption happens more so the standerd algo needs to be decryption effeicent
    - Rijandael usages seperate encryption and decryption algo and has the fasted decryption among the shortlisted
- How AES works:
    - block size: 128 bit
    - key size: 128/192/256 bit
    - rounds: 10
    - internal key: 10
    - decryption algo uses the internal key in reverse order
    - decryption algo is not same as encryption algo
- How AES works more details:
    - take data in 4x4 matrix
    - take key in 4x4 matrix
    - the do the following 4 transformation for 9 round:
        - sub bites subtutions the text with a S-Box lookup
        - shift row shifts the row by number of row. row count starts from 0
        - mix columns takes each columns and does a dot product with a matrix (where does it come from!?)
        - on add round key we take each column and XOR it with the round keys respective column
    - on the final round the previous process is done with the exception of doing the mix columns
    - We use key scheduler to generate the internal key
        - take the last column
        - we take the first value of the column and put in on bottom to get a new column
        - now substutite the values of new column with S-Box lookup
        - now we XOR the first column of the key, the newly substutied column and the 4th column of Rcon martix (what is the Rcon martix and why the 4th column?)
        - the result becomes the first column of next round
        - for the second to forth column, the approch a bit different and easy. here we take a column of previous key and XOR it with the last derived column of currrent key. for example, to derive second column we take the second column of previous key and XOR it with the first column of current key and so on.
- Padding:
    - what happens when the data size in less then the block size? we use aribterry data to fill up rest of the space which is known as padding.
    - PKCS5 is one of those padding scheam
- Public Key Cryptographic Standerd 5 (PKCS5):
    - assuming the block size is 64 bit any message that is not a multipule of 8 is padded
    - for 7 bit data, we need 1 bit padding: 0x1
    - for 6 bit data, we need 2 bit padding: 0x2 0x2
    - for 5 bit data, we need 3 bit padding: 0x3 0x3 0x3
    - and so on
    - but what would we do for 8 bit data? does it need padding if so how many?
        - 8 bit data also need padding of 8 bit length 0x8 0x8 0x8 0x8 0x8 0x8 0x8 0x8 because if no padding is found and the last bit is 0x1 it would be removed during decryption as the decryption algo would think it to be a 1 bit padding.
- PKCS7 usages the same stretigy but can be allpied for any block size
- Electronic Codebook (ECB)
    - breaks the message into chunk
    - apply a block alog like DES or AES on those checkes with the key
    - outputs the result as cipher text [see slide 30 for illustration]
    - ECB is not recommanded for two reasons: 
        - it takes one byte and changes that to another byte of data thus some of the data is extractable
        - if any byte is courupted that it is useless for us. further more if attacker changes the byte it will decrypt to a diffreect data make it volnurable to incertion attack
- Cipher Block Chaining (CBC)
    - takes an initial vector equal to block size
    - breaks the message into check
    - XOR's the first block with initial vector
    - apply a block alog like DES or AES on the XOR-ed data with the key
    - the output is carried as ciphertext for that block and the same output is used as the initial vector for next block [see slide 34 for illustration]
    - The last block can be used as Massage Auth Code (MAC) as it will condence the entire message to the last cipher block
- Using OpenSSL to enctypt and decrtpt file
    - encryption: openssl enc aes-256-cbc -in orig_photo.jpg -out photo.enc
    - decryption: openssl enc -d aes-256-cbc -in orig_photo.jpg -out photo.enc


Source
------

