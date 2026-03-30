There are two types of logs generated.

Host-Centric Log Sources and Network-Centric Log Sources

Host-Centric sources capture events that occurred within or related to the host while network-centric log sources capture logs that are generated when the hosts communicate with each other.

Devices that generate host-centric logs include Windows, Linux, servers, etc while those that generate Network-Centric Logs include Firewalls, IDS/IPS, routers. 

Examples of network-centric logs would include:

	SSH Connection
	A file being accessed via FTP
	Web Traffic
	A network sharing activity

SIEM is a security solution that collects logs from various types of log sources, standardizes their format into a consistent one, correlates them and detects malicious activities using detection rules.

![[Pasted image 20260306070921.png]]
### Features of SIEM
- Centralized Log Collection - Logs are pulled through lightweight agents or APIs and populated in one place.

- Normalization of Logs - Breaking down a log into several fields for ease of understanding is called Parsing. While converting all the logs of various sources into one consistent format is known as Normalization.

- Correlation of Logs - SIEM does this and finds relationships between different logs from different sources.

- Real-time Alerting

- Dashboards and reporting


## Log Ingestion

Process of collecting, importing and storing logs from different systems into a SIEM platform.

How SIEM Does this:

1. Agent /Forwarder - a lightweight tool that gets installed in an endpoint. it's configured to capture and send all the important logs tot he SIEM server.
2. Syslog - Widely used protocol to collect data from various system like web servers, databases, etc and send real-time data to the centralized destination.
3. Manual Upload - Some like SPLUNK allow users to ingest offline data for quick analysis.
4. Port-Forwarding - SIEM solutions can also be configured to listen on a certain port and then the endpoints forward the data to the SIEM instance on the listening port.
