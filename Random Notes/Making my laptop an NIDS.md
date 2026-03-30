
The goal is to make my laptop a network  Intrusion Detection System

Enable IP Forwarding: IN simple terms, it's when a computer device receives network packets not meant for it and then sends them onward to another destination. Just like a router does.

```bash
sudo sysctl -w net.ipv4.ip_forward=1
```

sysctl -> This is a tool to change kernel networking settings.
-w - writes
net.ipv4.ip_forward=1 tells Linux to not just receive packets but forward them to other devices.

Normally, your laptop just receives traffic and responds but does not act as a router. With this enabled, it can now behave like a router (forwarding traffic between interfaces.)

### Making it Permanent

```bash
sudo nano /etc/sysctl.conf
```

Add the following at the bottom

```bash
net.ipv4.ip_forward=1
```

/etc/sysctl.conf is the startup configuration file
Setting this ensures the forwarding stays enabled after reboot. Otherwise the routing will keep breaking after every restart.

