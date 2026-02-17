You've received an email and want to download it to your local machine. The Post Office Protocol Version 3 (POP3) is designed to allow the client to communicate with a mail server and retrieve email messages.

An email client sends its message by relying on SMTP and retrieves them using POP3.  SMTP is similar to handling your envelope or package to the post office and POP3 is similar to checking your local mailbox for new letters or packages.

![[Pasted image 20260212002917.png]]

Some common POP3 commands are:

USER <username> identifies the user
PASS <password> provides the user's password.
STAT requests the number of messages and total size.
LIST lists all the messages and their sizes.
RETR <message_number> retrieves the specified message.
DELE <message_number> marks a message for deletion.
QUIT ends the POP3 session applying changes, such as deletions.


POP3S Listens on port 110.

Dovecot is mostly used as a POP3 server. It enforces SSL/TLS to prevent credential sniffing.

TLS has to be enforced before credentials are sent.

Sniffing credentials over the network won't work.

POP3 allows secure connection via port 995. 

openssl s_client -connect <ip>:995 or openssl s_client -connect 10.48.189.7:110 -starttls pop3


This negotiates for an SSL/TLS session.


