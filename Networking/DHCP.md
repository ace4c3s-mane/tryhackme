Whenever we want to access a network, at the very least we need to configure the following:

- IP address along with subnet mask
- Router (gateway)
- DNS server

Manually configuring these settings is a good option, especially for servers. Servers are not expected to switch networks; you don’t carry your domain controller and connect it to the coffee shop WiFi.

Moreover, other devices need to connect to the servers and expect to find them at specific IP addresses.

DHCP is an applicatin-level protocol that relies on UDP; the server listens on UDP port 67 and the client sends from UDP port 68. Smartphones an laptops are configured to use DHCP by default.

![[Pasted image 20260208210739.png]]


The client broadcasts a DHCPDISCOVER message seeking the local DHCP server if one exists.

The server responds with a DHCPOFFER message with an IP address available for the client to accept.

The client responds with a DHCPREQUEST message to indicate that it has accepted the offered IP.

The server responds with a DHCPACK message to confirm that the offered IP address is now assigned to this client.


![[Pasted image 20260208211020.png]]

Before DORA happens, the device must first authenticate to the network by using the preshared key with the access point to ensure the communication with the server is secure.

At first, the client sends a broadcast, with source IP 0.0.0.0 (client has no ip yet)

Destination IP: 255.255.255.255 (limited broadcast)

Destination MAC: ff:ff:ff:ff:ff:ff (Ethernet broadcast)

Why broadcast? The client doesn't know where the DHCP server is (or even if one exists) and it has no IP to receive unicast replies. This message floods the network/subnet to ask :Any DHCP servers out there?



DHCP Offer: Usually unicast but can be broadcast depending on a flag.

The client sets a Broadcast flag in it's discover message.

- If flag = 1 (common for most clients that can't receive unicast IP packets before full config) server sends Offer as broadcast (to 255.255.255.255)
- if flag = 0 (client says "I can handle unicast"), server sends Offer as unicast to the offered IP or using the client's MAC.

In practice, many home routers and windows/linux clients set the flag to 1, offer is often broadcast. But modern systems sometimes allow unicast.


DHCP Request : Broadcast in the initial/selection phase: Source IP is still 0.0.0.0. Destination is still 255.255.255.255

Reason being; the client is telling all DHCP servers: "I'm accepting this offer from server X, please don't give that IP to anyone else" It has to be broadcast to other servers (that might have also offered IPs) know to withdraw their offers.


DHCP ACK: Usually unicast, but can be broadcast if the flag was set. Once the server confirms, it sends the final IP config typically to the now-"known" client IP.

| Message  | From   | Broadcast or Unicast?            | Reason                              |
| -------- | ------ | -------------------------------- | ----------------------------------- |
| Discover | Client | **Broadcast** (always)           | No IP, no server known              |
| Offer    | Server | Unicast (preferred) or Broadcast | Depends on client's BROADCAST flag  |
| Request  | Client | **Broadcast** (initial)          | To notify all servers of selection  |
| ACK      | Server | Unicast (preferred) or Broadcast | Depends on flag; final confirmation |