
A utility like Netcat will handle the connection and allow the attacker to interact with the exposed shell, but netcat is not the only utility that will allow us to do that.


#### Rlwrap

It's a small utility that uses the GNU readline library to provide editing keyboard and history.

We can enhance the netcat with Rlwrap.

```bash
rlwrap nc -lvnp 8080
```

rlwrap gives arrow key support, better command editing, history and tab completion.


#### Ncat

Is an improved version of Netcat distributed by NMAP project. It provides extra features like SSL encryption.

```bash
ncat -lnvp 4444
```

Listening for reverse shell with ssl

```bash
ncat --ssl -lvnp 4444
```

The --ssl option enables SSL encryption for the listener.


#### Socat

It's a utility that allows you to create a socket connection between two data sources, in this case two different hosts.

Default Usage (Listening for Reverse Shell)

```bash
socat -d -d TCP-LISTEN:443 STDOUT
```

The command above used the -d option to enable verbose output.  Using -d -d will increase the verbosity of the commands. 

The TCP-LISTEN:443 option creates a TCP listener on port 443, establishing a server socket for incoming connections. Finally, the STDOUT option directs any incoming data to the terminal.