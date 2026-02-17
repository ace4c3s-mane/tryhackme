
The main challenge when studying networking protocols is that we don't get a chance to see the protocol "conversations" taking place.

All the technical complexities are hidden behind friendly and elegant user interfaces.

Tcpdum tool and it's libcap library were written in C and CPP. The libcap library is the foundation for various other networking tools today. Windows has it as winpcap.

Captured files can be saved to a file using the -w FILE option and saved as a pcap file.

You can also read packets using -r FILE. Very useful when learning about protocol behavior.

You can specify the number of packets to capture by specifying the count using -c COUNT.

Tcpdump will resolve IP addresses and print friendly domains where possible. To avoid making such DNS lookups, you can the the -n argument. Similarly, if you don't want port numbers to be resolved, such as 80 being resolved to http, you can use the -nn.


| Command                | Explanation                                                       |
| ---------------------- | ----------------------------------------------------------------- |
| `tcpdump -i INTERFACE` | Captures packets on a specific network interface                  |
| `tcpdump -w FILE`      | Writes captured packets to a file                                 |
| `tcpdump -r FILE`      | Reads captured packets from a file                                |
| `tcpdump -c COUNT`     | Captures a specific number of packets                             |
| `tcpdump -n`           | Don’t resolve IP addresses                                        |
| `tcpdump -nn`          | Don’t resolve IP addresses and don’t resolve protocol numbers     |
| `tcpdump -v`           | Verbose display; verbosity can be increased with `-vv` and `-vvv` |


You can run tcpdump without providing any filtering expressions, it isn't helpful. Just like in a social gathering, you don't try to listen to everyone at the same time, you would rather give your attention to a specific person or conversation.

Filtering by host:

We use the host name:

```tcpdump
sudo tcpdump host example.com -w http.pcap
```

If you want to limit the packets to those from a particular source IP address or hostname, you must use src host IP or  src host HOSTNAME. Similary, you can limit packets to those sent to a specific destination using dst host IP or dst host HOSTNAME.


Filtering by port:

If you want to capture all DNS traffic, you can limit the captured packets to those on port 53.

```tcpdump
sudo tcpdump -i ens5 port 53 -n
```


You can limit the packets to those from a particular source port number or to a particular destination port number using `src port PORT_NUMBER` and `dst port PORT_NUMBER`, respectively.

Filtering by Protocol

```tcpdump
sudo tcpdump -i ens5 icmp -n
```

Logical Operators

Three logical operators that can be handy:

- `and`: Captures packets where both conditions are true. For example, `tcpdump host 1.1.1.1 and tcp` captures `tcp` traffic with `host 1.1.1.1`.
- `or`: Captures packets when either one of the conditions is true. For instance, `tcpdump udp or icmp` captures UDP or ICMP traffic.
- `not`: Captures packets when the condition is not true. For example, `tcpdump not tcp` captures all packets except TCP segments; we expect to find UDP, ICMP, and ARP packets among the results.


#### Advanced Searching

We can limit the displayed packets to those smaller or larger than a certain length:

- greather LENGTH: Filters packets that have a length greater than or equl to the specified length.
- less LENGTH: Filters packets that have a length less than or equal to the specified length.

### Binary Operations

A binary operation works on bits. An operation takes one to two bits and returns one bit. They include &, I and !

Header  Bytes
We are filtering based on the contents of the header byte.

How can we tell Tcpdump to filter packets based on the contents of the protocol header bytes? 

Using pcap-filter, Tcpdump allows you to refer to the contents of any byte in the header using the following syntax:

```
proto[expr:size], where:
```

proto refers to the protocol,
expr indicates the byte offset, where 0 is the first byte.
size indicates the number of bytes that interest us, which can be one, two, or four. It is optional and is one by default

```
ether[0] & 1 != 0
```

This takes the first byte in the Ethernet header and the decimal number 1 and applies the &. It will return true if the result is not equal to the number (0).

The purpose of this filter is to show packets sent to a multicast address.  A multicast Ethernet address is a  particular address that identifies a group of devices intended to receive the same data.


#### Tcpflags

tcp-syn - TCP SYN (Synchronize)
tcp-ack TCP ACK (Acknowledge)
tcp-fin TCP FIN(Finish)
tcp-rst TCP RST (Reset)
tcp-push TCP Push

Based on the above, we can write:

tcpdump "tcp[tcpflags] == tcp-syn" to capture TCP packets with only the SYN flag set, while all the other flags are unset.

tcpdump "tcp[tcpflags] & tcp-syn != 0" to capture TCP packets with at least the SYN (Synchronize) flag set.

tcpdump "tcp[tcpflags] & (tcp-syn|tcp-ack) != 0" to capture TCP packets with at least the SYN (Synchronize) or ACK (Acknowledge) flags set.


Getting IP address of host that sent packets larger than 15000 bytes:

```
sudo tcpdump -r traffic.pcap "len > 15000" -nn
```

Getting packets with TCP reset flag:

```
sudo tcpdump "tcp[tcpflags] & (tcp-rst)" | wc
```


Tcpdump is a rich program with many options to customize how the packets are printed and displayed. We have selected to cover the following five options:

- `-q`: Quick output; print brief packet information
- `-e`: Print the link-level header
- `-A`: Show packet data in ASCII
- `-xx`: Show packet data in hexadecimal format, referred to as hex
- `-X`: Show packet headers and data in hex and ASCII