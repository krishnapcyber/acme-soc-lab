cat > 02-network-recon-nmap/README.md << 'EOF'
# Network Reconnaissance & Nmap

## Objective

Perform host discovery, port scanning, and service enumeration
against an intentionally vulnerable target using Nmap, and interpret
results the way a SOC analyst or penetration tester would when
assessing attack surface.

## Lab Environment

- Attacker: Kali Linux
- Target: Metasploitable2 (deliberately vulnerable Linux VM)
- Network: Isolated Host-Only VirtualBox network (no internet exposure)

## 1. Host Discovery

Command:nmap -sn 192.168.x.0/24


Purpose: Identify live hosts on the subnet before scanning
individual targets, minimizing unnecessary traffic.

Result: [nmap -sn 192.168.x.0
Starting Nmap 7.99 ( https://nmap.org ) at 2026-08-24 00:13 -0400
Nmap scan report for 192.168.x.0
Host is up (0.00050s latency).
Nmap done: 1 IP address (1 host up) scanned in 0.58 seconds
]

## 2. Basic Port Scan

Command:nmap 192.168.x.x


Result: [nmap 192.168.x.x]     
Starting Nmap 7.99 ( https://nmap.org ) at 2026-08-24 00:11 -0400
Nmap scan report for 192.168.x.x
Host is up (0.0025s latency).
All 1000 scanned ports on 192.168.x.x are in ignored states.
Not shown: 1000 filtered tcp ports (no-response)

Nmap done: 1 IP address (1 host up) scanned in 59.20 seconds]

Findings: [list the open ports you found]

## 3. Service and Version Detection

Command:nmap -sV 192.168.x.x


Purpose: Identify not just open ports, but the specific service and
version running on each — critical for identifying known
vulnerabilities.

Result: [nmap -sV 192.168.x.x
Starting Nmap 7.99 ( https://nmap.org ) at 2026-08-24 00:20 -0400
Nmap scan report for 192.168.x.x
Host is up (0.0018s latency).
Not shown: 977 filtered tcp ports (no-response)
PORT     STATE SERVICE      VERSION
21/tcp   open  ftp          vsftpd 2.3.4
22/tcp   open  ssh          OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)
23/tcp   open  telnet       Linux telnetd
25/tcp   open  smtp         Postfix smtpd
53/tcp   open  domain       ISC BIND 9.4.2
80/tcp   open  http         Apache httpd 2.2.8 ((Ubuntu) DAV/2)
111/tcp  open  rpcbind      2 (RPC #100000)
139/tcp  open  netbios-ssn  Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn  Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
512/tcp  open  exec         netkit-rsh rexecd
513/tcp  open  login?
514/tcp  open  shell?
1099/tcp open  java-rmi     GNU Classpath grmiregistry
1524/tcp open  bindshell    Metasploitable root shell
2049/tcp open  nfs          2-4 (RPC #100003)
2121/tcp open  ccproxy-ftp?
3306/tcp open  mysql?
5432/tcp open  postgresql   PostgreSQL DB 8.3.0 - 8.3.7
5900/tcp open  vnc          VNC (protocol 3.3)
6000/tcp open  X11          (access denied)
6667/tcp open  irc          UnrealIRCd
8009/tcp open  ajp13        Apache Jserv (Protocol v1.3)
8180/tcp open  http         Apache Tomcat/Coyote JSP engine 1.1
Service Info: Hosts:  metasploitable.localdomain, irc.Metasploitable.LAN; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 179.95 seconds
]

Findings: [e.g. "vsftpd 2.3.4 detected on port 21 — this version has
a known backdoor vulnerability (CVE-2011-2523)"]

## 4. Aggressive Scan (OS Detection + Scripts)

Command:nmap -A 192.168.x.x


Result: [nmap -A 192.168.x.x
Starting Nmap 7.99 ( https://nmap.org ) at 2026-08-24 00:20 -0400
Nmap scan report for 192.168.x.x
Host is up (0.00075s latency).
Not shown: 977 filtered tcp ports (no-response)
PORT     STATE SERVICE      VERSION
21/tcp   open  ftp          vsftpd 2.3.4
|_ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_ftp-bounce: bounce working!
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to 192.168.x.1
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      vsFTPd 2.3.4 - secure, fast, stable
|_End of status
22/tcp   open  ssh          OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)
| ssh-hostkey: 
|   1024 60:0f:cf:e1:c0:5f:6a:74:d6:90:24:fa:c4:d5:6c:cd (DSA)
|_  2048 56:56:24:0f:21:1d:de:a7:2b:ae:61:b1:24:3d:e8:f3 (RSA)
23/tcp   open  telnet       Linux telnetd
25/tcp   open  smtp         Postfix smtpd
|_smtp-commands: metasploitable.localdomain, PIPELINING, SIZE 10240000, VRFY, ETRN, STARTTLS, ENHANCEDSTATUSCODES, 8BITMIME, DSN
53/tcp   open  domain       ISC BIND 9.4.2
| dns-nsid: 
|_  bind.version: 9.4.2
80/tcp   open  http         Apache httpd 2.2.8 ((Ubuntu) DAV/2)
|_http-server-header: Apache/2.2.8 (Ubuntu) DAV/2
|_http-title: Metasploitable2 - Linux
111/tcp  open  rpcbind      2 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2            111/tcp   rpcbind
|   100000  2            111/udp   rpcbind
|   100003  2,3,4       2049/tcp   nfs
|   100003  2,3,4       2049/udp   nfs
|   100005  1,2,3      42583/tcp   mountd
|   100005  1,2,3      48669/udp   mountd
|   100021  1,3,4      40720/udp   nlockmgr
|   100021  1,3,4      45603/tcp   nlockmgr
|   100024  1          50043/tcp   status
|_  100024  1          56068/udp   status
139/tcp  open  netbios-ssn  Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn  Samba smbd 3.0.20-Debian (workgroup: WORKGROUP)
512/tcp  open  exec         netkit-rsh rexecd
513/tcp  open  login?
514/tcp  open  shell?
1099/tcp open  java-rmi     GNU Classpath grmiregistry
1524/tcp open  bindshell    Metasploitable root shell
2049/tcp open  nfs          2-4 (RPC #100003)
2121/tcp open  ccproxy-ftp?
3306/tcp open  mysql?
5432/tcp open  postgresql   PostgreSQL DB 8.3.0 - 8.3.7
|_ssl-date: 2026-08-24T04:25:00+00:00; +18s from scanner time.
| ssl-cert: Subject: commonName=ubuntu804-base.localdomain/organizationName=OCOSA/stateOrProvinceName=There is no such thing outside US/countryName=XX
| Not valid before: 2010-03-17T14:07:45
|_Not valid after:  2010-04-16T14:07:45
5900/tcp open  vnc          VNC (protocol 3.3)
| vnc-info: 
|   Protocol version: 3.3
|   Security types: 
|_    VNC Authentication (2)
6000/tcp open  X11          (access denied)
6667/tcp open  irc          UnrealIRCd (Admin email admin@Metasploitable.LAN)
8009/tcp open  ajp13        Apache Jserv (Protocol v1.3)
|_ajp-methods: Failed to get a valid response for the OPTION request
8180/tcp open  http         Apache Tomcat/Coyote JSP engine 1.1
|_http-title: Apache Tomcat/5.5
|_http-favicon: Apache Tomcat
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: WAP|general purpose
Running: Actiontec embedded, Linux 2.4.X
OS CPE: cpe:/h:actiontec:mi424wr-gen3i cpe:/o:linux:linux_kernel cpe:/o:linux:linux_kernel:2.4.37
OS details: Actiontec MI424WR-GEN3I WAP, DD-WRT v24-sp2 (Linux 2.4.37)
Network Distance: 2 hops
Service Info: Host:  metasploitable.localdomain; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_clock-skew: mean: 1h20m17s, deviation: 2h18m33s, median: 17s
| smb-security-mode: 
|   account_used: <blank>
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
|_nbstat: NetBIOS name: METASPLOITABLE, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb-os-discovery: 
|   OS: Unix (Samba 3.0.20-Debian)
|   Computer name: metasploitable
|   NetBIOS computer name: 
|   Domain name: localdomain
|   FQDN: metasploitable.localdomain
|_  System time: 2026-08-24T00:23:54-04:00
|_smb2-time: Protocol negotiation failed (SMB2)

TRACEROUTE (using port 80/tcp)
HOP RTT     ADDRESS
1   0.12 ms 192.168.x.x
2   0.15 ms 192.168.x.x

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 275.49 seconds
                                 ]

## 5. Full Port Range Scan

Command: nmap -p- 192.168.x.x


Purpose: The default Nmap scan only checks the top 1000 ports.
Scanning all 65535 ports can reveal services running on non-standard
ports that a default scan would miss.

Result: [paste output]

## Security Analysis


## Security Analysis

**vsftpd 2.3.4 (Port 21 - FTP):** This is a known-backdoored version
of vsftpd. A malicious build of this version was distributed publicly
containing a backdoor (CVE-2011-2523) that opens a remote root shell
on port 6200 when a specific string is sent during login. Combined
with anonymous FTP login being enabled, this is one of the most
severe findings on the host - an attacker needs no credentials at
all to gain a foothold. A SOC analyst would flag this as critical
and recommend immediate removal or upgrade of the FTP service.

**Port 1524 (bindshell):** Nmap explicitly identifies this as
"Metasploitable root shell" - meaning a root-level command shell is
listening on this port with no authentication whatsoever. An
attacker who finds this port open can connect directly and execute
commands as root, no exploitation required. This would be treated as
an active compromise indicator in a real environment, not just a
misconfiguration.

**UnrealIRCd (Port 6667):** This build is associated with a
well-documented backdoor (CVE-2010-2075) baked directly into the
distributed binary, allowing remote command execution via a specific
trigger string sent to the IRC service. Because the backdoor is in
the software itself rather than a separate vulnerability to exploit,
a defender finding this would isolate the host immediately rather
than attempt to patch it.

**Legacy cleartext services (telnet, rexec, rlogin, rsh - ports 23,
512-514):** These protocols transmit credentials and data in plain
text with no encryption. An attacker positioned to observe network
traffic (e.g. via ARP spoofing on the local segment) could capture
login credentials directly. A defender would flag any of these
services as immediate remediation candidates in favor of SSH.

**SMB message signing disabled (ports 139/445):** With message
signing disabled, SMB traffic is more susceptible to
man-in-the-middle relay attacks. A defender would enable and enforce
SMB signing as a standard hardening step.

## Lessons Learned

1. Scan type matters more than I expected: the default unprivileged
   `nmap` scan reported all ports as filtered on this host, while
   `-sV` and `-A` (which I ran with elevated privileges) revealed 23
   open ports with full service detail on the same target. This
   showed me firsthand that scan technique and privilege level
   directly affect what you see - an unprivileged TCP connect scan
   behaves differently than the SYN-based scans used by `-sV`/`-A`,
   and relying on a single scan type could cause an analyst to
   completely miss a host's real attack surface.
2. I was surprised by how much a single default installation exposes
   - 23 open ports on one host, several with services that
   effectively hand over a root shell (port 1524, the UnrealIRCd
   backdoor) with zero exploitation effort required. It reframed for
   me how much attack surface reduction (disabling unused services)
   matters as a control, not just patching.
3. More thorough scans (`-A`, `-p-`) take significantly longer
   (nearly 5 minutes vs under a second for host discovery) and
   generate far more traffic/log noise. In a real engagement or
   red-team exercise, that's a real tradeoff - a noisy full scan is
   more likely to trip an IDS/SOC alert, so attackers (and
   penetration testers simulating them) have to balance thoroughness
   against staying undetected.

## Note on Lab Data

All scanning was performed only against a VM I own, on an isolated
host-only network with no exposure to the public internet or any
system I am not authorized to test.
EOF
echo "File written"

## Note on Lab Data

All scanning was performed only against a VM I own, on an isolated
host-only network with no exposure to the public internet or any
system I am not authorized to test.
EOF


