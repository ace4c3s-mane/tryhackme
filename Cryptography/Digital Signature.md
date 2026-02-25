Digital signatures provide a way to verify the authenticity and integrity of a digital message or document. Proving the authenticity of files means we know who created or modified them. 

Using asymmetric cryptographic, you produce a signature with your private key, which can be verified using your public key. Only you should have access to your private key, which proves you signed the file.

The simplest form of digital signature is encrypting the document with your private key. If someone wants to verify this signature, they would decrypt it with your public key and check if the files match. 

![[Pasted image 20260225030357.png]]

Some articles use terms such as electronic signature and digital signature interchangeably. 

They refer to pasting an image of a signature on top of a document. This approach does not prove the document’s integrity, as anyone can copy and paste an image.

Digital signature refers to signing a document using a private key or a certificate.

Certificates are trusted only when the Root CAs say they trust the organisation that signed them.

It's a chain. For example, the certificate is signed by an organization, the organization is trusted by CA and the CA is trusted by your browser. Therefore your browser trusts the certificate.