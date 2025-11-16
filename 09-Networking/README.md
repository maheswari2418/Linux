# 🌐 Linux Networking Guide

> Complete guide to Linux networking commands and configuration

---

## 📑 Table of Contents

| Section | Description |
|---------|-------------|
| [Introduction](#introduction) | What is Linux networking |
| [Why Networking?](#why-networking) | Importance and benefits |
| [Network Basics](#network-basics) | Fundamental concepts |
| [Network Interfaces](#network-interfaces) | Managing network adapters |
| [IP Configuration](#ip-configuration) | IP address management |
| [DNS Configuration](#dns-configuration) | Domain name resolution |
| [Routing](#routing) | Network routing |
| [Network Testing](#network-testing) | Connectivity testing |
| [Port and Services](#port-and-services) | Port management |
| [Network Statistics](#network-statistics) | Connection monitoring |
| [Firewall](#firewall) | Security and filtering |
| [Network Troubleshooting](#network-troubleshooting) | Diagnosing issues |
| [Advanced Networking](#advanced-networking) | Advanced tools |
| [Practical Examples](#practical-examples) | Real-world scenarios |

---

## Introduction

### What is Linux Networking?

| Concept | Description |
|---------|-------------|
| **Networking** | Communication between computers and devices |
| **TCP/IP** | Protocol suite for internet communication |
| **Interface** | Network adapter (physical or virtual) |
| **IP Address** | Unique identifier for device on network |
| **Port** | Endpoint for network communication |
| **Socket** | IP address + port combination |

### Key Networking Components

| Component | Description | Example |
|-----------|-------------|---------|
| **Network Interface** | Hardware/virtual adapter | eth0, wlan0, enp3s0 |
| **IP Address** | Network identifier | 192.168.1.100 |
| **Subnet Mask** | Network range definition | 255.255.255.0 or /24 |
| **Gateway** | Router/exit point | 192.168.1.1 |
| **DNS Server** | Name resolution | 8.8.8.8, 1.1.1.1 |
| **MAC Address** | Hardware address | 00:1A:2B:3C:4D:5E |

---

## Why Networking?

### Importance of Networking Knowledge

| Reason | Description | Example |
|--------|-------------|---------|
| **Connectivity** | Connect to internet and other devices | Browse web, access servers |
| **Troubleshooting** | Diagnose network issues | Fix connection problems |
| **Server Management** | Configure network services | Web servers, databases |
| **Security** | Protect against attacks | Firewall configuration |
| **Performance** | Optimize network speed | Identify bottlenecks |
| **Remote Access** | SSH, remote desktop | Manage remote servers |

### Use Cases

| Scenario | Networking Task |
|----------|----------------|
| **Can't access internet** | Check IP, gateway, DNS |
| **Slow connection** | Test bandwidth, check latency |
| **Setup server** | Configure static IP, open ports |
| **Security hardening** | Configure firewall rules |
| **Remote administration** | Setup SSH access |
| **File sharing** | Configure network shares |

---

## Network Basics

### Network Protocols

| Protocol | Layer | Purpose | Port |
|----------|-------|---------|------|
| **TCP** | Transport | Reliable connection | Various |
| **UDP** | Transport | Fast, connectionless | Various |
| **IP** | Network | Addressing and routing | N/A |
| **HTTP** | Application | Web traffic | 80 |
| **HTTPS** | Application | Secure web | 443 |
| **SSH** | Application | Secure remote access | 22 |
| **FTP** | Application | File transfer | 20, 21 |
| **DNS** | Application | Name resolution | 53 |
| **DHCP** | Application | IP assignment | 67, 68 |

### IP Address Types

| Type | Description | Example | Range |
|------|-------------|---------|-------|
| **IPv4** | 32-bit address | 192.168.1.100 | 0.0.0.0 to 255.255.255.255 |
| **IPv6** | 128-bit address | 2001:0db8::1 | Large address space |
| **Private IPv4** | Non-routable (local) | 192.168.x.x, 10.x.x.x | RFC 1918 ranges |
| **Public IPv4** | Internet routable | Varies | Non-private ranges |
| **Loopback** | Local machine | 127.0.0.1 | 127.0.0.0/8 |

### Common Private IP Ranges

| Range | Subnet | Usage |
|-------|--------|-------|
| **10.0.0.0 - 10.255.255.255** | 10.0.0.0/8 | Large networks |
| **172.16.0.0 - 172.31.255.255** | 172.16.0.0/12 | Medium networks |
| **192.168.0.0 - 192.168.255.255** | 192.168.0.0/16 | Home/small networks |

### Common Ports

| Port | Service | Protocol | Purpose |
|------|---------|----------|---------|
| **20, 21** | FTP | TCP | File transfer |
| **22** | SSH | TCP | Secure shell |
| **23** | Telnet | TCP | Remote terminal (insecure) |
| **25** | SMTP | TCP | Email sending |
| **53** | DNS | TCP/UDP | Domain name resolution |
| **80** | HTTP | TCP | Web traffic |
| **443** | HTTPS | TCP | Secure web |
| **3306** | MySQL | TCP | Database |
| **5432** | PostgreSQL | TCP | Database |
| **8080** | HTTP Alt | TCP | Alternative web port |

---

## Network Interfaces

### Viewing Network Interfaces

| Command | Description | Output |
|---------|-------------|--------|
| `ip link show` | Show all interfaces | Interface list with status |
| `ip addr show` | Show IP addresses | Interfaces with IPs |
| `ifconfig` | Show interfaces (legacy) | Interface details |
| `ifconfig -a` | Show all (including down) | All interfaces |
| `ip link` | Brief interface list | Link status |

### Interface Naming

| Name Type | Format | Example | Description |
|-----------|--------|---------|-------------|
| **Traditional** | ethX, wlanX | eth0, wlan0 | Old naming scheme |
| **Predictable** | enpXsY, wlpXsY | enp3s0, wlp2s0 | Modern naming |
| **Virtual** | Various | lo, docker0, virbr0 | Virtual interfaces |

### Interface States

| State | Description |
|-------|-------------|
| **UP** | Interface is active |
| **DOWN** | Interface is inactive |
| **RUNNING** | Interface has carrier signal |
| **LOWER_UP** | Physical link is up |

### Managing Interfaces

| Command | Description |
|---------|-------------|
| `ip link set eth0 up` | Bring interface up |
| `ip link set eth0 down` | Take interface down |
| `ifconfig eth0 up` | Bring up (legacy) |
| `ifconfig eth0 down` | Take down (legacy) |

### Interface Examples

| Task | Command |
|------|---------|
| Show all interfaces | `ip link show` |
| Show IP addresses | `ip addr show` |
| Show specific interface | `ip addr show eth0` |
| Bring interface up | `sudo ip link set eth0 up` |
| Bring interface down | `sudo ip link set eth0 down` |
| Show MAC addresses | `ip link show` |

---

## IP Configuration

### Viewing IP Configuration

| Command | Description |
|---------|-------------|
| `ip addr` | Show all IP addresses |
| `ip addr show eth0` | Show specific interface |
| `ifconfig` | Show IP config (legacy) |
| `hostname -I` | Show all IP addresses |
| `ip -4 addr` | Show only IPv4 |
| `ip -6 addr` | Show only IPv6 |

### Setting IP Address (Temporary)

| Command | Description |
|---------|-------------|
| `ip addr add 192.168.1.100/24 dev eth0` | Add IP address |
| `ip addr del 192.168.1.100/24 dev eth0` | Remove IP address |
| `ifconfig eth0 192.168.1.100 netmask 255.255.255.0` | Set IP (legacy) |

### DHCP Configuration

| Command | Description |
|---------|-------------|
| `dhclient eth0` | Request IP via DHCP |
| `dhclient -r eth0` | Release DHCP lease |
| `dhclient -v eth0` | Verbose DHCP request |

### Static IP Configuration Files

#### Ubuntu/Debian (Netplan)

| File | Purpose |
|------|---------|
| `/etc/netplan/*.yaml` | Netplan configuration |

**Example Netplan Config:**
```yaml
network:
  version: 2
  ethernets:
    eth0:
      dhcp4: no
      addresses:
        - 192.168.1.100/24
      gateway4: 192.168.1.1
      nameservers:
        addresses: [8.8.8.8, 8.8.4.4]
```

#### RHEL/CentOS (NetworkManager)

| File | Purpose |
|------|---------|
| `/etc/sysconfig/network-scripts/ifcfg-eth0` | Interface config |

**Example ifcfg Config:**
```
BOOTPROTO=static
DEVICE=eth0
IPADDR=192.168.1.100
NETMASK=255.255.255.0
GATEWAY=192.168.1.1
DNS1=8.8.8.8
DNS2=8.8.4.4
ONBOOT=yes
```

### Network Configuration Commands

| Command | Description |
|---------|-------------|
| `sudo netplan apply` | Apply Netplan config (Ubuntu) |
| `sudo systemctl restart NetworkManager` | Restart network (RHEL) |
| `sudo systemctl restart networking` | Restart network (Debian) |
| `nmcli` | NetworkManager CLI |
| `nmtui` | NetworkManager TUI |

---

## DNS Configuration

### DNS Files

| File | Purpose |
|------|---------|
| `/etc/resolv.conf` | DNS server configuration |
| `/etc/hosts` | Local hostname to IP mapping |
| `/etc/nsswitch.conf` | Name service switch config |

### /etc/resolv.conf Format

```
nameserver 8.8.8.8
nameserver 8.8.4.4
search example.com
```

### /etc/hosts Format

```
127.0.0.1       localhost
192.168.1.100   myserver.local myserver
```

### DNS Commands

| Command | Description |
|---------|-------------|
| `nslookup domain` | Query DNS server |
| `dig domain` | Detailed DNS lookup |
| `host domain` | Simple DNS lookup |
| `cat /etc/resolv.conf` | View DNS servers |
| `resolvectl status` | DNS status (systemd) |

### DNS Lookup Examples

| Task | Command |
|------|---------|
| Lookup domain | `nslookup google.com` |
| Detailed lookup | `dig google.com` |
| Reverse lookup | `dig -x 8.8.8.8` |
| Query specific server | `nslookup google.com 8.8.8.8` |
| Check DNS servers | `cat /etc/resolv.conf` |
| Trace DNS path | `dig +trace google.com` |

### Common DNS Servers

| Provider | Primary | Secondary |
|----------|---------|-----------|
| **Google** | 8.8.8.8 | 8.8.4.4 |
| **Cloudflare** | 1.1.1.1 | 1.0.0.1 |
| **Quad9** | 9.9.9.9 | 149.112.112.112 |
| **OpenDNS** | 208.67.222.222 | 208.67.220.220 |

---

## Routing

### Viewing Routes

| Command | Description |
|---------|-------------|
| `ip route` | Show routing table |
| `ip route show` | Show all routes |
| `route -n` | Show routes (legacy) |
| `netstat -rn` | Show routes (legacy) |
| `ip route get 8.8.8.8` | Show route to specific IP |

### Routing Table Components

| Component | Description |
|-----------|-------------|
| **Destination** | Target network |
| **Gateway** | Next hop router |
| **Genmask** | Subnet mask |
| **Interface** | Output interface |
| **Metric** | Route priority |

### Managing Routes

| Command | Description |
|---------|-------------|
| `ip route add 10.0.0.0/24 via 192.168.1.1` | Add route |
| `ip route del 10.0.0.0/24` | Delete route |
| `ip route add default via 192.168.1.1` | Add default gateway |
| `route add -net 10.0.0.0/24 gw 192.168.1.1` | Add route (legacy) |

### Default Gateway

| Command | Description |
|---------|-------------|
| `ip route show default` | Show default gateway |
| `ip route add default via 192.168.1.1` | Set default gateway |
| `ip route del default` | Remove default gateway |

### Routing Examples

| Task | Command |
|------|---------|
| Show routing table | `ip route` |
| Show default gateway | `ip route | grep default` |
| Add static route | `sudo ip route add 10.0.0.0/24 via 192.168.1.254` |
| Delete route | `sudo ip route del 10.0.0.0/24` |
| Add default gateway | `sudo ip route add default via 192.168.1.1` |
| Show route to host | `ip route get 8.8.8.8` |

---

## Network Testing

### Connectivity Testing

| Command | Description | Use Case |
|---------|-------------|----------|
| `ping host` | Test connectivity | Basic reachability |
| `ping -c 4 host` | Send 4 packets | Limited test |
| `ping6 host` | IPv6 ping | IPv6 connectivity |
| `traceroute host` | Trace route | Find network path |
| `tracepath host` | Trace path (no root) | Similar to traceroute |
| `mtr host` | Network diagnostic | Continuous trace |

### Speed and Performance

| Command | Description |
|---------|-------------|
| `ping -c 100 host` | Test packet loss |
| `ping -i 0.2 host` | Fast ping (5 per second) |
| `iperf3 -c server` | Bandwidth test |
| `speedtest-cli` | Internet speed test |

### Network Tools

| Command | Description |
|---------|-------------|
| `telnet host port` | Test TCP connection |
| `nc -zv host port` | Port scan with netcat |
| `curl -I https://example.com` | Test HTTP/HTTPS |
| `wget --spider https://example.com` | Test URL availability |

### Testing Examples

| Task | Command |
|------|---------|
| Test connectivity | `ping google.com` |
| Send 10 pings | `ping -c 10 8.8.8.8` |
| Trace route | `traceroute google.com` |
| Continuous trace | `mtr google.com` |
| Test port 80 | `nc -zv example.com 80` |
| Test HTTPS | `curl -I https://google.com` |
| Speed test | `speedtest-cli` |

---

## Port and Services

### Viewing Open Ports

| Command | Description |
|---------|-------------|
| `ss -tuln` | All TCP/UDP listening ports |
| `ss -tulnp` | With process names |
| `netstat -tuln` | Listening ports (legacy) |
| `netstat -tulnp` | With process (legacy) |
| `lsof -i` | All network connections |
| `lsof -i :80` | What's using port 80 |

### ss Command Options

| Option | Description |
|--------|-------------|
| `-t` | TCP sockets |
| `-u` | UDP sockets |
| `-l` | Listening sockets |
| `-n` | Numeric (don't resolve names) |
| `-p` | Show processes |
| `-a` | All sockets |
| `-s` | Summary statistics |

### Port States

| State | Description |
|-------|-------------|
| **LISTEN** | Waiting for connections |
| **ESTABLISHED** | Active connection |
| **TIME_WAIT** | Closed, waiting for packets |
| **CLOSE_WAIT** | Waiting for close |
| **FIN_WAIT** | Connection closing |
| **SYN_SENT** | Connection attempt |

### Checking Specific Ports

| Task | Command |
|------|---------|
| All listening ports | `ss -tuln` |
| TCP only | `ss -tln` |
| UDP only | `ss -uln` |
| With process names | `sudo ss -tulnp` |
| Specific port | `ss -tuln | grep :80` |
| What's on port 22 | `sudo lsof -i :22` |
| All connections | `ss -tun` |

### Port Scanning

| Command | Description |
|---------|-------------|
| `nmap localhost` | Scan local ports |
| `nmap 192.168.1.1` | Scan remote host |
| `nmap -p 80,443 host` | Scan specific ports |
| `nmap -p 1-1000 host` | Scan port range |
| `nc -zv host 1-1000` | Port scan with netcat |

---

## Network Statistics

### Connection Statistics

| Command | Description |
|---------|-------------|
| `ss -s` | Socket statistics summary |
| `netstat -s` | Network statistics |
| `ss -tun` | All active connections |
| `ss -tn state established` | Established TCP connections |
| `netstat -i` | Interface statistics |

### Bandwidth Monitoring

| Command | Description |
|---------|-------------|
| `iftop` | Real-time bandwidth |
| `nethogs` | Per-process bandwidth |
| `vnstat` | Network statistics |
| `nload` | Network load |
| `bmon` | Bandwidth monitor |
| `iptraf-ng` | IP traffic monitor |

### Traffic Statistics

| Command | Description |
|---------|-------------|
| `ip -s link` | Interface statistics |
| `ifconfig eth0` | Interface stats (legacy) |
| `cat /proc/net/dev` | Network device stats |
| `ethtool -S eth0` | Detailed NIC stats |

### Statistics Examples

| Task | Command |
|------|---------|
| Connection summary | `ss -s` |
| Active connections | `ss -tun` |
| Established only | `ss -tn state established` |
| Interface stats | `ip -s link show eth0` |
| Real-time bandwidth | `iftop -i eth0` |
| Per-process network | `sudo nethogs eth0` |

---

## Firewall

### UFW (Uncomplicated Firewall)

| Command | Description |
|---------|-------------|
| `ufw status` | Check firewall status |
| `ufw enable` | Enable firewall |
| `ufw disable` | Disable firewall |
| `ufw allow 22` | Allow port 22 |
| `ufw deny 80` | Deny port 80 |
| `ufw allow ssh` | Allow SSH service |
| `ufw delete allow 80` | Remove rule |
| `ufw reset` | Reset to defaults |

### UFW Advanced Rules

| Command | Description |
|---------|-------------|
| `ufw allow 80/tcp` | Allow TCP port 80 |
| `ufw allow from 192.168.1.0/24` | Allow subnet |
| `ufw allow from 192.168.1.100 to any port 22` | Allow IP to port |
| `ufw deny from 10.0.0.0/8` | Deny subnet |
| `ufw limit ssh` | Rate limit SSH |

### iptables (Advanced Firewall)

| Command | Description |
|---------|-------------|
| `iptables -L` | List all rules |
| `iptables -L -n` | List (numeric, no DNS) |
| `iptables -F` | Flush all rules |
| `iptables -A INPUT -p tcp --dport 80 -j ACCEPT` | Allow port 80 |
| `iptables -A INPUT -j DROP` | Drop all input |

### firewall-cmd (RHEL/CentOS)

| Command | Description |
|---------|-------------|
| `firewall-cmd --state` | Check status |
| `firewall-cmd --list-all` | List all rules |
| `firewall-cmd --add-port=80/tcp` | Allow port (temporary) |
| `firewall-cmd --add-port=80/tcp --permanent` | Allow port (permanent) |
| `firewall-cmd --reload` | Reload rules |

### Firewall Examples

| Task | Command |
|------|---------|
| Check UFW status | `sudo ufw status` |
| Enable firewall | `sudo ufw enable` |
| Allow SSH | `sudo ufw allow 22` |
| Allow HTTP/HTTPS | `sudo ufw allow 80/tcp && sudo ufw allow 443/tcp` |
| Allow from IP | `sudo ufw allow from 192.168.1.100` |
| Deny port | `sudo ufw deny 23` |
| List iptables rules | `sudo iptables -L -n` |

---

## Network Troubleshooting

### Troubleshooting Steps

| Step | Command | Check |
|------|---------|-------|
| 1. Check interface | `ip link show` | Interface UP? |
| 2. Check IP | `ip addr show` | IP assigned? |
| 3. Check gateway | `ip route` | Default gateway? |
| 4. Ping gateway | `ping -c 4 192.168.1.1` | Gateway reachable? |
| 5. Ping external | `ping -c 4 8.8.8.8` | Internet reachable? |
| 6. Check DNS | `nslookup google.com` | DNS working? |
| 7. Check firewall | `sudo ufw status` | Firewall blocking? |

### Common Issues and Solutions

| Problem | Diagnosis | Solution |
|---------|-----------|----------|
| **No IP address** | `ip addr show` | `sudo dhclient eth0` |
| **Can't ping gateway** | `ping 192.168.1.1` | Check cable, switch |
| **DNS not working** | `nslookup google.com` | Fix `/etc/resolv.conf` |
| **Port not open** | `ss -tuln | grep :80` | Check service, firewall |
| **Slow connection** | `ping -c 100 gateway` | Check packet loss |
| **No default gateway** | `ip route` | `sudo ip route add default via X.X.X.X` |

### Diagnostic Commands

| Command | Purpose |
|---------|---------|
| `ip addr` | Check IP configuration |
| `ip route` | Check routing |
| `ping` | Test connectivity |
| `traceroute` | Find network path |
| `nslookup` | Test DNS |
| `ss -tuln` | Check listening ports |
| `journalctl -xe` | Check system logs |

### Network Debug Tools

| Tool | Purpose |
|------|---------|
| `tcpdump` | Packet capture |
| `wireshark` | Packet analysis (GUI) |
| `ethtool` | Ethernet driver info |
| `mtr` | Network diagnostics |
| `arp` | ARP table |

---

## Advanced Networking

### Packet Capture

| Command | Description |
|---------|-------------|
| `tcpdump -i eth0` | Capture on eth0 |
| `tcpdump -i eth0 port 80` | Capture port 80 |
| `tcpdump -i eth0 -w capture.pcap` | Save to file |
| `tcpdump -i eth0 host 192.168.1.100` | Capture specific host |
| `tcpdump -i eth0 -c 100` | Capture 100 packets |

### ARP Commands

| Command | Description |
|---------|-------------|
| `arp -a` | Show ARP table |
| `ip neigh` | Show neighbor table |
| `arp -d IP` | Delete ARP entry |
| `ip neigh flush all` | Clear neighbor cache |

### Network Bonding/Teaming

| Concept | Description |
|---------|-------------|
| **Bonding** | Combine multiple NICs |
| **Team** | Modern alternative to bonding |
| **Modes** | Active-backup, load balance, etc. |

### VLAN Configuration

| Command | Description |
|---------|-------------|
| `ip link add link eth0 name eth0.10 type vlan id 10` | Create VLAN |
| `ip addr add 192.168.10.1/24 dev eth0.10` | Assign IP to VLAN |
| `ip link set eth0.10 up` | Bring VLAN up |

### Bridge Configuration

| Command | Description |
|---------|-------------|
| `ip link add br0 type bridge` | Create bridge |
| `ip link set eth0 master br0` | Add interface to bridge |
| `ip link set br0 up` | Bring bridge up |

---

## Practical Examples

### Example 1: Basic Network Setup

| Step | Command | Purpose |
|------|---------|---------|
| 1. Check interface | `ip link show` | Find interface name |
| 2. Bring up interface | `sudo ip link set eth0 up` | Activate interface |
| 3. Get DHCP | `sudo dhclient eth0` | Get IP address |
| 4. Verify IP | `ip addr show eth0` | Confirm IP |
| 5. Test gateway | `ping -c 4 192.168.1.1` | Test connectivity |
| 6. Test internet | `ping -c 4 google.com` | Test DNS and internet |

### Example 2: Configure Static IP

| Step | Command | Purpose |
|------|---------|---------|
| 1. Edit config | `sudo nano /etc/netplan/01-network.yaml` | Open config file |
| 2. Add config | (See YAML example above) | Set static IP |
| 3. Apply changes | `sudo netplan apply` | Activate config |
| 4. Verify | `ip addr show` | Check IP |

### Example 3: Troubleshoot No Internet

| Step | Command | Check |
|------|---------|-------|
| 1. Check interface | `ip link show` | UP status? |
| 2. Check IP | `ip addr show` | Has IP? |
| 3. Check gateway | `ip route` | Default gateway? |
| 4. Ping gateway | `ping -c 4 192.168.1.1` | Can reach gateway? |
| 5. Ping DNS | `ping -c 4 8.8.8.8` | Can reach internet? |
| 6. Test DNS | `nslookup google.com` | DNS resolving? |
| 7. Check DNS config | `cat /etc/resolv.conf` | DNS servers listed? |

### Example 4: Find What's Using Port

| Step | Command | Purpose |
|------|---------|---------|
| 1. Check port | `sudo ss -tulnp | grep :80` | Find process on port 80 |
| 2. Get PID | Note PID from output | Identify process |
| 3. Process details | `ps -p PID` | See process info |
| 4. Kill if needed | `sudo kill PID` | Stop process |

### Example 5: Test Network Speed

| Step | Command | Purpose |
|------|---------|---------|
| 1. Install tool | `sudo apt install speedtest-cli` | Get speed test tool |
| 2. Run test | `speedtest-cli` | Test speed |
| 3. Detailed test | `speedtest-cli --simple` | Simple output |

### Example 6: Setup Firewall

| Step | Command | Purpose |
|------|---------|---------|
| 1. Enable UFW | `sudo ufw enable` | Activate firewall |
| 2. Allow SSH | `sudo ufw allow 22` | Keep SSH access |
| 3. Allow HTTP | `sudo ufw allow 80` | Allow web traffic |
| 4. Allow HTTPS | `sudo ufw allow 443` | Allow secure web |
| 5. Check status | `sudo ufw status` | Verify rules |

### Example 7: Diagnose Slow Connection

| Step | Command | Purpose |
|------|---------|---------|
| 1. Ping test | `ping -c 100 gateway` | Check packet loss |
| 2. Check latency | `ping -c 10 8.8.8.8` | Measure latency |
| 3. Trace route | `mtr google.com` | Find slow hop |
| 4. Check bandwidth | `iftop -i eth0` | Monitor traffic |
| 5. Check errors | `ip -s link show eth0` | Check for errors |

### Example 8: Capture Network Traffic

| Step | Command | Purpose |
|------|---------|---------|
| 1. Start capture | `sudo tcpdump -i eth0 -w capture.pcap` | Capture packets |
| 2. Reproduce issue | (Perform action) | Generate traffic |
| 3. Stop capture | `Ctrl+C` | Stop capturing |
| 4. Analyze | `tcpdump -r capture.pcap` | Read capture |

---

## Quick Reference

### Essential Networking Commands

| Task | Command |
|------|---------|
| Show IP addresses | `ip addr` |
| Show routing table | `ip route` |
| Test connectivity | `ping google.com` |
| DNS lookup | `nslookup google.com` |
| Show open ports | `ss -tuln` |
| Check firewall | `sudo ufw status` |
| Show interfaces | `ip link show` |
| Get DHCP | `sudo dhclient eth0` |

### Quick Network Check

| Command | What to Check |
|---------|---------------|
| `ip link show` | Interface UP? |
| `ip addr show` | IP assigned? |
| `ip route` | Default gateway? |
| `ping 8.8.8.8` | Internet reachable? |
| `nslookup google.com` | DNS working? |

---

## Best Practices

| Practice | Description |
|----------|-------------|
| **Use static IPs for servers** | Prevent IP changes |
| **Document network config** | Keep records of settings |
| **Test before permanent changes** | Verify temporary configs work |
| **Keep firewall enabled** | Security first |
| **Monitor bandwidth** | Track usage patterns |
| **Regular connectivity tests** | Prevent issues |
| **Use VLANs** | Segment network traffic |

