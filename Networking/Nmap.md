
It uses multiple ways to determine who is online:

If you want to scan all the IP addresses from 192.168.0.1 to 192.168.0.10, you can write 192.168.0.1-10

If you want to scan a subnet, you can express it as 192.168.0.1/24 which is equivalent to 192.168.0.0.255

Nmap offers -sn option to discover the online hosts on a network. It means "ping scan only(no port scanning)"

It tries to identify live hosts using methods like: 

- ARP requests (on local LANS - very reliable)
- ICMP echo requests (ping)
- TCP/UDP probes (depending on privileges/settings)

This discovers devices connected to the same local network as I am including phones, laptops, Printers, e.t.c because on a local subnet, Nmap uses ARP discovery, which finds anything that currently has an IP address on that network.

Using Nmap as a local (non-root) user would limit us to fundamental types of scans such as ICMP echo and TCP connect scans.

Because we are scanning the local network, where we are connected via Ethernet or WiFi, we can look up the MAC addresses of the devices. Consequently, we can figure out the network card vendors, which is beneficial information as it can help us guess the type of target device(s).

When scanning a directly connected network, Nmap starts by sending ARP requests. When a device responds to the ARP request, Nmap labels it as "Host is Up"


We can scan a remote host, not on our local network using:

```nmap
nmap -sn 192.168.11.0/24
```


Before doing an Nmap scan, we can always run:

```nmap
nmap -sL 192.168.11.0/24
```


To list all the devices to be scanned.


### Port Scanning

We can discover services on a network listening on Live hosts. By network service, we mean any process that is listening for incoming connections on a TCP or UDP port.


The easiest and most basic way to know whether a TCP port is open would be to attempt to telnet to the port.

### Nmap's Connect Scan

The connect scan can be triggered using -sT. It tries to complete the TCP three-way handshake with every target TCP port.

If the port turns out to be open and Nmap connects successfully, Nmap will tear down the established connection.

### SYN Scan (Stealth)

Unlike the connect scan which tries to connect to the target TCP port, i.e complete a three-way handshake, the SYN scan only executes the first step: 

It sends a TCP SYN packet.

Consequently, the TCP three-way handshake is never completed. The advantage is that this is expected to lead to fewer logs as the connection is never established, and hence it is considered a relatively stealthy scan. 

You can select the SYN scan using the -sS flag


### Scanning UDP Ports

Although most services use TCP for communication, many use UDP like NTP, DNS and DHCP.

UDP does not require establishing a connection and tearing it down afterwords. It's very suitable for real-time communication such as broadcasts.

Nmap offers the -sU option to scan for UDP services.


### Limiting the Target Ports

Nmap scans the most common 1,000 ports by default. 

-F is for Fast Mode, which scans the 100 most common ports.
-p[range] allows you to specify a range of ports to scan. -p10-1024 scans from port 10 to port 1024.


### OS Detection

You can enable OS detection by adding the -O option.

### Service and Version Detection

You can use -sV option to know what services are listening on the open ports.

If you wanted to combine -O and -sV, that would be -A. This option enables OS detection, version scanning and traceroute.


#### Forcing the Scan

When we run our port scan, such as using -sS, there is a possibility that the target host does not reply during the host discovery  phase (e.g a host doesn't reply to ICMP requests)

Consequently, Nmap will mark this host as down and won't launch a port scan agaist it. We can ask Nmap to treat all hosts as online and  port scan every host, including those that didn't respond during the host discovery phase. The choice can be triggered by adding the -Pn Option.


### Timing 

Running my scan at its normal speed might trigger an IDS or other security solutions. It is reasonable to control how fast a scan should go.

Nmap gives you six timing templates and the names say it all: paranoid(0), sneaky(1), polite(2), normal(3), aggressive(4) and insane (5)


A second helpful option is the number of parallel service probes. The number of parallel probes can be controlled with --min-parallelism <numprobes>

These options can be used to set a minimum and maximum on the number of TCP and UDP port probes active simultaneously for a host group.

By default, namp will automatically control the number of parallel probes. If the network is performing poorly, i.e, dropping packets, the number of parallel probes might fall to one; furthermore, if the network performs flawlessly, the number of parallel probes can reach several hundred.

A similar helpful option is --min-rate <number> and --max-rate<number>.  As the names indicate, they can control the mininum and maximum rates at which nmap sends packets.

The rate is provide as the number of packets per second. The rate applies to the whole scan, and not to a single host.

--host-timeout <time> specifies the maximum time you are willing to wait and is suitable for slow hosts or hosts with slow network connections.


For debugging nmap results, we can use -d option.

