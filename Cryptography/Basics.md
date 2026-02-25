While networking protocols have made it possible for devices spread across the globe to communicate, cryptography has made it possible to trust this communication.

Cryptography's ultimate purpose is to ensure secure communication in the presence of adversaries.

Term secure includes confidentiality and integrity of the communicated data.

It's the study practice and study of techniques for secure communication and data protection where we expect the presence of adversaries and third parties.

Plaintext - readable data. It's passed through the encryption function along with a proper key, the encryption function returns a cipher text.

The encryption function is part of the cipher; a cipher is an algorithm to convert a plaintext into a cyphertext and vice versa.


![[Pasted image 20260218003505.png]]


To recover the plaintext, we must pass the ciphertext along with the proper key via the decryption function, which would give us the original plaintext.

![[Pasted image 20260218003643.png]]

Key is a string of bits the cipher uses to encrypt and decrypt data. In general, the used cipher is public knowledge but the key must remain secret unless it is the public asymmetric encryption.

Encryption is the process of converting plaintext into ciphertext using a cipher and a key.

Decryption is the reverse process of encryption, converting ciphertext back into plaintext using a cipher and a key.


### Types of Encryption

Symmetric Encryption/Symmetric Cryptography/secret key/shared-key cryptography

It uses the same key to encrypt and decrypt the data. Keeping the key secret is a must. It is called private key cryptography.

Communicating the key to the intended parties can b.e challenging as it requires  a secure communication channel.


**Examples of Symmetric Encryption**

- Data Encryption Standard - uses a 56-bit key
- 3DES which is DES applied 3 times - The key is 168 bits.
- AES - uses 128, 192 or 256

**Asymmetric Encryption**

It uses  a pair of keys, one to encrypt and the other to decrypt. It encrypts the data using the public key, hence it is also called public key cryptography.

![[Pasted image 20260218010043.png]]

Examples of RSA, Diffie-Hellman and Elliptic Curve Cryptography. Two keys involved in the process are referred to as public key and private key.

They use large keys than symmetric encryption. RSA uses 2048-bit, 3072-bit and 4096-bit keys. 2048-bit is the recommended minimum key size.

ECC can achieve equivalent security with shorter keys.

Asymmetric encryption is based on a particular group of mathematical problems that are easy to compute in one direction but extremely difficult to reverse.