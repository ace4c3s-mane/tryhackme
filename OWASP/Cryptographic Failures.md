
They happen when encryption is used incorrectly or not at all. This includes weak algorithms, hard-code keys, poor key handling or unencrypted sensitive data. 

#### Why It matters

Web apps rely in cryptography everywhere, protecting network traffic, securing stored data,  verifying identities and safeguarding secrets.

When these controls fail, sensitive data such as passwords, tokens or personal information can be exposed, leading to account takeovers or full-scale breaches.

Attackers can exploit these flaws through man-in-the-middle attacks, brute-force attacks on weak keys or simply discovering secrets that were never properly protected.


**Common Patterns** 

- Using deprecated or weak algorithms like MD5, SHA-1, or ECB mode
- Hard-coded secrets in code or configuration
- Poor key rotation or management practices
- Lack of encryption for sensitive data at rest or in transit
- Self-signed or invalid TLS certificates
- Using AI/ML systems without proper secret handling for model parameters or sensitive inputs

**How To Prevent It**
- Use strong, modern algorithms such as AES-GCM, ChaCha20-Poly1305, or enforce TLS 1.3 with valid certificates
- Use secure key management services like Azure Key Vault, AWS KMS, or HashiCorp Vault
- Rotate secrets and keys regularly, following defined crypto periods
- Document and enforce policies and standard operating procedures for key lifecycle management
- Maintain a complete inventory of certificates, keys, and their owners
- Ensure AI models and automation agents never expose unencrypted secrets or sensitive data
- The web application in this room contains a weakness of this type for you to explore.


#### Solving the Cryptographic Challenge on THM

Navigated to the site:

![[Pasted image 20260311020559.png]]


Viewed the source and came across this:

![[Pasted image 20260311020638.png]]


Interesting part was: 

```javascript
 // Configuration
    const SECRET_KEY = "my-secret-key-16";
    const ENCRYPTION_MODE = "ECB";
    const KEY_SIZE = 128;
```

The secret key was encrypted in AES, ECP

ECB (Electronic Codebook Mode) - It's one of the simplest ways to use a block cipher like AES.

### Block Cipher 

Algorithms like AES do not encrypt a whole file at once.
They break data into fixed-size blocks (For AES this is 16 bytes)

Example

```html
HELLO_THIS_IS_A_SECRET_MESSAGE
```

It gets split into blocks like:

```html
Block1 | Block2 | Block3 | Block4
```

Each block is 16 bytes


### How it works

In ECB mode, each block is encrypted independently using the same key.

Formula 

```html
Ciphertex = Encrypt(key, PlainBlock)
```

So the process looks like this:

```html
Plaintext Block 1  ──► Encrypt(Key) ──► Cipher Block 1
Plaintext Block 2  ──► Encrypt(Key) ──► Cipher Block 2
Plaintext Block 3  ──► Encrypt(Key) ──► Cipher Block 3
```

## Why ECB is Weak

If two plaintext blocks are **identical**, the encrypted blocks will also be **identical**.

```html
Plaintext:
AAAAAAAABBBBBBBBAAAAAAAA

Blocks:
A | B | A
```


#### Encrypted

```html
Enc(A) | Enc(B) | Enc(A)
```


The string was encoded in base64 so I, decoded it.

```javascript
echo "Nzd42HZGgUIUlpILZRv0jeIXp1WtCErwR+j/w/lnKbmug31opX0BWy+pwK92rkhjwdf94mgHfLtF26X6B3pe2fhHXzIGnnvVruH7683KwvzZ6+QKybFWaedAEtknYkhe" | base64 -d > encrypted.bin
```


```Javascript
erald@kali:~ $ cat encrypted.bin 
77x�vF�B��
          e���UJ�G����g)���}h�}[/���v�Hc����h|�Eۥ�z^��G_2�{ծ����������
ɱVi�@�'bH^ 
```

To decrypt this, I needed my key in hex, so I had to convert it.

```bash
 echo -n "my-secret-key-16" | xxd -p
6d792d7365637265742d6b65792d3136
```

Decryption

```bash
openssl enc -aes-128-ecb -d -in encrypted.bin -out decrypted.txt -K 6d792d7365637265742d6b65792d3136
```

```bash
cat decrypted.txt                   
CONFIDENTIAL: The admin password is 'admin123'. Flag: THM{CRYPTO_FAILURE_H4RDCOD3D_K3Y} 
```

