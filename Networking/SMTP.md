As with browsing the web and downloading files, sending emails needs it's own protocol. Simple Mail Transfer Protocol defines how a client talks with a mail server and how a mail server talks with another.

The analogy is when yo go to the local post office to send a package. You greet the employee, tell them where you want to send your package and provide the sender's information before handing them the package.

Depending on the country you're in, you might be asked to show your identity card. 

Commands used by my mail client when it transfers an email to an SMTP server.

HELO or EHLO initiates an SMTP session
MAIL FROM specifies the sender's email address.
RCPT TO specifies the recipient's email address
DATA indicates that the client will begin sending the content of the email message.
. is sent on a line by itself to indicate the end of the email message.

