fDLuDCf's Practical Cryptography: Lesson 08
===========================================
`< Blog <../blog.html>`_

fDLuDCf's Practical Cryptography DLC: Cryptographic Protocols

Created on: 2020-03-07

Tag: `cryptography <blogs/tag_cryptography.html>`_

.. warning:: This is my class-note for `fDLuDCf's Practical Cryptography DLC <https://dle.asiaconnect.bdren.net.bd/upcoming_event/practical-cryptography>`_. I typed out what I thought to be importent and note worthy from the lecture and the slides. This is by no means guilde or complete reference for the course.

.. warning:: this note has numeras spelling mistakes and not yet fixed.


Class Slides
------------
The slides for Lesson 01 is available `here <https://dle.asiaconnect.bdren.net.bd/DLE-3/L8(Protocols).pdf>`_.


Class Video
-----------
The video for all lessons are available in the `video page <https://dle.asiaconnect.bdren.net.bd/dle-course-3-practical-cryptography/>`_


Notes
-----
- Practical cryptographic protocols [see slide 2 for the list of service]
    - IPSec: protect the comms between two networks, host to host
    - DNSSEC: provide security for DNS system. Confidentiality is not archived, authenticity is.
    - PCT: introduced by Microsoft. in 1990. parallel to SSL. 
    - SSL: introduced by Netscape now Mozilla at the same time as PCT. People agreed to use SSL and dropped PCT
    - TLS: Internet Engineering Task Force (IEFT) took the SSL and standardised internationally. most used protocol. will be discussed more in details
    - SET: historical money transfer protocol
        - now a day's cryptocurrency use cryptography more intensely where mostly hashing and public key crypto
    - Cybercash: also a historical money transfer protocol
    - PGP: email encryption. de facto industry protocol and people use voluntarily  
    - S/MIME: internationally standardised protocol for email 
    - SSH: for remote login. used as both authentication and encryption protocol. based on public key cryptography. server client mode. where they may both have public and private key. If the server has public-private key and client don't then authentication is provided by username and password and session key and encryption is done by public private key,
    - We will only read about TLS and PGP
- Before we start TLS: What is SSL
    - SSL 1.0 is by Netscape in 1994
    - S-HTTP so web only
    - competition with PCT by Microsoft and PCT lost the competition
    - IETF standard it in and created TLS 1.0 in 1999
    - Now most of the web server usages TLS 1.2
- TLS
    - authentication of the web server, encryption of web server and integrity of data
    - authentication of browser is possible but optional
- TLS internal
    - not to confuse with TCP. TLS works in application layer and build on top of TCP layer
    - HTTP, Telnet, FTP and LDAP is also part of application layer and TLS sits between this and TCP layer
- TLS protocol stack [see slide 7 for picture]
    - application protocols like HTTP, Telnet, SMTP, FTP talks to TLS
    - TLS then communicates with TCP layer
    - When HTTP goes via TLS we call it HTTPS (HTTP Secure), when it talks to TCP layer directly it is just HTTP so are other protocols
- TLS on action:
    - Establishing a session
        - agrees on algorithm 
        - shares secret
        - perform authentication
    - Transferring application data
        - data encryption
        - data integrity
- TLS: task on server
    - server generates a key pair and stores the private key in a secure storage ie. Hardware Security Modules(HSM)
    - public key is published as digital certificates
- TLS: browser to server
    - supported browser looks for the URL and if it is ``https://`` then executes the next steps as TLS task
    - browser sends TLS hello message where it proposes a crypto algorithm. like hey google I would like AES for encryption, RSA for signing or Diffie-Hellman key. browser does it use a tool named cipher suites 
    - the server is configure to respond to those cipher suites and responds to the strongest algorithm the browser supports
    - when the algorithm is agreed upon the server exchanges the cert and browser verifies the authenticity of cert by verifying signature of cert with the embedded cert and accepts the cert
    - usually the domain name is included as common name in the cert and the browser checks if the common name is same as the domain name it is trying to connect
    - when the previous step succeeds the browser starts a key exchange. two type of key exchange is used
        - Diffie-Hellman: first gen TLS used it
        - RSA: new gen TLS usages this as DH algorithm in venerable to MiTM
        - recent recommendation is to use the both together
    - now that the browser and server has established a shared secret thus a secure tunnel it starts data exchange and all key are derived from the shared secret
- TLS: basic key exchange 
    - the browser generates a random number R
    - it encrypts the number R with the public key of server and the output is C
    - C gets sent to server where the server decrypts C with it's private key and gets R
    - now both browser and server has the R, a shared secret and now all key can be derived from it
- TLS: forward secrecy
    - forward secrecy is the concept that ensure that an encrypted piece of data will stay encrypted in the future
    - the traditional TLS with key exchange don't have forward secrecy
    - the C [from previous section] can be captured and try to decrypt it. once they do the will be able to compromise the server thus can get all the R of all client
    - RSA, for this reason is not forward secrecy proof but DH is.
    - As DH only exchanges each others public key and destroys the private key after the key exchange so it is impossible to get a private key of either the server or the browser
    - but DH can be attacked with MiTM. this problem is solved with RSA signed public key.
- TLS: data encryption
    - algorithm that can be used: DES, 3DES, AES, RC2, RC4, IDEA
    - it encrypts the following comms:
        - all browser-server and server-browser except which browser is talking to which server (I think DOH does it??)
        - URL of requested document
        - contents of requested document
        - contents of submitted form
        - cookies from browser to server
        - cookies from server to browser
        - contents of HTTP header
        - JS comms
        - etc
- TLS: data integrity
    - archived with message authentication code(MAC)
    - includes hash, shared secret and sequence
    - MAC is transmitted with the data
- TLS: authentication
    - partial support with challenge-response system
    - during the cert exchange with the server [TLS: browser to server section] accepting the server cert don't provide authenticity but only the identity of the web server. 
    - as anyone can send the public key aka cert if the browser wants to authenticate if the server is the one holding the private key for this particular public key, the browser challenges the server.
    - the challenge goes like this: the browser generates a random number, encrypts the number with the public key and sens it to the server asking to decrypt it with it's private key. If the server is the owner of the public key, it responds with the decrypted random number. the browser verifies the decrypted random number and authenticates. 
- TLS: Architecture
    - handshake protocol: establishes the session
    - change cipher protocol: changes cipher when needed
    - alert protocol: sends error 
    - TLS record protocol: used in confidentiality and integrity
- TLS record protocol:
    - application data is broken down in to chunks of data knows as Record Protocol Units and the security is applied to this chunks of data. The important distinction to remember is that TLS is not applied to the whole data but to the chunks of data
    - each chunk is compressed and then the MAC of that compassed data is calculated 
    - then we put the hash and the data together and encrypt it with the session key we established
    - finally the encrypted data is passed to the TCP layer, which then passes it to the IP layer
    - the whole process goes from down to up on the receiving end
    - the compression is done to save bandwidth and compute power thus saves time
    - if the compression was done after the encryption we wouldn't gain better compression 
- Demo with Let's Encrypt
- Email security
    - PGP
    - S-MIME
- PGP: popularity
    - available free on verity of platform
    - no need for cert, anyone can use it
- PGP: process
    - first take the message
    - calculate the hash on the message and encrypt the hash of the message using the public key of the sender aka creates a digital cert 
    - then the time stamp is added as a parameter and it becomes the signature of the massage. this step provides integrity, authenticity, non-repudiation
    - now we compress the message and the session key with it. then encrypt the compressed data with the session key with the recipients public key. this step provides the confidentiality
    - finally we encode as ``base64`` as email is a hex based system.
    - when the recipient receives the message, he/she decrypt the header with his/her private key then gets the session key and the encrypted message
    - using the session key the message is decrypted
    - once decrypted user gets the signature and text. user now can verify the signature by calculating the hash of the message and matches it with the one that he received.
    - the protocol is based on web of trust and no central authority is defined
- S-MIME
    - extension of MIME standard
    - usages PKCS7 to create signed data [see slide 33 for the structure]
    - can also encrypt data with analog data structure [see slide 34 for the structure]
    - we first sign the data then encrypt the data
    - the data is encoded into our email body
    - you MUST need a standard public key cert for a CA
- PGP demo with Mailvelope 


Source
------

