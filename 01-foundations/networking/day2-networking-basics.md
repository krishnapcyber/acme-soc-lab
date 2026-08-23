# Day 2 — Networking Fundamentals

## Objective

The objective of Day 2 is to understand fundamental networking
concepts and Linux networking commands required for cybersecurity
operations.

Topics covered:

- Network interfaces
- IP addresses
- Subnets and CIDR
- MAC addresses
- Loopback
- Default gateway
- Routing
- ARP / neighbor discovery
- DNS
- TCP
- UDP
- Ports
- Listening services
- HTTP / HTTPS
- Basic network troubleshooting

---

## 1. Network Interfaces

A network interface allows a computer to communicate with a network.

### Command

```bash
ip addr
```

### Purpose

The `ip addr` command displays network interfaces, their status, IP
addresses, and network prefixes.

### What I Learned

I used `ip addr` to identify the network interfaces available on my
Kali Linux system.

My active interface:

`[eth0:]`

My IP address:

`[REDACTED - LOCAL LAB]`

### Security Relevance

Network interface information is useful for:

- Network troubleshooting
- Host identification
- Incident investigation
- Network configuration analysis

---

## 2. Loopback Interface

The loopback interface allows a computer to communicate with itself
through the local networking stack.

The standard IPv4 loopback address is:

127.0.0.1

### Command

```bash
ping -c 4 127.0.0.1
```

### Purpose

This tests communication with the local machine.

### What I Learned

A successful loopback test confirms that the local networking stack
can respond to traffic directed to localhost.

### Security Relevance

Loopback communication is important because applications can
communicate locally without sending traffic to another host.

---

## 3. IP Address

An IP address is a logical address used to identify a host on an IP
network.

Example:

192.168.1.10


### Command

```bash
ip addr
```

### What I Learned

I used `ip addr` to identify the IP address assigned to my Kali Linux
network interface.

My lab IP:

`[REDACTED - LOCAL LAB]`

### Security Relevance

IP addresses are commonly used by SOC analysts to identify:

- Source systems
- Destination systems
- Internal hosts
- External hosts
- Suspicious network connections

---

## 4. Private IP Addresses

Private IPv4 address ranges commonly used inside internal networks
include:


10.0.0.0/8
172.16.0.0/12
192.168.0.0/16


### What I Learned

Private IP addresses are commonly used in:

- Home networks
- Corporate networks
- Virtual machines
- Internal servers
- Cloud environments

### Security Relevance

Security analysts need to distinguish between internal private
addresses and public Internet-routable addresses.

---

## 5. Subnets and CIDR

A subnet defines a logical range of IP addresses.

CIDR notation represents the network prefix.

Example:192.168.1.0/24


The `/24` indicates that 24 bits represent the network portion of the
address.

### What I Learned

A `/24` IPv4 network contains:

2^8 = 256


total addresses.

Subnetting allows organizations to divide networks into smaller
logical segments.

### Security Relevance

Subnet knowledge helps analysts understand:

- Network boundaries
- Network segmentation
- Incident scope
- Which hosts may communicate directly

---

## 6. MAC Address

A MAC address is a link-layer address associated with a network
interface.

Example:
AA:BB:CC:DD:EE:FF



### Command

```bash
ip link
```

### Purpose

Displays network interface and link-layer information.

### What I Learned

I used `ip link` to identify the MAC address associated with my
network interface.

My lab MAC address:

`[REDACTED - LOCAL LAB]`

### IP vs MAC

**IP address:** Logical network address

**MAC address:** Link-layer interface address

### Security Relevance

MAC addresses are useful when investigating local network
communication and ARP activity.

---

## 7. Default Gateway

A default gateway is the device used to forward traffic when the
destination is outside the local network.

### Command

```bash
ip route
```

### What I Learned

I used `ip route` to identify the default gateway configured on my
Kali Linux system.

My lab gateway:

`[REDACTED - LOCAL LAB]`

### Security Relevance

Gateway information can help analysts understand:

- Network connectivity
- Outbound traffic
- Network segmentation
- Routing behavior

---

## 8. Routing

Routing determines where network traffic should be sent.

### Command

```bash
ip route
```

### Example

192.168.1.0/24 dev eth0
default via 192.168.1.1


### What I Learned

The routing table contains routes for directly connected networks and
a default route for destinations without a more specific route.

### Security Relevance

Routing information helps analysts understand:

- Network paths
- Internal traffic
- External traffic
- Network segmentation
- Possible attack paths

---

## 9. ARP / Neighbor Discovery

ARP stands for Address Resolution Protocol.

On IPv4 local networks, ARP helps determine the MAC address
associated with an IP address.

Conceptually:

IP Address
|
v
ARP
|
v
MAC Address


### Command

```bash
ip neigh
```

### Purpose

Displays known network neighbors and their link-layer addresses.

### What I Learned

I used `ip neigh` to examine information about neighboring network
devices known to my system.

### Security Relevance

ARP is important when investigating:

- Local network communication
- ARP spoofing
- Man-in-the-middle attacks
- Local network reconnaissance

---

## 10. DNS

DNS stands for Domain Name System.

DNS translates domain names into IP addresses and provides other DNS
information.

Example:

example.com
|
v
DNS
|
v
IP Address


### Command

```bash
cat /etc/resolv.conf
```

### Purpose

Displays DNS resolver configuration.

### What I Learned

DNS allows systems to use human-readable domain names instead of
requiring users to remember IP addresses.

### Security Relevance

SOC analysts investigate DNS activity to identify:

- Suspicious domains
- Malware communication
- Command-and-control activity
- Phishing domains
- DNS tunneling
- Unusual DNS queries

---

## 11. DNS Lookup

### Command

```bash
dig example.com
```

Alternative:

```bash
nslookup example.com
```

### Purpose

Performs a DNS query for a domain.

### What I Learned

The system sends a DNS query and receives DNS information from the
configured resolver.

### Security Relevance

DNS queries can provide valuable evidence during malware, phishing,
and incident investigations.

---

## 12. TCP

TCP stands for Transmission Control Protocol.

TCP is a connection-oriented transport protocol.

### TCP Three-Way Handshake
### Command

```bash
cat /etc/resolv.conf
```

### Purpose

Displays DNS resolver configuration.

### What I Learned

DNS allows systems to use human-readable domain names instead of
requiring users to remember IP addresses.

### Security Relevance

SOC analysts investigate DNS activity to identify:

- Suspicious domains
- Malware communication
- Command-and-control activity
- Phishing domains
- DNS tunneling
- Unusual DNS queries

---

## 11. DNS Lookup

### Command

```bash
dig example.com
```

Alternative:

```bash
nslookup example.com
```

### Purpose

Performs a DNS query for a domain.

### What I Learned

The system sends a DNS query and receives DNS information from the
configured resolver.

### Security Relevance

DNS queries can provide valuable evidence during malware, phishing,
and incident investigations.

---

## 12. TCP

TCP stands for Transmission Control Protocol.

TCP is a connection-oriented transport protocol.

### TCP Three-Way Handshake
### Command

```bash
cat /etc/resolv.conf
```

### Purpose

Displays DNS resolver configuration.

### What I Learned

DNS allows systems to use human-readable domain names instead of
requiring users to remember IP addresses.

### Security Relevance

SOC analysts investigate DNS activity to identify:

- Suspicious domains
- Malware communication
- Command-and-control activity
- Phishing domains
- DNS tunneling
- Unusual DNS queries

---

## 11. DNS Lookup

### Command

```bash
dig example.com
```

Alternative:

```bash
nslookup example.com
```

### Purpose

Performs a DNS query for a domain.

### What I Learned

The system sends a DNS query and receives DNS information from the
configured resolver.

### Security Relevance

DNS queries can provide valuable evidence during malware, phishing,
and incident investigations.

---

## 12. TCP

TCP stands for Transmission Control Protocol.

TCP is a connection-oriented transport protocol.

### TCP Three-Way Handshake


### Command

```bash
cat /etc/resolv.conf
```

### Purpose

Displays DNS resolver configuration.

### What I Learned

DNS allows systems to use human-readable domain names instead of
requiring users to remember IP addresses.

### Security Relevance

SOC analysts investigate DNS activity to identify:

- Suspicious domains
- Malware communication
- Command-and-control activity
- Phishing domains
- DNS tunneling
- Unusual DNS queries

---

## 11. DNS Lookup

### Command

```bash
dig example.com
```

Alternative:

```bash
nslookup example.com
```

### Purpose

Performs a DNS query for a domain.

### What I Learned

The system sends a DNS query and receives DNS information from the
configured resolver.

### Security Relevance

DNS queries can provide valuable evidence during malware, phishing,
and incident investigations.

---

## 12. TCP

TCP stands for Transmission Control Protocol.

TCP is a connection-oriented transport protocol.

### TCP Three-Way Handshake

Client Server

| ------- SYN --------> |
| <----- SYN/ACK -------|
| ------- ACK --------> |
| |
| Connection Established|


### What I Learned

TCP establishes a connection before normal data exchange and provides
mechanisms for reliable and ordered delivery.

### Security Relevance

SOC analysts frequently investigate TCP connections using:

- Source IP
- Destination IP
- Source port
- Destination port
- TCP flags
- Timestamp

---

## 13. UDP

UDP stands for User Datagram Protocol.

UDP is a connectionless transport protocol.

### Common Uses

- DNS
- DHCP
- Real-time applications
- Streaming applications

### What I Learned

UDP has lower protocol overhead than TCP but does not provide TCP's
built-in reliable and ordered delivery mechanisms.

### Security Relevance

UDP traffic can be investigated for:

- Suspicious network activity
- Network scanning
- DNS abuse
- Data exfiltration
- Unusual communication

---

## 14. TCP vs UDP

| Feature     | TCP                          | UDP                          |
|-------------|-------------------------------|-------------------------------|
| Connection  | Connection-oriented           | Connectionless                |
| Reliability | Reliable delivery mechanisms  | No built-in reliable delivery |
| Ordering    | Ordered delivery              | No built-in ordering          |
| Handshake   | TCP three-way handshake       | No TCP-style handshake        |
| Overhead    | Higher                        | Lower                         |

### Security Takeaway

Neither TCP nor UDP is automatically secure or insecure. Security
depends on the application, configuration, authentication,
encryption, and network controls.

---

## 15. Network Ports

A port identifies a service endpoint associated with network
communication.

Conceptually:

IP Address + Port
|
v
Network Service


### Common Ports

| Port | Common Service |
|------|-----------------|
| 22   | SSH             |
| 53   | DNS             |
| 80   | HTTP            |
| 443  | HTTPS           |
| 445  | SMB             |
| 3389 | RDP             |

These are common associations and should not be treated as guaranteed
service identification.

### Security Relevance

Open services contribute to the attack surface of a system.

An analyst may investigate whether an open service is:

- Expected
- Authorized
- Vulnerable
- Misconfigured
- Suspicious

---

## 16. Listening Services

### Command

```bash
ss -tuln
```

### Options

- `-t` TCP
- `-u` UDP
- `-l` Listening
- `-n` Numerical output

### Purpose

Displays listening TCP and UDP sockets.

### What I Learned

I used `ss -tuln` to identify services listening for network
connections on my Kali Linux system.

### Security Relevance

Unexpected listening services can increase the attack surface of a
host.

During an investigation, an analyst may ask:

- What service is listening?
- Is it expected?
- Which process owns it?
- Is it exposed?
- Is it vulnerable?

---

## 17. HTTP

HTTP stands for Hypertext Transfer Protocol.

HTTP is an application-layer protocol commonly used for web
communication.

Basic communication:

Client
|
| HTTP Request
v
Web Server
|
| HTTP Response
v
Client


### Security Relevance

HTTP traffic can be involved in:

- Phishing
- Malware delivery
- Web attacks
- Credential theft
- Command-and-control
- Data exfiltration

---

## 18. HTTPS

HTTPS is HTTP protected using TLS.

### Basic Flow
Client
|
| HTTPS
| TLS-protected communication
v
Web Server


### What I Learned

HTTPS protects HTTP communication using TLS when properly configured.

### Security Relevance

HTTPS is frequently investigated during:

- Phishing investigations
- Malware investigations
- Web security incidents
- Network monitoring
- Threat hunting

---

## 19. Testing HTTPS with curl

### Command

```bash
curl -I https://example.com
```

### Purpose

The `-I` option requests HTTP response headers.

### What I Learned

I used `curl` to communicate with a web server from the command line
and inspect its HTTP response headers.

### Security Relevance

Command-line HTTP testing is useful for:

- Troubleshooting
- Service verification
- Web security testing
- Understanding HTTP behavior

---

## 20. Network Troubleshooting

A basic network troubleshooting methodology is:

Check network interface
|
v
Check IP configuration
|
v
Check routing
|
v
Check gateway
|
v
Check DNS
|
v
Check application connectivity


### Step 1 — Check Interface

```bash
ip addr
```

### Step 2 — Check Routing

```bash
ip route
```

### Step 3 — Test Local Connectivity

```bash
ping -c 4 127.0.0.1
```

### Step 4 — Test Gateway

```bash
ping -c 4 <gateway>
```

The actual gateway is not included in this public repository.

### Step 5 — Test DNS

```bash
dig example.com
```

### Step 6 — Test Application Connectivity

```bash
curl -I https://example.com
```

### Security Takeaway

Network troubleshooting should be performed systematically from the
lower-level network configuration toward the application layer.

---

## 21. Commands Practiced

The following Linux commands were practiced during Day 2:

```bash
ip addr
ip link
ip route
ip neigh
ping -c 4 127.0.0.1
cat /etc/resolv.conf
dig example.com
nslookup example.com
ss -tuln
curl -I https://example.com
```

---

## 22. SOC Investigation Perspective

The networking concepts learned today are directly relevant to SOC
operations.

A security alert may contain:

- Timestamp
- Source IP
- Source Port
- Destination IP
- Destination Port
- Protocol
- Hostname
- DNS Query
- URL
- Process
- User

A SOC analyst must understand these fields before deciding whether
network activity is normal or suspicious.

A simplified investigation can be:

Suspicious Alert
|
v
Identify Source Host
|
v
Identify Destination
|
v
Identify Port
|
v
Identify Protocol
|
v
Investigate DNS
|
v
Identify Process
|
v
Determine Whether Activity Is Legitimate


---

## 23. Security and Privacy

This project is stored in a public GitHub repository.

The following information must never be committed:

- Passwords
- API keys
- Access tokens
- Private SSH keys
- VPN credentials
- Production credentials
- Customer information
- Confidential company information
- Sensitive infrastructure information

Real local network information is redacted.

Example:

IP Address: [REDACTED - LOCAL LAB]
MAC Address: [REDACTED - LOCAL LAB]
Default Gateway: [REDACTED - LOCAL LAB]


All cybersecurity testing will be performed only against systems that
I own or have explicit authorization to test.

---

## 24. Lessons Learned

During Day 2 I learned:

- Network interfaces provide network connectivity.
- IP addresses provide logical addressing.
- MAC addresses operate at the link layer.
- Subnets define logical network boundaries.
- CIDR represents network prefixes.
- Default gateways provide paths to other networks.
- Routing determines where traffic is sent.
- ARP helps map IPv4 addresses to MAC addresses on local networks.
- DNS translates domain names into IP addresses.
- TCP is connection-oriented.
- UDP is connectionless.
- Ports identify service endpoints.
- Listening services contribute to attack surface.
- HTTP is an application-layer protocol.
- HTTPS uses TLS to protect HTTP communication.
- Network troubleshooting should be systematic.
- Network knowledge is fundamental to SOC operations.
- Network information is critical during incident investigations.

---

## 25. Day 2 Outcome

After completing Day 2, I can use basic Linux networking commands to
inspect a host's network configuration.

I can identify and investigate:

- Network interfaces
- IP configuration
- MAC information
- Routes
- Default gateway
- Neighbor information
- DNS configuration
- Listening services
- Basic network connectivity

These concepts will be used throughout the remainder of the
cybersecurity lab.

---

## 26. Next Step

The next stage of the project will introduce network reconnaissance
and Nmap.

Topics will include:

- Passive reconnaissance
- Active reconnaissance
- Host discovery
- Port discovery
- Service discovery
- Nmap
- Scan interpretation
- Attack surface identification

All scanning activities will be performed only against authorized
systems inside the isolated cybersecurity lab.
