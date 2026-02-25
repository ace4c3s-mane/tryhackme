
```bash
root@TryHackMe# ssh 10.10.244.173
The authenticity of host '10.10.244.173 (10.10.244.173)' can't be established.
ED25519 key fingerprint is SHA256:lLzhZc7YzRBDchm02qTX0qsLqeeiTCJg5ipOT0E/YM8.
This key is not known by any other name.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.10.244.173' (ED25519) to the list o
```


ED25519 is a public-key algorithm used for digital signature generation and verification.

Our SSH client didn't recognise this key and is asking me to confirm whether I want to continue with the connection. This warning is because  a man-in-the-middle attack is probable; a malicious server might have intercepted the connection and replied, pretending to be the target server.

In this case, the user must authenticate the server, i.e confirm the server's identity by checking the public key signature. Once you answer with "yes" the SSH client will record this public key signature for this host. In the future, it will connect me silently unless this host replies with a different public key.

Now that we have confirmed that we are talking with the correct server, we need to identify ourselves and get authenticated. In many cases, SSH users are authenticated using usernames and passwords like you would log into a physical machine. However, considering the inherent issues with passwords, this does not fall within the best security practices.

At one point we'll find SSH configured with key authentication. This authentication uses public and private keys to prove the client is a valid and authorised user on the server. By default, SSH keys are RSA keys.

You can choose with algorithm to generate and add a paraphrase to encrypt the SSH key.

ssh-keygen is the program usually used to generate key pairs. It supports various algorithms:

- DSA (Digital Signature Algorithm) - a public-key cryptography algorithm specifically designed for digital signatures.
- ECDSA (Elliptic Curve Digital Signature Algorithm) - A variant of dSA that uses elliptic curve cryptography to provide smaller key sizes for equivalent security.
- **ECDSA-SK (ECDSA with Security Key)** is an extension of ECDSA. It incorporates hardware-based security keys for enhanced private key protection.
- **Ed25519** is a public-key signature system using EdDSA (Edwards-curve Digital Signature Algorithm) with Curve25519.
- **Ed25519-SK (Ed25519 with Security Key)** is a variant of Ed25519. Similar to ECDSA-SK, it uses a hardware-based security key for improved private key protection.

The paraphrase used to decrypt the private key doesn't identify you to the server at all. It only decrypts the SSH private key. The paraphrase is never transmitted and never leaves your system.


Using tools like John the Ripper, you can attack an encrypted SSH key to attempt to find the passphrase, highlighting the importance of using a complex passphrase and keeping your private key private.

When generating an SSH key to log in to a remote machine, you should generate the keys on your machine and then copy the public key over, as this means the private key never exists on the target machine using ssh-copy-id. This doesn't matter in CTF boxes.

Permissions must be set-up correctly to use a private SSH key. Otherwise, your SSH client will ignore the file with a warming. Only the owner should be able to read and write to the private key (600 or stricter)

`ssh -i privateKeyFileName user@host` is how you specify a key for the standard Linux OpenSSH client.