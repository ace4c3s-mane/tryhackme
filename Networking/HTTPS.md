
HTTP relies on TCP and uses port 80 by default.

Steps taken before a browser can request a page over HTTP. 

After resolving the domain name to an IP address, the client will carry out the following steps:

- Establish a TCP three-way handshake with the target server.
- Communicate using the HTTP protocol; for example, issue HTTP requests such as GET / HTTP/1.1


HTTPS is basically HTTP over TLS. Requesting a page over HTTPs will require the following 3 steps (after resolving the domain name):

- Establish a TCP 3-way handshake with the target server.
- Establish a TLS session
- Communication using the HTTP protocol.

Adding TLS to HTTP leads to all the packets being encryped. We can no longer see the contents of the exchanged packets unless we get access to the private key.

The insecure versions use the default TCP port numbers shown in the table below:

|Protocol|Default Port Number|
|---|---|
|HTTP|80|
|SMTP|25|
|POP3|110|
|IMAP|143|

The secure versions, i.e., over TLS, use the following TCP port numbers by default:

|Protocol|Default Port Number|
|---|---|
|HTTPS|443|
|SMTPS|465 and 587|
|POP3S|995|
|IMAPS|993|

TLS can be added to many other protocols; the reasoning and advantages would be similar.

