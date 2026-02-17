At one point, you would only need a packet-capturing tool to read all the chats and passwords of the users on your network.

It was not uncommon for an attacker to set their network card in promiscuous mode, capture all packets including those not destined to it.

They would then go through all the packet captures and obtain the login credentials of unsuspecting victim.

Secure Sockets Layer was developed by Netscape Communications in early 1990s.

Internet Engineering Task Force (IETF) developed Transport Layer security which was an upgrade of SSL.

Like SSL, TLS is a cryptographic protocol operating at the OSI model's transport layer. It allows secure communication between a client and a server over an insecure network.

It ensure no one can read or modify the exchanged data.

The first step for every server (or client) that needs to identify itself is to get a signed TLS certificate.

Generally, the server administrator creates a Certificate Signing Request (CSR) and submits it to a Certificate Authority. The CA verifies the CSR and issues a digital certificate. Once the signed certificate is received, it can be used to identify the server (or the client) to others who can confirm the validity of the signature.


For a host to confirm the validity of a signed certificate, the certificates of the signing authorities need to be installed on the host.

Generally speaking, getting a certificate signed requires paying an annual fee. However, [Let’s Encrypt](https://letsencrypt.org/) allows you to get your certificate signed for free

Some users opt to create a self-signed certificate. A self-signed certificate cannot prove the server’s authenticity as no third party has confirmed it.