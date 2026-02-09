The goal is to find hidden directories or files.

### Tools


|Rank|Tool|Speed|Recursive?|Best for CTF because|Language|
|---|---|---|---|---|---|
|1|**ffuf**|★★★★★|Yes|Extremely fast + very flexible filters|Go|
|2|**feroxbuster**|★★★★☆|Yes (strong)|Recursive by default, smart auto-filtering|Rust|
|3|**gobuster**|★★★★☆|No|Still very common, simple syntax, vhost fuzzing|Go|
|4|**dirsearch**|★★★☆☆|Yes|Very good default filters & extensions|Python|

**Recommendation for most CTFs in 2025/2026**: start with **ffuf** or **feroxbuster**


Examples

```bash
ffuf -u http://target:port/FUZZ -w /usr/share/seclists/Discovery/Web-Content/raft-medium-directories.txt \
  -fc 404 -fs 0 -t 50 -o results.json -of json
```

-fc 404, 403,500 - Filter (hide) these status codes.
-fs 1234 - Filter responses of this exact size.
-fr "Forbidden" - Filter pages containing this regex
-mc - Match only these codes.
-recursion -Recursive fuzzing depth
-t 30-80 - Threads (Too high leads to IP ban, 40 - 80 usually a sweet spot)
-rate 150 - Requests per second limit, when rate limited.


### Optimization strategies

Order of wordlists - Start small $ smart, then go deeper.

```bash
1. raft-small-directories.txt / common.txt             (~1–5k entries)
2. directory-list-2.3-small.txt / quickhits.txt        (~20–50k)
3. raft-medium-directories.txt / directory-list-2.3-medium.txt   (~200–300k)
4. big.txt / raft-large-directories.txt                 (only if time allows)
```

### Extensions in ctf

```bash
-e .php,.bak,.old,.zip,.js,.txt,.env,.config,.yaml,.yml,.git,.DS_Store
```


Recursive fuzzing – when you find something interesting


```bash
ffuf -u https://target/FUZZ -w wordlist.txt -recursion -recursion-depth 2 -recursion-strategy greedy
```



### Feroxbuster

```bash
ffuf -u https://target/FUZZ -w wordlist.txt -recursion -recursion-depth 2 -recursion-strategy greedy
```


### enumeration for the machine to find interesting stuff

Use: enum4Linux

```bash
enum4linux -a > output.txt
```


### Difference btw enum4Linux and linpeas

|Aspect|enum4linux|linPEAS|
|---|---|---|
|Runs where?|Your machine (remote target)|On the compromised target machine|
|Protocol/Service|SMB/Samba (139/445)|Local Linux system (no network needed)|
|Main goal|Discover remote users/shares/policies|Find local privesc paths|
|Needs shell?|No|Yes (you need to execute it locally)|
|Output style|Plain text, grep-friendly|Color-coded, prioritized (very readable)|
|Common in THM room|Early (port enum → usernames)|Later (after SSH → root)|
|Example command|enum4linux -a 10.10.x.x > out.txt|
