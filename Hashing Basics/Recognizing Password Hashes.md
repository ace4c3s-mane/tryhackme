
On Linux, password hashes are stored in /etc/shadow, which is normally only readable by root.

The shadow file contains the password information. Each line contains nine fields, separated by colons: The first two fields are login name and encrypted password. More information about the other fields can be found executing man 5 shadow on Linux.

The encrypted password field contains the hashed passphrase with four components: prefix, (algorithm id), options(parameters), salt and hash. it is saved in the format ($prefix$options$salt$hash)

$y$  - yescrypt is a scalable hashing scheme and is the default and recommended choice in new systems.

|Prefix|Algorithm|
|---|---|
|`$y$`|yescrypt is a scalable hashing scheme and is the default and recommended choice in new systems|
|`$gy$`|gost-yescrypt uses the GOST R 34.11-2012 hash function and the yescrypt hashing method|
|`$7$`|scrypt is a password-based key derivation function|
|`$2b$`, `$2y$`, `$2a$`, `$2x$`|bcrypt is a hash based on the Blowfish block cipher originally developed for OpenBSD but supported on a recent version of FreeBSD, NetBSD, Solaris 10 and newer, and several Linux distributions|
|`$6$`|sha512crypt is a hash based on SHA-2 with 512-bit output originally developed for GNU libc and commonly used on (older) Linux systems|
|`$md5`|SunMD5 is a hash based on the MD5 algorithm originally developed for Solaris|
|`$1$`|md5crypt is a hash based on the MD5 algorithm originally developed|


Windows passwords are hashed using NTLM, a variant of MD4. They're visually identical to MD4 and MD5 hashes.

In Windows, password hashes are stored in SAM (Security Accounts Manager)  MS windows tries to prevent normal users from dumping them  but tools like mimikatz exist to circumvent MS windows security. 

Notably, the hashes found there are split into NT hashes and LM hashes.

Yescrypt is a password-based key derivation function (KDF) that uses

**SHA-256** for its underlying cryptographic operations. The resulting hash output (the digest) is **256 bits (32 bytes)**