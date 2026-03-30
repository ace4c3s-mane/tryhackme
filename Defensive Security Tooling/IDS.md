
They play the role of surveillance cameras when firewalls fail to detect the malicious traffic at the entrance.

However, it does not act on the detections, it only notifies the security admins about them.

### Categories of IDS

Host Intrustion Detection Systems
Network Intrustion Detection Systems

![[Pasted image 20260320061054.png]]


### Detection Modes

Signature-based IDS - Attacks have their unique patterns and that's what we call a signature. These signatures are preserved by the IDS in their databases so that  if the same attack happens in the future, it gets detected bu it signature and reported to the sec admins for action.

It's however difficult to detect zero days

Anomaly-based IDS - This type of IDs first learns the normal behavior(baseline) of the network or system and performs detections if there is any deviation from the normal behavior.

It can also detect zero-days because it doesn't rely on available signatures for detection. They detect abnormalities inside the network or system by comparing the current state with the normal behavior (baseline)

Hybrid IDS  - Combines the detection methods of signature based IDS and anomaly-based IDS.



### Snort 

One of the most widely used open source IDS solutions. It uses signature-based and anomaly-based detections to identify known threats.

These are defined in the rule files of the Snort Tool.

Running snort on a PCAP file

```shell-session
ubuntu@tryhackme:~$ sudo snort -q -l /var/log/snort -r Task.pcap -A console -c /etc/snort/snort.conf
```

