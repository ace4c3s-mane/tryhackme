It operates at the application layer.

Here are the main reasons why DNS belongs at the application layer:

1. Only applications care about human-readable names -  Computers and routers work exclusively with IP addresses (numbers). They don't understand or need domain names like google.com or example.co.ke.

   Domain names are purely a convenience for humans and for application software (browsers, email clients, mobile apps, etc.). Therefore, the translation from name → IP address is something applications request — it doesn't belong in lower layers that are concerned with moving bits around.

2. DNS is an application-level service / protocol. DNS defines its own query format, response format, resource records (A, AAAA, MX, CNAME, TXT, etc.), message structure, error codes, etc.

   These are high-level concepts that only the application (or the DNS client library inside it) understands.
   
   Lower layers (transport, network, data link) have no idea what a "CNAME" or "NS record" is — they just carry the bytes.

3. It runs on top of transport-layer protocol -   DNS queries/responses are encapsulated in UDP (port 53, most common) or sometimes TCP (port 53). This is the classic sign of an application-layer protocol: it uses transport protocols (UDP/TCP) rather than being part of them.

DNS traffic users port 53 by default or port 53 as a default fallback. Types of DNS records include:

1. A record: The A (address) record maps a hostname to one or more IPv4 addresses.
2. AAAA Record - Is similar to A record but it is for IPv6. 
3. CNAME Record - The CNAME record maps a domain name to another domain name. For example www.example.com can be mapped to example.com  or example.org
4. MX Record: The MX (Mail Exchange) record specifies the mail server responsible for handling emails for a domain.


### nslookup

It's a tool used to find the IP address of a domain from the commandline.


#### What DNS Records Actually Contain

Every DNS record follows a basic format

```text
name TTL Class type value/data
```


name: the domain or subdomain this record is for (www.example.com or just @ meaning the root domain)

TTL - Time to Live (How many seconds other servers should cache this before asking again)

class - Almost always IN(internet)

Type - What kind of record this is (A, MX)

Value/data - The actual information (IP Address, another name, text string etc.)


NS Records (These are official DNS servers responsible for this domain) - Tells the world who to ask for all records of this domain.

MX records tell the world where to deliver a mail for any domain.