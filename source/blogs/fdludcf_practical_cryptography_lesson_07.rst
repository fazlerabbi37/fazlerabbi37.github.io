fDLuDCf's Practical Cryptography: Lesson 07
===========================================
`< Blog <../blog.html>`_

fDLuDCf's Practical Cryptography DLC: Public Key Distribution 

Created on: 2020-03-06

Tag: `cryptography <blogs/tag_cryptography.html>`_

.. warning:: This is my class-note for `fDLuDCf's Practical Cryptography DLC <https://dle.asiaconnect.bdren.net.bd/upcoming_event/practical-cryptography>`_. I typed out what I thought to be importent and note worthy from the lecture and the slides. This is by no means guilde or complete reference for the course.

.. warning:: this note has numeras spelling mistakes and not yet fixed.


Class Slides
------------
The slides for Lesson 07 is available `here <https://dle.asiaconnect.bdren.net.bd/DLE-3/L7(KeyDistribution).pdf>`_.


Class Video
-----------
The video for all lessons are available in the `video page <https://dle.asiaconnect.bdren.net.bd/dle-course-3-practical-cryptography/>`_


Notes
-----
- previous class review
    - asymmetric key crypto
    - comring to symmetric asymmetric is more secure
    - but it is slower then symmetric
    - DH review
- hybrid encryption
    - a mix of symmetric and asymmetric key
    - practical use case
- storing and handling public keys
    - for user A and B the private key stays at the local machine
    - the public key is stored in a key server
    - A pulls B's public key and encrypt a session key with the public key and sends it to B. this key will be used for communcation in between them
    - problem is B has no idea as to who's key is it. Anyone can intercept and send their session key to B as his public key is accessable and say that he is A. so no authentcity.
    - the sloution is signine the session key. A will sign the session key with his private key and sent it to B.
    - B then can verify the session key is signed with A's key by pulling A's public key and running sign verification againes it
    - but this way we compromize confedentiality. for the first one we lose autenticity and for this one we lose confendentiality but we need both and both can be acived with double encryption
    - first A encrypts (signs!?) the session key with A's private key and then encrypt it using B's public key. so only B can decrypt the outer layer of encryption with his private key only then he would be able to veryfy the session key's signature with A's public key
- the distribution system
    - the key server that holds the public key needs to secure so that we can ensure that A's public key has not been replaced by someone malicious
    - we slove it using Certificate Authority or CA
    - CA legetamise the public key by digitally signing the keys of the users with their private key thus anyone having the public key of the CA can verify if the user key is vaild or not
- CA
    - A org that everyone trusts
    - binds the user's public key
    - A user or entity can register with a public key with the CA
    - then the user provides proof of identity to the CA
    - if the identity is verifed then the CA binds the user's public key by digitally signing it with their private key and provides a certificate
    - the certificate contains A's public key and the CA's private key
- Why CA?
    - certificate allows public key exchange without having to accees to public key
    - certificate also contains info like: expire date, issuer's info and cryptography details
    - the CA must have to sign very thing and everyone must trust the CA
    - the certificate can be verified by all who knows the public key of the CA
    - CA must ensure the identity of the certificate owner
    - BIG QUESTION: who ensure the vlidity of CA???
- structure of a certificate
    - Version
    - Serial Number
    - Signature Algorithm
    - Issuer: CA
    - Subject: not clear
    - Validity: expires on
    - Subject Public Key Information
    - Extensions
    - Signature: signature for this data
- issuer info:
    - Country Name
    - State and Province Name
    - Locality Name
    - Organization Name
    - Organization Unit Name
    - Common Name: domain for website and Full name for humans
    - Email Address
    - URL
- certificate type:
    - Digital Signature: sign your public key
    - Key Encipherment: for website
    - Data Encipherment: email
    - Key Certificate Signature: certify some CA's public key
    - CRL Signature
    - Object Signing: software like object
    - the first 3 are for general usages the leter ones are for CA like org
- Exchangeing key's with CA
    - now we have a CA certified public key so if A want's B's public key it get's B's certificate
    - then verifies it with CA's public key
    - so how we distribute CA signed public key
        - what if certificate is expired
        - how this is used in practical life
- How to verify the authinticity of the CA's public key
    - normally the self-certify it
    - or use some other CA to certify the public key. the other CA is called the root certificate authority and provides a root certificate. if check our browser this root cerificates are the authority certificates
    - if anyone changes the root certificate and replaces with their bogus own the site checks the signature of the certificates the as the mismatch it rejects the bogus certificate
- Certificate Hierarchy
    - as one CA must sign the public key of another CA [see slide 25 for the picture]
    - helps us to verify a user public key
- CA Hierarchy in practice
    - the root CA is embaded/ hard code within the software so that the hierarchy can be verified
- Trust Hierarchy
    - used by PGP
    - A want to send something to B but don't know B. But knows C
    - C knows D and D knows B thus A trusts that B can be trusted
    - close to real life trust mode
    - no CA
    - web of trust
- Cross Certification 
    - user builds the trust hierarchy
    - the CAs verify each other thus cross
    - both CAs have two root certificate one self-signed with their own and another from the other CA
    - [see slide 28 for picture]
- certificate revocation
    - if someone has lost the private key or wants to cancle a cert
    - generate by CA
    - it is managed with certificate recovation list(CRL) a form of anti-certificate the cancles certificate and distrubutes
    - relaying parties checks CRL before using a ceritfiate
- using CRL
    - if anyone want to revoke a cert, the contact CA and CA puts the serial number in the CRL
    - has a fix validity period or expire data
    - at expire every one contacts the CA and get new CRL
    - CRL url is added in the certificate
    - but how fast is fast enough to know if a cert has been revocked? not fast enough so OCSP
    - [see slide 30 for more explanation] 
- Online Certificate Status Protocol (OCSP)
    - OCSP are servars that tell us the validity of a cert
    - status value have no application [status values: good, revocked, unkowwn]
    - not revocked don't necsserally mean good
    - unknown could be anyting form cert never issue to maybe issued but can't find a CRL to verify
- OCSP problems
    - may caches status so already expired key can have 'good' status
    - CRL can only give revocked status not what the cert is
    - some OCSP would give good status for a cert whos CRL is not found
    - much debated
    - other protocols are being build [see slide 34]
- Automatic Certificate Management Environment (ACME)
    - solves the identity problem by trying to validate if the applicent ligitematelly represents the domain
    - automates the process of verification and cert issue
- Cert generation demo


Source
------

