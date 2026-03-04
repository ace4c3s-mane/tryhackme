A security Operations Center is a dedicated facility operated by a specialized team.

This team aims to continuously monitor an organization's network and resources and identify suspicious activity to prevent damage.

The main focus of the SOC team is to keep Detection and Response intact.

![[Pasted image 20260304032747.png]]

### Detection

**Detect Vulnerabilities** - A vulnerability is a weakness that an attacker can exploit to carry out things beyond their permission level.

**Detect unauthorized activity** 

**Detect Policy Violations** - A security policy is a set of rules and procudures created to protect a company against security threats and ensure compliance. It varies from company to company.

**Detect Intrusions** - Unauthorized access to systems and networks.


### Pillars of a SOC

People
Processes 
Technology

The People
![[Pasted image 20260304033323.png]]

SOC Analyst (Level1) - Anything detected by the security solution would pass through these analysts first. there are the first responders to any detection. They perform basic alert triage to determine if a specific detection is harmful.

SOC Analyst Level 2: Level 2 analysts help level 1 dive deeper into the investigations and correlated the data from multiple data sources to perform a proper analysis.

****SOC Analyst (Level 3)**:** Level 3 Analysts are experienced professionals who proactively look for any threat indicators and support in the incident response activities. The critical severity detection reported by Level 1 and Level 2 Analysts are often security incidents that need detailed responses, including containment, eradication, and recovery. This is where Level 3 analysts’ experience comes in handy.

**Security Engineer:** All analysts work on security solutions. These solutions need deployment and configuration. Security Engineers deploy and configure these security solutions to ensure their smooth operation.

**Detection Engineer:** Security rules are the logic built behind security solutions to detect harmful activities. Level 2 and 3 Analysts often create these rules, while the SOC team can sometimes also utilize the detection engineer role independently for this responsibility.

**SOC Manager:** The SOC Manager manages the processes the SOC team follows and provides support. The SOC Manager also remains in contact with the organization’s CISO (Chief Information Security Officer) to provide him with updates on the SOC team’s current security posture and efforts.

### Process

Alert Triage - Basis of the SOC team. 
The first response to any alert is to perform triage. The triage is focused on analyzing the specific alert.

This determines the severity of the alert and helps us prioritize it. It's all about answering the 5 Ws.

![[Pasted image 20260304050224.png]]

|5 Ws|Answers|
|---|---|
|What?|A malicious file was detected on one of the hosts inside the organization’s network.|
|When?|The file was detected at 13:20 on June 5, 2024.|
|Where?|The file was detected in the directory of the host: "GEORGE PC".|
|Who?|The file was detected for the user George.|
|Why?|After the investigation, it was found that the file was downloaded from a pirated software-selling website. The investigation with the user revealed that they downloaded the file as they wanted to use a software for free.|

### Reporting

The detected harmful alerts need to be escalated to higher-level analysts for a timely response and resolution. These alerts are escalated as tickets and assigned to the relevant people. The report should discuss all the 5 Ws along with a thorough analysis, and screenshots should be used as evidence of the activity.

### Incidence Response and Forensics

Sometimes, the reported detections point to highly malicious activities that are critical. In these scenarios, high-level teams initiate an incident response. 


Security Solutions centralize all the information of the devices or apps present in the network and automate the detection and response capabilities.


**The Tools**

SIEM - Security Information and Event Management. This tool collects logs from various network devices referred to as log sources. 

Detection rules are configured in the SIEM solution which contains logic to identify suspicious activity.

The SIEM provides us with the detections after correlating them with multiple log sources and alerts us in case of a match with any of the rules.

Modern SIEM solutions surpass this rule based detection analysis, providing us with user behavior analytics and threat intelligence capability. ML algorithms support this to enhance the detection capabilities.

SIEM provides the Detection capabilities only.

**EDR** - Endpoint Detection and Response provides the SOC team with detailed real-time and historical visibility of the device's activities. It operates on the endpoint level and can carry out automated responses. it has extensive detection capabilities for endpoints, allowing you to investigate them in detail and respond in a few clicks.

Firewall - Functions purely for network security and acts as a barrier between your internal and external networks.