Ip: 10.112.167.112

Echo into /etc/hosts

```bash
echo "10.112.167.112 keldagrim" | sudo tee -a /etc/hosts
```

Nmap Scan

```bash
sudo nmap -sT -Pn -T4 --min-rate 5000 -p- keldagrim
```

Results

```bash
gerald@kali:~ $ nmap -n -Pn -T4 --min-rate 5000 -p- keldagrim
Starting Nmap 7.98 ( https://nmap.org ) at 2026-02-27 21:31 -0500
Warning: 10.112.167.112 giving up on port because retransmission cap hit (6).
Nmap scan report for keldagrim (10.112.167.112)
Host is up (0.15s latency).
Not shown: 65453 closed tcp ports (reset), 80 filtered tcp ports (no-response)
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 24.44 seconds
```

Deep Scan

```bash
gerald@kali:~ $ nmap -sC -sV -p 22,80 keldagrim              
Starting Nmap 7.98 ( https://nmap.org ) at 2026-02-27 21:33 -0500
Nmap scan report for keldagrim (10.112.167.112)
Host is up (0.15s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.13 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 34:21:88:d2:bd:52:01:ea:0f:c8:7c:fa:35:8f:60:4a (RSA)
|   256 a1:03:de:c8:18:f1:c1:6a:7d:7d:59:03:23:ce:47:68 (ECDSA)
|_  256 2f:56:8d:e3:a8:e0:ea:16:ec:df:61:17:12:e8:9d:d8 (ED25519)
80/tcp open  http    Werkzeug httpd 3.0.6 (Python 3.8.10)
| http-cookie-flags: 
|   /: 
|     session: 
|_      httponly flag not set
|_http-server-header: Werkzeug/3.0.6 Python/3.8.10
|_http-title:  Home page 
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 21.48 seconds
                                                            
```