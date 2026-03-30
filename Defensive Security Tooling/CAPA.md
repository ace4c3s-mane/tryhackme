
One of the challenges when analyzing potentially malicious software is that we risk our machine or environment being compromised when we run it unless we have a or a completely isolated environment where we can test all we want.

There are two types of analysis, dynamic analysis and static analysis.

CAPA (Common Analysis Platform for Artifacts) is a tool developed by the FireEye Mandiant team.

It's designed to identify the capabilities present in executable files like Portable Executables (PE), ELF binaries, .NET modules, shellcode and even sandbox reports.

It does so by analyzing the file and applying a set of rules that describe common behaviors, allowing it to determine what the program is capable of doing such as network communication, file manipulation, process injection and many more.

The beauty of CAPA is that it encapsulates years of reverse engineering knowledge into an automated tool, making it accessible even to those who may not be experts in reverse engineering.

This tool is particularly useful in malware analysis and threat hunting, where understanding a binary's capabilities is crucial for incident response and defensive measures.

### Challenge

To solve this challenge, I had to use xfreerdp to connect to the machine

```bash
xfreerdp /u:username /p:password /v:ip /f /dynamic-resolution
```


The MITRE ATT&CK (Adversarial Tactics, Techniques, and Common Knowledge) framework is a comprehensive global knowledge repository that meticulously documents the tactics and techniques employed by threat actors at every stage of a cyber-attack.

It functions as a strategic playbook, providing detailed insights into attackers' methods, from **gaining initial access** to **maintaining a presence**, **escalating privileges**, **evading defenses**, **moving laterally within a network**,and much more.



### Malware Attribute Enumeration & Characterization

A specialized language designed to encode and communicate complex details concerning malware.

It contains an extensive range of attributes, including behaviors, artifacts and interconnections among various  instances of malware.

This language functions as a standardized system for tracking and analyzing the complicated complexities of malware.



### Malware Behavior Catalogue (MBC)

Is designed to support various aspects of malware analysis, such as labeling, similarity analysis and standardized reporting.

Essentially, it serves as a catalogue of malware objectives and behaviours.