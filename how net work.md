From top to bottom:

```
Application
    ↓
HTTP / HTTPS / SSH / SMTP / DNS / FTP / NTP / IMAP / POP3
    ↓
TCP / UDP
    ↓
IP (IPv4 / IPv6)
    ↓
Ethernet / Wi-Fi
    ↓
Physical (copper, fiber, radio waves)
```

## Application Layer Protocols


<details> <summary>Expand</summary> <br> 
HTTP (HyperText Transfer Protocol)
- Web traffic

HTTP (HyperText Transfer Protocol Secure)
- HTTP + TLS encryption

SSH (Secure Shell)
- Remote login and command execution

SMTP (Simple Mail Transfer Protocol)
- Sending email

DNS (Domain Name System)
- Converts names to IPs

FTP (File Transfer Protocol)
- File uploads/downloads

NTP (Network Time Protocol)
- Clock synchronization

IMAP (Internet Message Access Protocol)
- Read email while keeping mail on server

POP3 (Post Office Protocol Version 3)
- Download email from server
</details>

## Transport Layer
<details> <summary>Expand</summary> <br>



TCP (Transmission Control Protocol)
- Reliable, ordered connections

UDP (User Datagram Protocol)
- Fast, connectionless packets

Examples:
- DNS often uses UDP
- Voice calls often use UDP
- SSH uses TCP
- HTTP uses TCP

</details>

## Internet Layer
<details> <summary>Expand</summary> <br>


IP
- Internet Protocol
- Addressing and routing packets

IPv4
- Internet Protocol Version 4

Examples:
- 192.168.1.1
- 8.8.8.8

IPv6
- Internet Protocol Version 6

Example:
- 2001:4860:4860::8888


Link Layer

Ethernet
- IEEE 802.3
- Wired networking

Wi-Fi
- IEEE 802.11
- Wireless networking


Physical Layer

Copper
- Electrical signals over cable

Examples:
- Cat5e
- Cat6
- Cat6A

Fiber
- Light through glass fiber

Examples:
- Single-mode fiber
- Multi-mode fiber

Radio Waves
- Wireless transmission

Examples:
- Wi-Fi
- Bluetooth
- Cellular

</details>

## Other Common Networking / Security Terms

<details> <summary>Expand</summary> <br>
  

ARP
- Address Resolution Protocol
- IP → MAC lookup

MAC
- Media Access Control
- Hardware address

Example:
- 00:11:22:33:44:55

DHCP
- Dynamic Host Configuration Protocol
- Automatically assigns IP addresses

NAT
- Network Address Translation
- Many devices share one public IP

VPN
- Virtual Private Network
- Encrypted tunnel

TLS
- Transport Layer Security
- Encryption used by HTTPS

SSL
- Secure Sockets Layer
- Old predecessor to TLS

ICMP
- Internet Control Message Protocol
- Used by ping

LAN
- Local Area Network

WAN
- Wide Area Network

VLAN
- Virtual Local Area Network

CIDR
- Classless Inter-Domain Routing

Example:
- 192.168.1.0/24

BGP
- Border Gateway Protocol
- Internet routing between ISPs

ASN
- Autonomous System Number
- Identifier used by BGP

OSI
- Open Systems Interconnection
- The 7-layer networking model

MITM
- Man-In-The-Middle

DoS
- Denial of Service

DDoS
- Distributed Denial of Service

XSS
- Cross-Site Scripting

CSRF
- Cross-Site Request Forgery

SQLi
- SQL Injection
