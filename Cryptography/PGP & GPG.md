
PGP stands for Pretty Good Privacy. It's a software that implements encryption for encrypting files, performing digital signing and more.

GnuPG or GPG is an open-source implementation of the OpenPGP standard.

GPG is commonly used in email to protect the confidentiality of email messages. It can also be used to sign an email message and confirm it's integrity.

After generating the gpg key, you can share the public key with your contacts. Whenever your contacts want to communicate securely, they encrypt their messages to your using the public key. To decrypt the message, you will  have to use your private key. Due to the importance of the GPG keys, it is vital that you keep a backup copy in a secure location.

Let’s say you got a new computer. All you need to do is import your key, and you can start decrypting your received messages again:

- You would use `gpg --import backup.key` to import your key from backup.key
- To decrypt your messages, you need to issue `gpg --decrypt confidential_message.gpg`


To use gpg, first import the private key into the gpg keyring.

```python
gpg --import tryhackme.key
```

then:

```python
gpg --decrypt message.gpg
```


- **Cryptography** is the science of securing communication and data using codes and ciphers.
- **Cryptanalysis** is the study of methods to break or bypass cryptographic security systems without knowing the key.
- **Brute-Force Attack** is an attack method that involves trying every possible key or password to decrypt a message.
- **Dictionary Attack** is an attack method where the attacker tries dictionary words or combinations of them.