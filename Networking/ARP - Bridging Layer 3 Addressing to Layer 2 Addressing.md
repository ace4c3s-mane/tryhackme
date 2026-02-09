As two hosts communicate over a network, an IP packet is encapsulated within a data link frame as it travels over layer 2.

We use two data link layers, Ethernet (IEEE 802.3 ) and WIFI (802.11)

Whenever one host needs to communicate with another host on the same Ethernet or WIFI, it must send the IP packet within a data link layer frame.

Although it knows the IP address of the target host, it needs to look up the target's MAC address so the proper data link header can be created.


Devices on the same ethernet network do not need to know each other's MAC addresses all the time; they only need to know each other's MAC addresses while communicating.

Two devices on the same Ethernet cannot communicate without knowing each other's MAC addresses.

ARP protocol makes it possible to find MAC addresses of another device on the Ethernet.

ARP request is sent from the MAC address of the requester to the broadcast MAC address.

It's considered layer 2 because it deals with MAC addresses. Others would argue that it is part of layer 3 because it supports IP operations. What it essential to know is that ARP allows the translation from layer 3 addressing to layer 2 addressing.