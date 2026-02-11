
Internet Control Message Protocol is mainly used for network diagnostics and error reporting.

Two popular commands rely on ICMP, and they are instrumental in network troubleshooting and network security.

ping - uses ICMP to test connectivity to a target system and measures the round-trip time. It can be used to learn that the target is alive and its reply can reach our system.

traceroute: This command on linux and tracert on Windows systems. it uses ICMP to discover the route from your host to the target.

Many things such as firewalls, system being offline might prevent us from getting a reply.

**Traceroute**

The Internet Protocol has a field called Time-to-Live that indicates the maximum number of routers a packet can travel through before it is dropped.

The router decrements the packet's  TTL by one before it sends it across. When the TTL reaches zero, the router drops the packet and sends an ICMP Time Exceeded message (ICMP Type 11) ( In this context, time is measured in the number of routers, not seconds)



