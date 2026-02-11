
Unlike HTTP which is designed to retrieve web pages, FTP is designed to transfer files.

It's very efficient for file transfer and when all conditions are equal, it can achieve higher speeds than HTTP.

Example commands defined the FTP protocol are:

- USER is used to input the username
- PASS is used to enter the password
- RETR is used to download a file from the client to the FTP server

FTP listens for incoming connections requests from clients on TCP port 21 by default; data transfer is conducted via another connection from the client to the server.

The FTP client initiates an outbound connection to the server's port 21, usually from a random high-numbered (ephemeral) port on the client side.

FTP has two separate connections instead of one:

### Control/command connection - The 'conversation' channel
Data Connection - The actual file transfer/directory listing channel.

The control connection is always the same in both modes. The big difference is only in how the data connection gets created.

The control/Command Connection is like the "chat or instructions line". The client always starts it. Client connects to the servers port 21. Server listens on port 21. Over this connection, you do: Login(username/password), Send commands like (ls, get file.txt, put photo.jpg, cd folder), server sends replies like '226 transfer complete'.

This connection stays open the whole session. IT's TCP reliable and only carries text commands + responses (small data)


### The Data Connection

When you actually want to transfer something like (file, folder list, etc), FTP opens a second TCP connection just for the raw data bytes.

##### Active Mode (older, server initiates data connection)

1. Control connection already open(client -> server:21)
2. You type e.g. ls or get file.txt
3. Client says to server over control connection: "Hey server, when you want to send me data, connect back to my IP and this port number I'm giving you now" (This is the PORT command)
4. Client starts listening on that port it just told the server about.
5. Server connects out from it's port 20 -> the client's IP and port
6. Data flows over this new connection (server pushes data to client, or client pushes to server)

Key point is that server actively makes the outgoing connection for data. Problem today is Firewalls/NAT on home routers or company networks usually block incoming connections -> This often fails.

#### Passive Mode

1. Connection already open (client -> server:21)
2. You type e.g ls or get file.txt)
3. Client says to server over control connection: "I want data, please tell me which port you are listening on" (This is the PASV command - "passive")
4. Server picks a random high port (e.g 50000 - 51000, configurable), starts listening on it and tells the client "OK, connect to my IP and this port" (Reply code 227 Entering passive Mode) 
5. Client now connects out from its random high port -> server's high port.

Key point is the client makes both connections (control + data). Advantage today: Firewalls/NAT allow outgoing connections easily - This always always works.

![[Pasted image 20260210214234.png]]

![[Pasted image 20260210214300.png]]