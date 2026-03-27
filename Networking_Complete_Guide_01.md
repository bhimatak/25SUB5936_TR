# 🌐 Computer Architecture — Networking


---

## 📋 Table of Contents

| Section | Topic | Day |
|---------|-------|-----|
| **Prerequisites** | Checklist & Tools | Before Day 1 |
| **2.0** | Understanding Computer Networking | Day 1 AM |
| **2.1** | Introduction to Networking | Day 1 PM – Day 2 AM |
| **2.2** | Network Models and Protocols | Day 2 PM – Day 3 |
| **Appendix A** | Glossary | Reference |
| **Appendix B** | Interview Questions | Reference |
| **Appendix C** | Quick Reference Cheat Sheet | Reference |
| **Appendix D** | Projects & Code Templates | Reference |
| **Appendix E** | Resources & Certifications | Reference |

---

**Tools to install (all free):**

| Tool | Purpose | Where |
|------|---------|-------|
| **Wireshark** | Capture and analyze network packets | wireshark.org |
| **nmap** | Network scanning and exploration | nmap.org |
| **curl** | Test HTTP/FTP requests from command line | Built-in on Mac/Linux |
| **ping/traceroute** | Test connectivity | Built-in on all OS |
| **Postman** | Test HTTP APIs visually | postman.com |

---

## ⚡ Quick Start — Your First 5 Minutes of Networking

Open a terminal and run these three commands. They demonstrate fundamental networking concepts we'll explore in depth:

```bash
# Command 1: Find your own IP address
# Windows:
ipconfig
# Mac/Linux:
ifconfig   # or: ip addr show

# Command 2: Test if you can reach Google's servers (ICMP protocol)
ping -c 4 google.com

# Command 3: Trace the path your data takes to reach Google
traceroute google.com   # Mac/Linux
tracert google.com      # Windows
```

What you just saw: IP addresses, packet transmission, and routing hops — the three foundational concepts of networking. By the end of Day 1, you'll understand exactly how every step works.

---

---

# ══════════════════════════════════════════════════════
# MODULE 2.0 — UNDERSTANDING COMPUTER NETWORKING
# ══════════════════════════════════════════════════════


---

## 📖 Introduction

Imagine you're trying to send a handwritten letter to someone across the city. You write the letter, put it in an envelope, address it, drop it at the post office, and the postal system routes it to the destination. A week later, they receive it and write back. Computer networking is the same idea, but instead of letters, we send data; instead of post offices, we have routers; and instead of weeks, it takes milliseconds.

A **computer network** is a collection of devices (computers, phones, servers, printers) connected together so they can share information and resources. Without networks, every computer would be an island. You couldn't send email, stream video, browse websites, or use cloud services. The internet itself is simply the world's largest computer network — a network of networks.

Networks are built on three fundamental things: **hardware** (the physical equipment), **software** (the programs that manage communication), and **protocols** (the agreed-upon rules that make everything work together). Understanding all three is the foundation of network engineering.

---

## 🏗️ Core Content

### 2.0.1 What Is a Network?

```
WHAT A NETWORK ACTUALLY IS:

  ┌──────────────────────────────────────────────────────────────────┐
  │                                                                  │
  │   Your Laptop ──────────┐                                       │
  │                         │                                       │
  │   Your Phone  ──────────┼──── Router ──── Internet ──── Server  │
  │                         │       │                              │
  │   Smart TV    ──────────┘       │                              │
  │                                 │                              │
  │   Printer ─────────────────────┘                              │
  │                                                                  │
  │   All connected → can share files, internet access, printing    │
  │   This is your HOME NETWORK (Local Area Network - LAN)         │
  └──────────────────────────────────────────────────────────────────┘

POSTAL SYSTEM ANALOGY:
  Letter/Package     = Data packet
  Envelope           = IP header (contains address info)
  Your address       = IP address
  Post office        = Router
  Postal routes      = Network routes
  Tracking number    = Sequence numbers (TCP)
  Return receipt     = Acknowledgment packets (TCP ACK)
```

### 2.0.2 Network Classification by Size

```
NETWORK SIZE CLASSIFICATION:

PAN — Personal Area Network
  Range: ~10 meters
  Examples: Bluetooth headphones, Apple Watch, keyboard
  ┌─────────────────────┐
  │  You  ◄──BT──►  Phone │ (personal bubble of devices)
  └─────────────────────┘

LAN — Local Area Network
  Range: Building or campus
  Examples: Home Wi-Fi, office network, school network
  ┌──────────────────────────────────────────┐
  │  Office Floor / Home                      │
  │  PC ──┐                                  │
  │       ├── Switch ── Router ── Internet    │
  │  PC ──┘                                  │
  └──────────────────────────────────────────┘

MAN — Metropolitan Area Network
  Range: City / large campus
  Examples: City-wide fiber, cable TV network
  [University Campus A] ── fiber ── [University Campus B]
  (same city, ~10–100 km range)

WAN — Wide Area Network
  Range: Country / worldwide
  Examples: The Internet, corporate VPN networks
  ┌────────┐            ┌────────┐
  │New York│── internet ──│London │
  └────────┘            └────────┘
  
INTERNET: A network of networks (WAN connecting all WANs!)
```

### 2.0.3 Network Hardware — The Physical Building Blocks

```
KEY NETWORK HARDWARE:

1. NETWORK INTERFACE CARD (NIC):
   ┌──────────────────────────────────────────────────────────┐
   │  The hardware that connects your device to the network   │
   │  Every device has a unique MAC address burned in at      │
   │  manufacture: e.g., AA:BB:CC:DD:EE:FF                   │
   │  Wi-Fi adapter = wireless NIC                           │
   └──────────────────────────────────────────────────────────┘

2. SWITCH (Layer 2 device):
   ┌──────────────────────────────────────────────────────────┐
   │  Connects devices within ONE network (LAN)               │
   │  Learns which device is on which port (MAC table)       │
   │  Sends data ONLY to the correct port (not broadcast)    │
   │                                                          │
   │  ┌────┐  ┌────────────────────────────────┐  ┌────┐    │
   │  │ PC1│──│         SWITCH                 │──│ PC2│    │
   │  └────┘  │  Port1 → MAC_PC1               │  └────┘    │
   │          │  Port2 → MAC_PC2               │            │
   │  ┌────┐  │  Port3 → MAC_PC3               │  ┌────┐    │
   │  │ PC3│──│                                │──│ PC4│    │
   │  └────┘  └────────────────────────────────┘  └────┘    │
   └──────────────────────────────────────────────────────────┘

3. ROUTER (Layer 3 device):
   ┌──────────────────────────────────────────────────────────┐
   │  Connects DIFFERENT networks together                    │
   │  Reads IP addresses to decide where to send packets     │
   │  Your home router: connects LAN to Internet              │
   │                                                          │
   │  [Home Network 192.168.1.x] ──ROUTER── [Internet]       │
   │                              │                           │
   │               Routes by IP address                       │
   └──────────────────────────────────────────────────────────┘

4. ACCESS POINT (AP):
   Extends network wirelessly; connects wireless devices to wired LAN

5. MODEM:
   Converts digital data (your network) ↔ analog signal (phone/cable line)
   "MOdulator-DEModulator"
   Your ISP provides this; sits between router and the internet

6. FIREWALL:
   Guards the network boundary; blocks unauthorized traffic
   Can be hardware (dedicated device) or software (Windows Firewall, iptables)
```

**Switch vs Router vs Hub — The Confusion Resolved:**

```
╔═══════════════╦══════════════════╦═══════════════════╦══════════════════╗
║ Device        ║ Works at Layer   ║ Reads             ║ Connects         ║
╠═══════════════╬══════════════════╬═══════════════════╬══════════════════╣
║ Hub (legacy)  ║ Layer 1          ║ Nothing (dumb!)   ║ Same network     ║
║               ║ Physical         ║ Broadcasts to ALL ║ (all same port)  ║
╠═══════════════╬══════════════════╬═══════════════════╬══════════════════╣
║ Switch        ║ Layer 2          ║ MAC addresses     ║ Same network     ║
║               ║ Data Link        ║ Sends to right port║ (smart!)        ║
╠═══════════════╬══════════════════╬═══════════════════╬══════════════════╣
║ Router        ║ Layer 3          ║ IP addresses      ║ Different        ║
║               ║ Network          ║ Routes between    ║ networks         ║
║               ║                  ║ networks          ║                  ║
╚═══════════════╩══════════════════╩═══════════════════╩══════════════════╝
```

### 2.0.4 Key Performance Metrics

```
NETWORK PERFORMANCE — THREE METRICS THAT MATTER:

1. BANDWIDTH:
   Maximum data rate the link CAN carry
   Think: width of a pipe
   Measured in: Mbps, Gbps
   
   1 Gbps Ethernet: ████████████████████████ (wide pipe)
   100 Mbps Wi-Fi: ██████                   (narrower)
   4G LTE:         ███                      (narrower still)
   
   Common confusion: Your ISP says "1 Gbps" = 1 Gbps maximum
   Real-world: often 60–80% due to protocol overhead

2. LATENCY (RTT — Round Trip Time):
   Time for data to travel from A to B and back
   Think: speed of the pipe
   Measured in: milliseconds (ms)
   
   Latency affects: Gaming, video calls, real-time systems
   
   ┌────────────────────────────────────────────────────────┐
   │ Typical Latencies:                                     │
   │  Your home router:          1–2 ms                     │
   │  Within a city:             5–10 ms                    │
   │  Coast to coast (USA):      ~70 ms                    │
   │  USA to Europe:             ~100 ms                   │
   │  USA to Australia:          ~200 ms                   │
   │  Geostationary satellite:   ~600 ms                   │
   │  LEO satellite (Starlink):  ~20–40 ms                │
   └────────────────────────────────────────────────────────┘

3. THROUGHPUT:
   Actual data rate achieved (≤ bandwidth)
   = What you ACTUALLY get vs what the pipe CAN carry
   
   BANDWIDTH 100 Mbps → THROUGHPUT might be 70 Mbps
   Reduced by: overhead, congestion, packet loss, protocol
   
   Real example: 
   Speedtest shows 500 Mbps download
   Downloading a file: actually achieves 450–480 Mbps
   (overhead from TCP headers, IP headers, Ethernet frames)
```

---

## 🔬 Hands-On Exercise 2.0

**Exercise A: Discover Your Network**

```bash
# Run these commands and record the results:

# 1. Your device's IP address
# Windows:   ipconfig /all
# Mac/Linux: ifconfig

# What to look for:
# - IPv4 Address: Your device's IP (e.g., 192.168.1.105)
# - Subnet Mask: Defines network boundary (e.g., 255.255.255.0)
# - Default Gateway: Your router's IP (e.g., 192.168.1.1)
# - MAC Address: Your NIC's unique ID (e.g., 00:1A:2B:3C:4D:5E)

# 2. Measure latency to Google
ping -c 5 8.8.8.8   # Mac/Linux (-n 5 on Windows)
# Record: min, avg, max latency

# 3. Trace the path to Google
traceroute 8.8.8.8   # Mac/Linux
tracert 8.8.8.8      # Windows
# Count how many hops (routers) between you and Google
```

**Expected findings:** 10–15 router hops to reach Google, latency 20–100ms depending on location.

---

## ⚠️ Common Mistakes — Module 2.0

| Mistake | Reality |
|---------|---------|
| "Bandwidth and speed are the same" | Bandwidth is capacity; latency is actual speed; throughput is actual data rate |
| "Switch and router are the same" | Switch operates within one network; router connects different networks |
| "My 1 Gbps router means 1 Gbps everywhere" | Router-to-ISP link is the bottleneck; Wi-Fi adds more overhead |
| "More bandwidth always fixes slow internet" | Often latency or server capacity is the real bottleneck |

---

# ══════════════════════════════════════════════════════
# MODULE 2.1 — INTRODUCTION TO NETWORKING
# ══════════════════════════════════════════════════════

## 🎯 Learning Objectives

After completing this section, you will be able to:
- Explain IP addressing (IPv4 and IPv6) and subnet masks
- Understand how DNS resolves domain names to IP addresses
- Describe routing protocols (OSPF, BGP) and how the internet routes packets
- Explain network topology designs and their trade-offs
- Understand cellular network architecture (4G LTE, 5G)
- Describe how networking enables cloud computing
- Explain emerging technologies: 5G, IoT, and future internet

---

## 📖 Introduction

The internet connects 5 billion people across 193 countries, yet data reliably finds its way from source to destination in milliseconds. This isn't magic — it's the result of elegant systems for addressing (how do we uniquely identify every device?), routing (how does data find its way?), and protocols (what language do devices speak?). Understanding these systems is the difference between treating the internet as a black box and understanding one of humanity's greatest engineering achievements.

Modern networking has evolved far beyond the simple "send and receive" model. Today's networks span cloud computing environments that elastically scale to millions of users, 5G networks delivering gigabit wireless, IoT networks connecting billions of sensors, and software-defined networks that can be reconfigured in software in milliseconds. The principles you learn here apply equally to a home Wi-Fi network and the most advanced data center infrastructure in the world.

---

## 🏗️ Core Content

### 2.1.1 Basic Networking Concepts — IP Addressing

**IPv4 Addressing:**

```
IPv4 ADDRESS ANATOMY:

  192  .  168  .   1   .  100
  ─────────────────────────────
  8 bits  8 bits  8 bits  8 bits  = 32 bits total
  
  Each 8-bit section: 0–255
  Total possible IPv4 addresses: 2^32 = ~4.3 billion

BINARY REPRESENTATION:
  192 = 11000000
  168 = 10101000
    1 = 00000001
  100 = 01100100
  
  Full address: 11000000.10101000.00000001.01100100

SPECIAL ADDRESS RANGES:
  ┌──────────────────────────────────────────────────────────────┐
  │ Private (not routable on internet):                          │
  │   10.0.0.0 – 10.255.255.255      (10/8)     — enterprises  │
  │   172.16.0.0 – 172.31.255.255    (172.16/12)— medium nets  │
  │   192.168.0.0 – 192.168.255.255  (192.168/16)— home/small  │
  │                                                              │
  │ Loopback (yourself):                                         │
  │   127.0.0.1 — "localhost" — talks to your own device        │
  │                                                              │
  │ Broadcast (all devices on subnet):                           │
  │   192.168.1.255 (last address in subnet)                    │
  │                                                              │
  │ APIPA (no DHCP server found):                                │
  │   169.254.x.x — self-assigned when DHCP fails               │
  └──────────────────────────────────────────────────────────────┘
```

**Subnet Masks — Dividing Networks:**

```
SUBNET MASK EXPLAINED:

Your IP:      192.168.1.100   (binary: 11000000.10101000.00000001.01100100)
Subnet mask:  255.255.255.0   (binary: 11111111.11111111.11111111.00000000)

1s in mask = NETWORK part (fixed for everyone in this network)
0s in mask = HOST part (unique per device)

Network:  192.168.1.x (everyone on this LAN shares this)
Host:     .100 (this specific device)
Range:    192.168.1.1 – 192.168.1.254 (usable hosts)
Broadcast:192.168.1.255

CIDR NOTATION (modern shorthand):
  255.255.255.0 = /24  (24 ones in subnet mask)
  255.255.0.0   = /16  (16 ones)
  255.0.0.0     = /8   (8 ones)
  
  192.168.1.100/24 = same as 192.168.1.100 with 255.255.255.0 mask
  
  /24 subnet: 2^8 - 2 = 254 usable hosts
  /16 subnet: 2^16 - 2 = 65,534 usable hosts
  /8  subnet: 2^24 - 2 = 16,777,214 usable hosts

SUBNETTING EXAMPLE (splitting /24 into four /26 subnets):
  Original: 192.168.1.0/24 (254 hosts)
  Split into:
  Subnet 1: 192.168.1.0/26   (hosts: .1 – .62,  62 hosts)
  Subnet 2: 192.168.1.64/26  (hosts: .65 – .126, 62 hosts)
  Subnet 3: 192.168.1.128/26 (hosts: .129 – .190, 62 hosts)
  Subnet 4: 192.168.1.192/26 (hosts: .193 – .254, 62 hosts)
```

**IPv6 — The Future of Addressing:**

```
IPv6 — WHY WE NEED IT AND HOW IT WORKS:

Problem: 4.3 billion IPv4 addresses are EXHAUSTED (ran out 2011!)
Solution: IPv6 — 128-bit addresses = 2^128 = 340 undecillion addresses
         = 340,000,000,000,000,000,000,000,000,000,000,000,000 addresses!
         = 670 quadrillion addresses per square millimeter of Earth's surface!

FORMAT:
  2001:0db8:85a3:0000:0000:8a2e:0370:7334
  └──┴──┴──┴──┘  ←16-bit groups, hex, separated by colons
  
  Shortening rules:
  • Leading zeros can be dropped: 0db8 → db8
  • One group of consecutive all-zero groups → ::
  
  Full:  2001:0db8:0000:0000:0000:0000:0000:0001
  Short: 2001:db8::1

TYPES:
  ::1              = Loopback (equivalent to IPv4 127.0.0.1)
  fe80::/10        = Link-local (self-assigned, non-routable)
  2001:db8::/32    = Documentation/examples
  2001::/32        = Teredo (IPv6 over IPv4 tunnel)
  ::/0             = Default route (all IPv6)
  
REAL EXAMPLE: Google's IPv6 address
  2607:f8b0:4004:c1b::65
  
KEY IMPROVEMENTS over IPv4:
  ✓ No more NAT needed (every device gets globally routable address)
  ✓ Built-in security (IPSec required, not optional)
  ✓ Better header (simpler, faster to process)
  ✓ Stateless autoconfiguration (SLAAC — no DHCP needed)
  ✓ No broadcast (replaced with multicast)
  ✓ Larger packet payloads (jumbograms)
```

**DHCP — Automatic Address Assignment:**

```
DHCP (Dynamic Host Configuration Protocol) — HOW IT WORKS:

When your laptop connects to Wi-Fi, it doesn't know its own IP.
DHCP gives it one automatically.

THE DORA PROCESS:
  
  Your Device          DHCP Server (your router)
      │                      │
      │── DISCOVER ─────────▶│  "Is there a DHCP server here?"
      │   (broadcast to all)  │  (I don't have an IP yet)
      │                      │
      │◀─ OFFER ─────────────│  "Yes! I offer you 192.168.1.105"
      │                      │  "Lease: 24 hours"
      │                      │  "Gateway: 192.168.1.1"
      │                      │  "DNS: 8.8.8.8"
      │                      │
      │── REQUEST ──────────▶│  "I accept 192.168.1.105!"
      │   (broadcast to all  │
      │    so other servers  │
      │    know)             │
      │                      │
      │◀─ ACK ───────────────│  "Confirmed. Lease active!"
      │                      │

After DORA: Your device has an IP, subnet mask, gateway, DNS
           All from those 4 messages in < 1 second!

DHCP LEASE:
  • Each IP assignment has a lease time (hours/days)
  • Device renews at 50% of lease time (T1)
  • Device tries another server at 87.5% (T2)
  • After expiry: device loses IP, must restart DORA
```

### 2.1.2 DNS — The Internet's Phone Book

```
DNS (Domain Name System) — TRANSLATING NAMES TO IPs:

PROBLEM: Humans remember "google.com"; computers need "142.250.80.100"
SOLUTION: DNS — a distributed database mapping names to IPs

THE DNS RESOLUTION PROCESS:
(When you type google.com in your browser)

  Browser                               DNS System
     │                                       │
     │── Check browser cache ─────────────── ? (cache miss)
     │── Check OS cache ────────────────────  ? (cache miss)
     │                                       │
     │── Query Local DNS Resolver ──────────▶│ (your ISP or 8.8.8.8)
     │                                       │── Query Root Server
     │                                       │   "Who handles .com?"
     │                                       │◀─ "TLD servers: a.gtld-servers.net"
     │                                       │── Query TLD Server (.com)
     │                                       │   "Who handles google.com?"
     │                                       │◀─ "google's NS: ns1.google.com"
     │                                       │── Query Authoritative DNS
     │                                       │   "What is google.com's IP?"
     │                                       │◀─ "google.com → 142.250.80.100"
     │◀── "google.com = 142.250.80.100" ─────│
     │                                       │
     (Whole process: ~10–50ms first time)
     (Cached: ~0ms, just reads local memory)

DNS RECORD TYPES:
  ┌──────┬─────────────────────────────────────────────────────────┐
  │ A    │ Maps hostname to IPv4 address                           │
  │      │ google.com → 142.250.80.100                             │
  ├──────┼─────────────────────────────────────────────────────────┤
  │ AAAA │ Maps hostname to IPv6 address                           │
  │      │ google.com → 2607:f8b0:4004:c1b::65                    │
  ├──────┼─────────────────────────────────────────────────────────┤
  │ CNAME│ Alias (one name points to another name)                 │
  │      │ www.example.com → example.com                          │
  ├──────┼─────────────────────────────────────────────────────────┤
  │ MX   │ Mail server (where to send email for this domain)       │
  │      │ example.com MX → mail.example.com                      │
  ├──────┼─────────────────────────────────────────────────────────┤
  │ NS   │ Nameservers (authoritative DNS for this domain)         │
  │      │ google.com NS → ns1.google.com                          │
  ├──────┼─────────────────────────────────────────────────────────┤
  │ TXT  │ Text record (SPF, DKIM, domain verification)            │
  │      │ Used for email authentication, ownership proof          │
  ├──────┼─────────────────────────────────────────────────────────┤
  │ PTR  │ Reverse lookup (IP → hostname)                          │
  │      │ 100.80.250.142.in-addr.arpa → google.com               │
  └──────┴─────────────────────────────────────────────────────────┘

PRACTICAL: Look up DNS records from command line:
  nslookup google.com              # basic lookup
  dig google.com A                 # detailed A record lookup
  dig google.com MX                # mail server records
  dig -x 8.8.8.8                  # reverse lookup (IP → name)
  dig @8.8.8.8 google.com         # query specific DNS server
```

### 2.1.3 Advanced Routing and Switching Concepts

**How Routing Works:**

```
ROUTING — HOW DATA FINDS ITS WAY ACROSS THE INTERNET:

Each router has a ROUTING TABLE — a map of where to send packets

Example Routing Table (simplified):
  ┌──────────────────┬─────────────┬──────────────────┬─────────┐
  │ Destination      │ Subnet Mask │ Next Hop         │ Interface│
  ├──────────────────┼─────────────┼──────────────────┼─────────┤
  │ 192.168.1.0      │ /24         │ Directly connected│ eth0   │
  │ 10.0.0.0         │ /8          │ 192.168.1.1      │ eth0    │
  │ 0.0.0.0          │ /0          │ 203.0.113.1      │ eth1    │
  │ (default route)  │             │ (ISP gateway)    │         │
  └──────────────────┴─────────────┴──────────────────┴─────────┘

HOW A ROUTER MAKES A DECISION:
  1. Receive packet with destination IP: 172.217.9.100
  2. Check routing table — longest prefix match:
     • Does it match 192.168.1.0/24? No (different range)
     • Does it match 10.0.0.0/8? No (different range)
     • Does it match 0.0.0.0/0? YES (default — matches everything)
  3. Forward to 203.0.113.1 (ISP) via eth1
  4. Repeat at each router until destination reached!

LONGEST PREFIX MATCH:
  If both 10.0.0.0/8 and 10.1.0.0/16 match the destination,
  always use the MORE SPECIFIC (longer prefix) route.
  10.1.0.0/16 wins over 10.0.0.0/8 for destinations in 10.1.x.x
```

**Routing Protocols:**

```
ROUTING PROTOCOLS — HOW ROUTERS LEARN ROUTES:

STATIC ROUTING:
  Admin manually types routes
  ┌─────────────────────────────────────────────────────────┐
  │  Pro: Simple, secure, predictable                       │
  │  Con: Doesn't adapt to failures, time-consuming         │
  │  Use: Small networks, specific routes (default route)   │
  └─────────────────────────────────────────────────────────┘

DYNAMIC ROUTING (self-learning):
  Routers automatically discover and share routes

  ┌────────────────────────────────────────────────────────────┐
  │  OSPF (Open Shortest Path First)                          │
  │  • Used WITHIN an organization (Interior Gateway Protocol) │
  │  • Link-State protocol: each router knows full topology    │
  │  • Finds shortest path using Dijkstra's algorithm         │
  │  • Fast convergence (seconds after failure)               │
  │  • Used in enterprise, ISP core networks                  │
  └────────────────────────────────────────────────────────────┘
  
  ┌────────────────────────────────────────────────────────────┐
  │  BGP (Border Gateway Protocol)                            │
  │  • THE routing protocol of the internet!                  │
  │  • Used BETWEEN organizations (Exterior Gateway Protocol)  │
  │  • Path-vector: knows entire AS-path to destination       │
  │  • Policy-based: ISPs control traffic flow for business   │
  │  • Extremely stable but slow to converge (~minutes)       │
  │  • ~900,000 routes in the global routing table (2024)     │
  └────────────────────────────────────────────────────────────┘
  
  ┌────────────────────────────────────────────────────────────┐
  │  RIP (Routing Information Protocol)                        │
  │  • Old, simple distance-vector protocol                   │
  │  • Max 15 hops (not suitable for large networks)          │
  │  • Mostly replaced by OSPF; still found in small networks  │
  └────────────────────────────────────────────────────────────┘

THE INTERNET'S STRUCTURE — Autonomous Systems (AS):
  ┌──────────────────────────────────────────────────────────────┐
  │  Each ISP or large network = one Autonomous System (AS)      │
  │  Each AS has a unique AS Number (ASN)                        │
  │                                                              │
  │  AS 15169 (Google)  ── BGP ──  AS 7018 (AT&T)               │
  │                              ── BGP ──  AS 3356 (Lumen)      │
  │                                        ── BGP ──  AS 9498 (BSNL)│
  │                                                              │
  │  BGP is what "glues" the internet's 80,000+ ASes together!   │
  └──────────────────────────────────────────────────────────────┘
```

**NAT — Network Address Translation:**

```
NAT (Network Address Translation):

PROBLEM: Only 4.3B IPv4 addresses, but billions of devices
SOLUTION: One public IP shared by many private IPs

  Your Home Network (Private)          Internet (Public)
  ┌────────────────────────┐
  │ PC:    192.168.1.100   │──┐
  │ Phone: 192.168.1.101   │──┤         ┌─────────────────┐
  │ TV:    192.168.1.102   │──┤── ROUTER──│ 203.0.113.50    │── Internet
  │                        │  │ (NAT)    │ (your public IP)│
  │ All appear to internet  │  │          └─────────────────┘
  │ as ONE IP address!     │──┘
  └────────────────────────┘

NAT TABLE (router tracks connections):
  ┌──────────────────────┬─────────────┬──────────────────────┐
  │ Private IP:Port      │ Public IP   │ External Server      │
  ├──────────────────────┼─────────────┼──────────────────────┤
  │ 192.168.1.100:50234  │ 203.113.50  │ google.com:443       │
  │ 192.168.1.101:51290  │ 203.113.50  │ youtube.com:443      │
  │ 192.168.1.102:49876  │ 203.113.50  │ netflix.com:443      │
  └──────────────────────┴─────────────┴──────────────────────┘

When google.com responds → router checks table → routes to correct device!

PORT FORWARDING (punch hole through NAT):
  When you run a server behind NAT, external users can't reach it.
  Port forwarding: "Incoming traffic on port 8080 → 192.168.1.100:8080"
  Used for: home servers, gaming (PS5/Xbox), cameras
```

### 2.1.4 Network Topology Design and Analysis

```
NETWORK TOPOLOGIES:

BUS TOPOLOGY (legacy):
  All devices share one cable
  ─────────────────────────── (the "bus")
    │        │        │        │
   PC1      PC2      PC3     PC4
  
  Pro: Simple, cheap
  Con: One break = whole network down; collisions; half-duplex
  Status: OBSOLETE (replaced by star/switch topology)

STAR TOPOLOGY (home/office standard today):
         [PC1]
           │
  [PC3]──[Switch]──[PC2]
           │
         [PC4]
  
  Pro: One device failure doesn't affect others; easy to troubleshoot
  Con: Switch is single point of failure; central device required
  Status: DOMINANT for LANs worldwide

RING TOPOLOGY:
  PC1 ── PC2 ── PC3
   │              │
  PC4 ── PC5 ── PC6
  
  Pro: No collisions; predictable performance
  Con: One break can stop entire ring (unless dual ring)
  Used in: SONET/SDH fiber rings, some industrial networks

MESH TOPOLOGY:
  Each device connected to many others
  
  PC1 ──── PC2
   │  ╲  ╱   │
   │   PC5   │
   │  ╱  ╲   │
  PC3 ──── PC4
  
  Full mesh: every device connects to every other (N×(N-1)/2 links)
  Partial mesh: some redundant links
  Pro: Extremely resilient; multiple paths
  Con: Expensive; complex
  Used in: Internet backbone, military, financial networks

TREE (HIERARCHICAL) TOPOLOGY:
  Core Switch
     │
  ┌──┴──┐
 Dist  Dist
  │      │
 ┌┴┐   ┌┴┐
 Acc Acc Acc Acc
  │   │   │   │
 PCs PCs PCs PCs
 
  Used in: Enterprise campus networks (3-tier: core/distribution/access)
  Pro: Scalable; logical organization; easy to troubleshoot
```

**Modern Enterprise Network Design:**

```
ENTERPRISE NETWORK — THREE-TIER ARCHITECTURE:

  ┌─────────────────────────────────────────────────────────────────┐
  │                    INTERNET                                     │
  └───────────────────────────┬─────────────────────────────────────┘
                              │
  ┌───────────────────────────▼─────────────────────────────────────┐
  │                    EDGE / DMZ LAYER                             │
  │   ┌──────────────┐  ┌──────────────┐  ┌──────────────────────┐ │
  │   │   Firewall   │  │  Load Balancer│  │   Web/Email/DNS      │ │
  │   │ (filters     │  │  (distributes │  │   Servers (public    │ │
  │   │  bad traffic)│  │   load)       │  │   services)          │ │
  │   └──────────────┘  └──────────────┘  └──────────────────────┘ │
  └───────────────────────────┬─────────────────────────────────────┘
                              │
  ┌───────────────────────────▼─────────────────────────────────────┐
  │                    CORE LAYER                                   │
  │   ┌──────────────────────────────────────────────────────────┐  │
  │   │ Core Switches (10/40/100 Gbps; high availability pair)   │  │
  │   │ Routes traffic between all distribution blocks           │  │
  │   └──────────────────────────────────────────────────────────┘  │
  └──────────────────┬──────────────────────────────────────────────┘
          ┌──────────┴───────────────┐
  ┌───────▼──────────────┐   ┌──────▼─────────────────┐
  │  DISTRIBUTION LAYER  │   │  DISTRIBUTION LAYER    │
  │  Building A          │   │  Building B             │
  │  ┌─────────────────┐ │   │  ┌─────────────────┐   │
  │  │Distribution Sw  │ │   │  │Distribution Sw  │   │
  │  │(routing, VLANs, │ │   │  │                 │   │
  │  │ QoS policies)   │ │   │  │                 │   │
  │  └──────┬──────────┘ │   │  └──────┬──────────┘   │
  │    ┌────┴────┐       │   │    ┌────┴────┐         │
  │   Acc Sw  Acc Sw     │   │   Acc Sw  Acc Sw       │
  │    │         │       │   │    │         │         │
  │   PCs    Printers    │   │  Servers  PCs          │
  └──────────────────────┘   └────────────────────────┘
  
  VLAN segmentation: HR, Finance, Engineering on separate virtual networks
  QoS: Voice traffic prioritized over email
```

### 2.1.5 Mobile Networking and Cellular Technologies

```
CELLULAR NETWORK EVOLUTION:

1G (1981): Voice only, analog
  Frequency: 850 MHz | Speed: ~2 kbps (data) | Security: None!

2G (1991): Voice + SMS + basic data (GSM)
  Frequency: 900/1800 MHz | Speed: up to 384 kbps (EDGE) | Digital!

3G (2001): Mobile broadband
  Frequency: 850/1900/2100 MHz | Speed: up to 42 Mbps (HSPA+)

4G LTE (2009): Real mobile broadband
  Frequency: 700–2600 MHz | Speed: up to 150 Mbps (LTE) / 1 Gbps (LTE-A)
  Latency: ~30–50 ms

5G (2019): Ultra-fast, ultra-low latency, massive IoT
  Frequency: Sub-6 GHz AND mmWave (24–100 GHz)
  Speed: up to 20 Gbps theoretical
  Latency: ~1 ms (ultra-reliable low latency)

CELLULAR NETWORK ARCHITECTURE:

  Your Phone
     │
     │ (radio waves: 700 MHz – 100 GHz)
     ▼
  ┌─────────────────────────┐
  │  Base Station (gNB/eNB) │ ← antennas you see on towers
  │  Cell Tower             │
  └─────────────┬───────────┘
                │ (fiber backhaul)
                ▼
  ┌─────────────────────────┐
  │   Core Network (5GC)    │
  │   • AMF: Access control │
  │   • SMF: Session mgmt   │
  │   • UPF: Data forwarding│
  └─────────────┬───────────┘
                │
                ▼
           Internet / IMS (IP Multimedia Subsystem for voice)
```

**5G Technology Deep Dive:**

```
5G — THREE KEY USE CASES:

1. eMBB (Enhanced Mobile Broadband):
   Streaming 8K video, AR/VR, faster smartphones
   Speed: ~1–10 Gbps
   Technology: Massive MIMO (hundreds of antennas), mmWave (high-frequency)

2. mMTC (Massive Machine-Type Communications):
   IoT — millions of low-power devices per square km
   Battery life: devices last years on small battery
   Tech: Narrowband IoT (NB-IoT), LTE-M

3. URLLC (Ultra-Reliable Low-Latency):
   Self-driving cars, remote surgery, industrial automation
   Latency: <1 ms, 99.9999% reliability
   Tech: Network slicing, edge computing

5G FREQUENCY BANDS:
  ┌─────────────────────────────────────────────────────────────────┐
  │  Sub-1 GHz (600/700/850 MHz):                                  │
  │    • Coverage: huge (many km)                                   │
  │    • Speed: moderate (hundreds of Mbps)                        │
  │    • Penetrates buildings well                                  │
  │    • First 5G band deployed widely                             │
  │                                                                 │
  │  Mid-band (2.5–4.2 GHz — the "sweet spot"):                    │
  │    • Coverage: good (1–2 km cells)                             │
  │    • Speed: excellent (1+ Gbps)                                │
  │    • Balance of coverage and capacity                           │
  │    • C-band (3.5 GHz): most important globally                │
  │                                                                 │
  │  mmWave (24–100 GHz):                                          │
  │    • Coverage: tiny (< 300 meters, line-of-sight)             │
  │    • Speed: extraordinary (10+ Gbps)                           │
  │    • Blocked by rain, walls, leaves!                            │
  │    • Used in: dense urban, stadiums, indoor venues             │
  └─────────────────────────────────────────────────────────────────┘

NETWORK SLICING (5G innovation):
  One physical 5G network → multiple virtual networks
  Slice 1: "eMBB" → max bandwidth for consumers
  Slice 2: "URLLC" → min latency for autonomous cars
  Slice 3: "mMTC" → max device density for IoT
  Each slice has its own QoS guarantees! SDN makes this possible.
```

### 2.1.6 Networking in Cloud Computing

```
CLOUD NETWORKING — MAKING IT SCALE:

TRADITIONAL NETWORKING vs CLOUD NETWORKING:

Traditional:               Cloud:
Physical switches          Virtual switches (vSwitches)
Physical routers           Virtual routers
Manual configuration       API-driven configuration
Weeks to provision         Seconds to provision
Fixed capacity             Elastic scaling
Physical firewalls         Security groups (software)

CLOUD NETWORKING COMPONENTS:

  ┌──────────────────────────────────────────────────────────────────┐
  │                   Cloud Provider Network                          │
  │                                                                  │
  │  ┌──────────────────────────────────────────────────────────┐   │
  │  │              Your VPC (Virtual Private Cloud)             │   │
  │  │                                                          │   │
  │  │  ┌──────────────────┐  ┌──────────────────────────────┐  │   │
  │  │  │  Public Subnet   │  │       Private Subnet          │  │   │
  │  │  │  10.0.1.0/24     │  │       10.0.2.0/24             │  │   │
  │  │  │                  │  │                               │  │   │
  │  │  │ [Load Balancer]  │  │ [App Server 1] [App Server 2]│  │   │
  │  │  │ [Web Server]     │  │ [Database]                    │  │   │
  │  │  └────────┬─────────┘  └───────────────────────────────┘  │   │
  │  │           │                       ↑                        │   │
  │  │    [Internet Gateway]     [NAT Gateway]                    │   │
  │  └────────────┬──────────────────────────────────────────────┘   │
  │               │                                                   │
  └───────────────┼───────────────────────────────────────────────────┘
                  │
              Internet

SDN (Software-Defined Networking):
  Traditional: Network config embedded in hardware (routers/switches)
  SDN: Separate the "brains" (control plane) from "muscles" (data plane)
  
  ┌────────────────────────────────────────────────────────────┐
  │                  SDN ARCHITECTURE                          │
  │                                                            │
  │  ┌──────────────────────────────────────────────────────┐ │
  │  │              SDN Controller                           │ │
  │  │  "Central brain" — makes routing decisions            │ │
  │  │  OpenFlow, NETCONF, YANG                             │ │
  │  └───────────┬────────────────────┬─────────────────────┘ │
  │              │  (control plane)   │                        │
  │  ┌───────────▼──────┐  ┌──────────▼──────┐               │
  │  │  Switch/Router 1 │  │  Switch/Router 2 │  ...          │
  │  │  (just forwards  │  │  (just forwards  │               │
  │  │   packets, no    │  │   packets)       │               │
  │  │   thinking)      │  │                  │               │
  │  └──────────────────┘  └─────────────────┘               │
  │              ↑ data plane (forwarding)                     │
  └────────────────────────────────────────────────────────────┘
  
  Benefits: Central view of whole network, programmable, fast reconfiguration
  Used by: Google B4 (runs Google's backbone), AWS, Microsoft Azure
```

### 2.1.7 Future Internet Technologies

**IoT Networking:**

```
IoT (Internet of Things) — NETWORKING BILLIONS OF DEVICES:

IoT SCALE:
  2025 estimate: 75 billion connected IoT devices
  From: Smart sensors (1 byte/hour) to 4K cameras (50 Mb/s)
  
IoT COMMUNICATION TECHNOLOGIES:
  ┌────────────────┬──────────────┬───────────────┬─────────────┐
  │ Technology     │ Range        │ Power         │ Throughput  │
  ├────────────────┼──────────────┼───────────────┼─────────────┤
  │ Bluetooth LE   │ ~10m         │ Ultra-low     │ 1–3 Mbps    │
  │ (wearables,    │              │               │             │
  │  medical)      │              │               │             │
  ├────────────────┼──────────────┼───────────────┼─────────────┤
  │ Zigbee/Z-Wave  │ ~10–100m     │ Very low      │ 250 kbps    │
  │ (smart home)   │ (mesh)       │               │             │
  ├────────────────┼──────────────┼───────────────┼─────────────┤
  │ LoRaWAN        │ ~5–15 km     │ Extremely low │ 0.3–50 kbps │
  │ (agriculture,  │              │ (years        │             │
  │  utilities)    │              │  on battery)  │             │
  ├────────────────┼──────────────┼───────────────┼─────────────┤
  │ NB-IoT / LTE-M │ Cell range   │ Very low      │ 1–1000 kbps │
  │ (smart meters, │              │               │             │
  │  tracking)     │              │               │             │
  ├────────────────┼──────────────┼───────────────┼─────────────┤
  │ Wi-Fi 6/6E     │ ~60m         │ Medium        │ 1–10 Gbps   │
  │ (cameras,      │              │               │             │
  │  appliances)   │              │               │             │
  └────────────────┴──────────────┴───────────────┴─────────────┘

IoT NETWORK ARCHITECTURE:
  Sensor → Gateway → Edge Computing → Cloud
  
  Why edge computing? Sensor generates 1 GB/hr of raw video
  Sending all to cloud: too expensive, too slow
  Edge: process locally, send only meaningful events ("motion detected")
  
MQTT (Message Queue Telemetry Transport):
  THE protocol for IoT — ultra-lightweight publish/subscribe
  
  Temperature Sensor ──MQTT Publish──▶ Broker ──MQTT Subscribe──▶ Dashboard
  "temperature/room1"    23.5°C       (server)                   displays 23.5°C
  
  Designed for: unreliable networks, battery-powered devices
  Header: just 2 bytes! (vs HTTP's ~500 bytes minimum)
```

---

## 🔬 Hands-On Exercise 2.1

**Exercise A: DNS Investigation**

```bash
# Investigate how DNS works for a website:

# 1. Find IP of a website
nslookup github.com
dig github.com A

# 2. Check MX records (mail servers)
dig github.com MX

# 3. Trace DNS resolution path
dig +trace github.com

# 4. Measure DNS resolution time
time nslookup github.com 8.8.8.8    # Google's DNS
time nslookup github.com 1.1.1.1    # Cloudflare's DNS

# 5. Reverse lookup (IP to hostname)
dig -x 140.82.112.4   # GitHub's IP
```

**Exercise B: Subnet Calculation**

```
Given: 172.16.0.0/16 network
Task: Divide into 4 equal subnets

Solution:
Original: 172.16.0.0/16 = 65,534 hosts

To get 4 subnets: borrow 2 bits (2^2 = 4)
New mask: /16 + 2 = /18 (255.255.192.0)

Subnet 1: 172.16.0.0/18    (172.16.0.1 – 172.16.63.254)
Subnet 2: 172.16.64.0/18   (172.16.64.1 – 172.16.127.254)
Subnet 3: 172.16.128.0/18  (172.16.128.1 – 172.16.191.254)
Subnet 4: 172.16.192.0/18  (172.16.192.1 – 172.16.255.254)

Each subnet: 2^14 - 2 = 16,382 usable hosts
```

---

## ⚠️ Common Mistakes — Module 2.1

| Mistake | Reality |
|---------|---------|
| "192.168.x.x is the internet" | 192.168.x.x is PRIVATE; not reachable directly from internet |
| "DNS = IP address" | DNS resolves names TO IP addresses; they're different things |
| "5G mmWave works everywhere" | mmWave has <300m range and is blocked by buildings; mid-band is the workaround |
| "Cloud networking is different from regular networking" | Same protocols (TCP/IP, BGP, DNS); just virtualized and API-controlled |

---

# ══════════════════════════════════════════════════════
# MODULE 2.2 — NETWORK MODELS AND PROTOCOLS
# ══════════════════════════════════════════════════════

## 🎯 Learning Objectives

After completing this section, you will be able to:
- Explain all 7 OSI layers and map them to real protocols
- Understand TCP vs UDP and when to use each
- Trace an HTTP request from browser to server at every layer
- Explain how TLS/SSL creates secure HTTPS connections
- Describe SMTP, SNMP, SIP, and SCTP protocols and their roles
- Understand protocol design principles

---

## 📖 Introduction

Protocols are the languages of networking. Without shared protocols, devices from different manufacturers, different countries, and different eras couldn't communicate. Protocols define exactly how data is formatted, transmitted, received, and acknowledged — down to the precise layout of every bit in every packet header.

The genius of networking protocols is in their layering. Just as you don't need to know how a car engine works to drive, application developers don't need to know how IP routing works. Each layer provides services to the layer above and relies on services from the layer below. This separation of concerns enables the internet to be both incredibly complex internally and remarkably simple to develop applications for.

---

## 🏗️ Core Content

### 2.2.1 The OSI Model — The Seven-Layer Reference

```
THE OSI MODEL (Open Systems Interconnection):

Layer 7: APPLICATION
  "What the user/app sees"
  Protocols: HTTP, FTP, SMTP, DNS, SSH, SNMP
  Data unit: Message / Data
  
  Example: Your browser sends "GET /index.html"

Layer 6: PRESENTATION
  "Data format, encryption, compression"
  Protocols: SSL/TLS, JPEG, MP3, ASCII, Unicode
  Data unit: Data
  
  Example: HTML data encoded in UTF-8, TLS encryption applied

Layer 5: SESSION
  "Establishing, managing, terminating sessions"
  Protocols: NetBIOS, RPC, SQL sessions
  Data unit: Data
  
  Example: Maintaining a login session across multiple requests

Layer 4: TRANSPORT
  "End-to-end communication, reliability, flow control"
  Protocols: TCP, UDP, SCTP
  Data unit: Segment (TCP) / Datagram (UDP)
  
  Example: TCP breaks data into segments, numbers them, ensures delivery

Layer 3: NETWORK
  "Logical addressing and routing between networks"
  Protocols: IP (IPv4/IPv6), ICMP, OSPF, BGP
  Data unit: Packet
  
  Example: IP adds source/destination IP addresses, routers read this

Layer 2: DATA LINK
  "Node-to-node communication on same network segment"
  Protocols: Ethernet, Wi-Fi (802.11), PPP, VLAN (802.1Q)
  Data unit: Frame
  
  Example: Ethernet adds MAC addresses for local delivery

Layer 1: PHYSICAL
  "Actual bits on the wire/air"
  Technologies: Cat6 cable, fiber, Wi-Fi radio, coax
  Data unit: Bits
  
  Example: Electrical signals on copper, light pulses in fiber

─────────────────────────────────────────────────────────
MEMORY AIDS:
"Please Do Not Throw Sausage Pizza Away" (bottom to top: 1→7)
"All People Seem To Need Data Processing" (top to bottom: 7→1)
─────────────────────────────────────────────────────────
```

**Encapsulation — How Data Gets Wrapped:**

```
DATA ENCAPSULATION — TRAVELING DOWN THE OSI STACK:

Application wants to send: "Hello World"

Layer 7 (App):    [Hello World]
                  ↓ + HTTP header
Layer 6/5 (Pres/Sess): [HTTP Header][Hello World]
                  ↓ + TCP header
Layer 4 (Transport): [TCP Hdr][HTTP Hdr][Hello World]
                  ↓ + IP header
Layer 3 (Network): [IP Hdr][TCP Hdr][HTTP Hdr][Hello World]
                  ↓ + Ethernet header + trailer
Layer 2 (Data Link): [ETH Hdr][IP Hdr][TCP Hdr][HTTP Hdr][Hello World][ETH Trl]
                  ↓ Convert to bits
Layer 1 (Physical): 01101000 01100101 01101100 01101100 ...

AT THE RECEIVER — DECAPSULATION (reverse):
Layer 1: bits → bytes
Layer 2: strips Ethernet header, passes IP packet up
Layer 3: strips IP header, passes TCP segment up
Layer 4: strips TCP header, reassembles segments, passes HTTP up
Layer 7: HTTP data → browser renders "Hello World"
```

### 2.2.2 TCP/IP Model — The Practical Four-Layer Model

```
TCP/IP MODEL vs OSI MODEL:

OSI Model (7 layers)        TCP/IP Model (4 layers)
─────────────────────        ─────────────────────────
7. Application         ┐
6. Presentation        ├──► Application (HTTP, FTP, DNS, SMTP)
5. Session             ┘
4. Transport           ────► Transport (TCP, UDP)
3. Network             ────► Internet (IP, ICMP, ARP)
2. Data Link           ┐
1. Physical            ┴──► Network Access (Ethernet, Wi-Fi)

OSI: Academic reference model (useful for learning/troubleshooting)
TCP/IP: What the internet actually uses (practical implementation)

Why TCP/IP won:
  ✓ Simpler (4 vs 7 layers)
  ✓ Battle-tested in real deployment
  ✓ Vendor-neutral from the start
  ✓ ARPANET/internet was built on it first
```

### 2.2.3 TCP — Transmission Control Protocol in Depth

```
TCP (Transmission Control Protocol):
"The reliable workhorse of the internet"

KEY FEATURES:
  ✓ Connection-oriented (3-way handshake before data)
  ✓ Reliable delivery (every byte acknowledged)
  ✓ Ordered delivery (sequence numbers)
  ✓ Error detection (checksum)
  ✓ Flow control (receiver controls sender speed)
  ✓ Congestion control (slows down when network congested)

THE THREE-WAY HANDSHAKE:

  Client                          Server
    │                               │
    │── SYN (seq=100) ─────────────▶│  "I want to connect, starting at 100"
    │                               │
    │◀─ SYN-ACK (seq=300, ack=101) ─│  "OK! I start at 300, got your 100"
    │                               │
    │── ACK (ack=301) ─────────────▶│  "Got it! Connection established!"
    │                               │
    │════════ DATA TRANSFER ════════│
    │                               │
    │── FIN ───────────────────────▶│  "I'm done sending"
    │◀─ ACK ────────────────────────│  "Got it"
    │◀─ FIN ────────────────────────│  "I'm done too"
    │── ACK ───────────────────────▶│  "OK, goodbye!"
    
  Why 3-way? Establish that BOTH sides can send AND receive!

TCP HEADER FIELDS:
  ┌────────────────────────────────────────────────────────────┐
  │ Source Port (16)    │ Destination Port (16)                │
  ├────────────────────────────────────────────────────────────┤
  │                Sequence Number (32 bits)                   │
  ├────────────────────────────────────────────────────────────┤
  │              Acknowledgment Number (32 bits)               │
  ├────────────────────────────────────────────────────────────┤
  │ Offset │Reserved│ Flags: URG ACK PSH RST SYN FIN           │
  ├────────────────────────────────────────────────────────────┤
  │ Window Size (16)    │ Checksum (16)   │ Urgent Ptr (16)   │
  ├────────────────────────────────────────────────────────────┤
  │                Options (if any)                            │
  └────────────────────────────────────────────────────────────┘
  Total minimum: 20 bytes overhead per segment

TCP FLOW CONTROL (Sliding Window):
  Receiver advertises how much buffer space it has (Window Size)
  Sender can send up to Window Size bytes without waiting for ACK
  
  Window = 3 segments:
  Send: [1][2][3]→ → → (no ACK needed yet)
  ACK 1 arrives: window slides → Send [4]
  ACK 2 arrives: window slides → Send [5]
  
  If receiver buffer full → Window Size = 0 → sender pauses!

TCP CONGESTION CONTROL:
  Slow Start: Start with 1 segment, double each RTT until threshold
  Congestion Avoidance: Linear increase after threshold
  Packet loss detected → halve window size, restart
  
  This prevents the internet from collapsing under load!
```

**TCP vs UDP — Choose the Right Tool:**

```
TCP vs UDP COMPARISON:

╔═════════════════════╦══════════════════════╦═══════════════════════╗
║ Feature             ║ TCP                  ║ UDP                   ║
╠═════════════════════╬══════════════════════╬═══════════════════════╣
║ Connection          ║ Yes (3-way handshake)║ No (connectionless)   ║
╠═════════════════════╬══════════════════════╬═══════════════════════╣
║ Reliability         ║ Guaranteed           ║ Not guaranteed         ║
╠═════════════════════╬══════════════════════╬═══════════════════════╣
║ Ordering            ║ In-order delivery    ║ May arrive out of order║
╠═════════════════════╬══════════════════════╬═══════════════════════╣
║ Error checking      ║ Yes + retransmit     ║ Checksum only         ║
╠═════════════════════╬══════════════════════╬═══════════════════════╣
║ Speed               ║ Slower (overhead)    ║ Faster (minimal overhead)║
╠═════════════════════╬══════════════════════╬═══════════════════════╣
║ Header size         ║ 20+ bytes            ║ 8 bytes               ║
╠═════════════════════╬══════════════════════╬═══════════════════════╣
║ Flow control        ║ Yes                  ║ No                    ║
╠═════════════════════╬══════════════════════╬═══════════════════════╣
║ Congestion control  ║ Yes                  ║ No                    ║
╠═════════════════════╬══════════════════════╬═══════════════════════╣
║ Best for            ║ Web, email, files,   ║ Video streaming, DNS, ║
║                     ║ database, SSH        ║ gaming, VoIP, DHCP    ║
╚═════════════════════╩══════════════════════╩═══════════════════════╝

WHEN UDP WINS:
  • Real-time applications (1 stale frame better than wait for retransmit)
  • DNS queries (quick request/response; retry on timeout)
  • Games (fast paced; old position data is useless anyway)
  • Streaming (buffer handles minor loss; retransmit = too slow)
  • QUIC/HTTP3: UDP with reliability built at app layer (best of both!)

UDP HEADER (tiny — 8 bytes!):
  ┌───────────────────────────────────────┐
  │ Source Port (16)│ Dest Port (16)      │
  ├───────────────────────────────────────┤
  │ Length (16)     │ Checksum (16)       │
  └───────────────────────────────────────┘
```

### 2.2.4 HTTP — HyperText Transfer Protocol

```
HTTP — THE LANGUAGE OF THE WEB:

HTTP VERSIONS EVOLUTION:
  HTTP/1.0 (1996): One request per connection (very slow!)
  HTTP/1.1 (1997): Persistent connections, pipelining
  HTTP/2  (2015):  Multiplexing (multiple requests on one connection)
  HTTP/3  (2022):  Built on QUIC (UDP-based), eliminates head-of-line blocking

HTTP REQUEST STRUCTURE:
  ┌─────────────────────────────────────────────────────────────┐
  │ GET /api/users?id=123 HTTP/1.1                              │ ← Request Line
  │ Host: api.example.com                                       │ ← Headers
  │ User-Agent: Mozilla/5.0 (Chrome/120.0)                     │
  │ Accept: application/json                                    │
  │ Authorization: Bearer eyJhbGci...                          │
  │ Cookie: session=abc123                                      │
  │                                                             │ ← Blank line
  │ (no body for GET)                                           │ ← Body
  └─────────────────────────────────────────────────────────────┘

HTTP RESPONSE STRUCTURE:
  ┌─────────────────────────────────────────────────────────────┐
  │ HTTP/1.1 200 OK                                             │ ← Status Line
  │ Content-Type: application/json                             │ ← Headers
  │ Content-Length: 84                                         │
  │ Cache-Control: max-age=3600                                │
  │ Set-Cookie: session=xyz789; Secure; HttpOnly               │
  │                                                             │ ← Blank line
  │ {"id": 123, "name": "Alice", "email": "alice@example.com"} │ ← Body
  └─────────────────────────────────────────────────────────────┘

HTTP STATUS CODES:
  ┌──────┬────────────────────────────────────────────────────────┐
  │ 1xx  │ Informational (100 Continue, 101 Switching Protocols) │
  ├──────┼────────────────────────────────────────────────────────┤
  │ 2xx  │ Success                                                │
  │      │ 200 OK, 201 Created, 204 No Content                   │
  ├──────┼────────────────────────────────────────────────────────┤
  │ 3xx  │ Redirection                                            │
  │      │ 301 Moved Permanently, 302 Found, 304 Not Modified    │
  ├──────┼────────────────────────────────────────────────────────┤
  │ 4xx  │ Client Error                                           │
  │      │ 400 Bad Request, 401 Unauthorized, 403 Forbidden      │
  │      │ 404 Not Found, 429 Too Many Requests                  │
  ├──────┼────────────────────────────────────────────────────────┤
  │ 5xx  │ Server Error                                           │
  │      │ 500 Internal Server Error, 503 Service Unavailable    │
  └──────┴────────────────────────────────────────────────────────┘

HTTP METHODS (Verbs):
  GET    → Retrieve resource (no body, cacheable)
  POST   → Create resource (has body)
  PUT    → Replace resource completely (idempotent)
  PATCH  → Partial update of resource
  DELETE → Delete resource
  HEAD   → Like GET but returns only headers (check if resource exists)
  OPTIONS→ What methods does this endpoint support?
```

**A Complete HTTP Request Journey (Wireshark-level view):**

```
WHAT HAPPENS WHEN YOU TYPE "https://github.com" AND PRESS ENTER:

1. Browser checks DNS cache → miss
2. DNS resolver: "github.com" → 140.82.112.4 (A record)  [~10ms]

3. TCP 3-way handshake to 140.82.112.4:443  [~50ms]
   SYN → SYN-ACK → ACK

4. TLS Handshake (HTTPS security):  [~50ms]
   ClientHello → ServerHello → Certificate → 
   Key Exchange → Finished (now encrypted!)

5. HTTP/2 GET request sent (over TLS):  [~10ms]
   ":method: GET"
   ":path: /"
   ":authority: github.com"
   "accept: text/html"

6. Server sends HTTP/2 HEADERS frame (status 200)
   Then DATA frames (HTML content)
   
7. Browser parses HTML, requests additional resources:
   JS, CSS, images → all multiplexed on same TCP connection (HTTP/2)

8. Browser renders page

TOTAL TIME: 100–500ms for first page load
(Much faster on subsequent loads: DNS cached, TLS resumed, HTTP cached)
```

### 2.2.5 FTP and File Transfer Protocols

```
FTP (File Transfer Protocol):

ARCHITECTURE — Two connections:
  ┌────────────────────────────────────────────────────────────────┐
  │  FTP uses TWO TCP connections:                                  │
  │                                                                │
  │  Client                          Server                        │
  │    │── port 21 ─────────────────▶│  Control Connection         │
  │    │   (commands: LIST, RETR, STOR│  "ls /files"               │
  │    │    USER, PASS, QUIT)         │  "get report.pdf"          │
  │    │                              │                            │
  │    │◀─ Data Connection ───────────│  (port 20 from server)     │
  │    │   (actual file data flows    │  or any port (passive mode)│
  │    │    on separate connection)   │                            │
  └────────────────────────────────────────────────────────────────┘

ACTIVE vs PASSIVE MODE:
  Active FTP:  Client sends its IP/port → Server initiates data connection
               PROBLEM: Firewalls block incoming connections to clients!
  
  Passive FTP: Server sends its IP/port → Client connects to it
               SOLUTION: Client always initiates → firewall-friendly

FTP ALTERNATIVES (because FTP is insecure!):
  ┌────────────────────────────────────────────────────────────────┐
  │ Protocol │ Security    │ Port │ Notes                          │
  ├──────────┼─────────────┼──────┼────────────────────────────────┤
  │ FTP      │ None (plain)│  21  │ Username/password in cleartext!│
  │ FTPS     │ TLS/SSL     │ 990  │ FTP + encryption               │
  │ SFTP     │ SSH         │  22  │ Different protocol; runs on SSH│
  │ SCP      │ SSH         │  22  │ Simple file copy over SSH      │
  │ HTTPS    │ TLS         │ 443  │ Modern web file transfers      │
  │ rsync    │ SSH         │  22  │ Efficient sync (only diffs)    │
  └────────────────────────────────────────────────────────────────┘
  
  RECOMMENDATION: Never use plain FTP in 2024. Use SFTP or HTTPS.
```

### 2.2.6 Transport Layer Beyond TCP/UDP — SCTP

```
SCTP (Stream Control Transmission Protocol):

"The best protocol you've never heard of"

WHY SCTP EXISTS:
  TCP: Single stream (if one message blocked, all wait)
  UDP: No reliability at all
  SCTP: Multiple streams + reliability + multi-homing!

SCTP KEY FEATURES:
  ┌────────────────────────────────────────────────────────────────┐
  │ 1. MULTI-STREAMING:                                           │
  │    One SCTP association → multiple independent streams         │
  │    Stream 1: signaling messages (real-time!)                   │
  │    Stream 2: bulk file data (can lag)                         │
  │    Stream 3: log events (best-effort)                         │
  │    → Head-of-line blocking eliminated!                         │
  │                                                                │
  │ 2. MULTI-HOMING:                                              │
  │    One connection can use multiple IP addresses                │
  │    Server has: 192.168.1.10 AND 10.0.0.5                      │
  │    Primary path fails → instantly failover to secondary        │
  │    → Zero-downtime failover! TCP can't do this.               │
  │                                                                │
  │ 3. MESSAGE-ORIENTED:                                          │
  │    Like UDP: preserves message boundaries                      │
  │    Like TCP: guaranteed delivery                               │
  │    Perfect for signaling protocols!                            │
  │                                                                │
  │ 4. 4-WAY HANDSHAKE (more secure than TCP):                    │
  │    INIT → INIT-ACK → COOKIE-ECHO → COOKIE-ACK                │
  │    Stateless server until cookie verified (SYN-flood resistant)│
  └────────────────────────────────────────────────────────────────┘

WHERE SCTP IS USED:
  • Telecom signaling: SS7 over IP (Sigtran), Diameter
  • 4G/5G core network: S1-AP, X2-AP, NGAP interfaces
  • WebRTC data channels (internally)
  • Financial systems (multi-homing for failover)

QUIC (The Modern Answer):
  HTTP/3 uses QUIC (UDP-based) to solve HTTP/2 head-of-line blocking
  QUIC brings: reliability, multiplexing, 0-RTT connection on UDP
  Essentially: TCP + TLS + HTTP/2 multiplexing built on UDP
```

### 2.2.7 Application Layer Protocols — SMTP, SNMP, SIP

**SMTP — Simple Mail Transfer Protocol:**

```
SMTP — HOW EMAIL ACTUALLY WORKS:

You click "Send" in Gmail. Here's what happens:

  ┌──────────────────────────────────────────────────────────────────┐
  │ gmail.com (sender)              yahoo.com (recipient)            │
  │                                                                  │
  │  [Gmail Client]                                                  │
  │      │ SMTP (port 587, STARTTLS)                                │
  │      ▼                                                           │
  │  [Gmail SMTP Server]                                             │
  │      │ 1. DNS lookup: yahoo.com MX record → mta5.am0.yahoodns.net
  │      │ 2. TCP connect to mta5.am0.yahoodns.net:25               │
  │      │ 3. SMTP dialog:                                          │
  │      ▼                                                           │
  │  [Yahoo MX Server] ──stores──▶ [Yahoo Mailbox]                  │
  │                                      │                          │
  │                                      │ IMAP/POP3 (port 993/995) │
  │                                      ▼                          │
  │                                 [Yahoo Client: Retrieves email] │
  └──────────────────────────────────────────────────────────────────┘

SMTP CONVERSATION (wire-level):
  C→S: EHLO mail.gmail.com
  S→C: 250-mta5.am0.yahoodns.net
       250-SIZE 41943040
       250-STARTTLS
       250 8BITMIME
  C→S: STARTTLS           ← upgrade to TLS!
  S→C: 220 Go ahead
  [TLS handshake happens...]
  C→S: EHLO mail.gmail.com
  C→S: MAIL FROM:<alice@gmail.com>
  S→C: 250 OK
  C→S: RCPT TO:<bob@yahoo.com>
  S→C: 250 OK
  C→S: DATA
  S→C: 354 Start input
  C→S: Subject: Hello Bob
       From: alice@gmail.com
       To: bob@yahoo.com
       
       Hello Bob! How are you?
       .              ← single dot on line = end of message
  S→C: 250 OK, queued
  C→S: QUIT
  S→C: 221 Bye

EMAIL SECURITY TRIO (prevent spam/phishing):
  SPF:  "These IPs are allowed to send email for gmail.com"
        TXT record: "v=spf1 include:_spf.google.com ~all"
  
  DKIM: Gmail SIGNS each email with private key
        Recipient verifies with public key in DNS
        Proves email not tampered with in transit
  
  DMARC: Policy: if SPF or DKIM fail, quarantine or reject the email
         Reports sent to postmaster — visibility into abuse
```

**SNMP — Network Management:**

```
SNMP (Simple Network Management Protocol):

HOW NETWORK ADMINS MONITOR THOUSANDS OF DEVICES:

ARCHITECTURE:
  ┌────────────────────────────────────────────────────────────────┐
  │  [Network Management System (NMS)]                            │
  │   Observium, PRTG, Zabbix, Nagios, Prometheus                 │
  │        │                                                       │
  │        │ SNMP queries (UDP port 161)                          │
  │        │ SNMP traps received (UDP port 162)                   │
  │        │                                                       │
  │   ┌────▼────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐     │
  │   │ Router  │  │  Switch  │  │ Firewall │  │  Server  │     │
  │   │ Agent   │  │  Agent   │  │  Agent   │  │  Agent   │     │
  │   │ (runs   │  │ (reports │  │          │  │          │     │
  │   │  SNMP)  │  │  to NMS) │  │          │  │          │     │
  │   └─────────┘  └──────────┘  └──────────┘  └──────────┘     │
  └────────────────────────────────────────────────────────────────┘

MIB (Management Information Base):
  Hierarchical tree of variables every device exposes
  
  1.3.6.1.2.1.1.1.0 = sysDescr (device description)
  1.3.6.1.2.1.1.3.0 = sysUpTime (how long running)
  1.3.6.1.2.1.2.2.1.10 = ifInOctets (bytes received on interface)
  1.3.6.1.2.1.2.2.1.16 = ifOutOctets (bytes sent on interface)

SNMP OPERATIONS:
  GET:        NMS reads one MIB variable from agent
  GET-NEXT:   Walk through MIB tree
  GET-BULK:   Efficient bulk reads (SNMPv2+)
  SET:        NMS writes variable (configure device remotely!)
  TRAP:       Agent sends alert to NMS (link down, high CPU, etc)
  INFORM:     Trap with acknowledgment (SNMPv2+)

VERSIONS:
  SNMPv1:  Cleartext community strings (like passwords) — INSECURE
  SNMPv2c: Better performance, same security model — still cleartext
  SNMPv3:  Authentication + encryption — USE THIS in production!
```

**SIP — Session Initiation Protocol (VoIP):**

```
SIP (Session Initiation Protocol):

THE PROTOCOL BEHIND VOIP (IP Phones, Zoom, WhatsApp calls):

SIP ARCHITECTURE:
  ┌────────────────────────────────────────────────────────────────┐
  │  [Alice SIP Phone]         [SIP Proxy/Server]   [Bob SIP Phone]│
  │  sip:alice@company.com          │              sip:bob@company.com│
  │         │                       │                     │         │
  │         │── INVITE ────────────▶│── INVITE ──────────▶│         │
  │         │   (call Bob, let's    │                     │         │
  │         │    use G.711 codec)   │◀─ 180 Ringing ──────│ (ring!) │
  │         │◀─ 180 Ringing ────────│                     │         │
  │         │                       │◀─ 200 OK ───────────│ (answer)│
  │         │◀─ 200 OK ─────────────│                     │         │
  │         │── ACK ───────────────────────────────────── ▶│         │
  │         │                                              │         │
  │         │◀═══════════RTP (audio packets, UDP)══════════│         │
  │         │═══════════════════════════════════════════════▶        │
  │         │          (direct media flow — bypasses SIP server!)    │
  │         │                                              │         │
  │         │── BYE ───────────────────────────────────── ▶│ (hang up)│
  │         │◀─ 200 OK ─────────────────────────────────── │         │
  └────────────────────────────────────────────────────────────────┘

SIP: Signaling only (INVITE, BYE, ACK — like phone call setup)
RTP: Real-time media (actual audio/video — UDP for low latency)

CODECS (compression algorithms for audio):
  G.711:  8 kHz, 64 kbps — toll-quality, no compression
  G.729:  8 kHz, 8 kbps — compressed, slight quality loss
  Opus:   6–510 kbps, adaptive — used by WebRTC, best quality/compression
  G.722:  16 kHz (HD voice) — sounds much better than G.711!

SIP SECURITY:
  Plain SIP: Unencrypted! Anyone on network can eavesdrop calls!
  SIPS: SIP over TLS (port 5061) — encrypts signaling
  SRTP: Secure RTP — encrypts media (audio/video)
  WebRTC: Uses DTLS-SRTP — both TLS and SRTP by default!
```

### 2.2.8 Network Protocol Security — SSL/TLS

```
TLS (Transport Layer Security) — HOW HTTPS WORKS:

TLS is the security layer under HTTPS, IMAPS, FTPS, SMTPS, LDAPS, etc.

TLS PROVIDES THREE GUARANTEES:
  1. AUTHENTICATION: Is this really github.com? (via certificates)
  2. CONFIDENTIALITY: Is our conversation private? (via encryption)
  3. INTEGRITY: Was data modified in transit? (via HMAC/AEAD)

TLS 1.3 HANDSHAKE (the modern version, 2018):

  Client                                    Server
    │                                          │
    │── ClientHello ──────────────────────────▶│
    │   "I support TLS 1.3"                    │
    │   "My key_share (Diffie-Hellman public)" │
    │   "Supported cipher suites"              │
    │                                          │
    │◀─ ServerHello ────────────────────────── │
    │   "Using TLS 1.3"                        │
    │   "My key_share (DH public)"             │
    │   "Using AES-256-GCM cipher"             │
    │◀─ Certificate (server's public cert) ─── │
    │◀─ CertificateVerify (signed by server) ──│
    │◀─ Finished (HMAC of handshake) ──────────│
    │                                          │
    │   [Both derive same session keys from    │
    │    DH key exchange — no key transmitted! │
    │    Ephemeral keys → Perfect Forward Sec] │
    │                                          │
    │── Finished (HMAC of handshake) ─────────▶│
    │                                          │
    │═══════ ENCRYPTED APPLICATION DATA ═══════│

TOTAL: 1 Round-Trip Time (vs 2 RTT for TLS 1.2)!
TLS 1.3 0-RTT: Resume previous session → send data immediately!

TLS CERTIFICATE CHAIN OF TRUST:
  ┌────────────────────────────────────────────────────────────────┐
  │  ROOT CA (DigiCert, Let's Encrypt, etc.)                      │
  │  Self-signed, stored in OS/browser trust store                │
  │  └── INTERMEDIATE CA                                          │
  │       Signed by Root; one level down for security             │
  │       └── SERVER CERTIFICATE (github.com)                     │
  │            Signed by Intermediate                             │
  │            Contains: domain, expiry, public key               │
  │                                                               │
  │  Validation: Browser verifies chain: Server ← Intermediate ← Root │
  │  If any signature invalid → HTTPS WARNING!                    │
  └────────────────────────────────────────────────────────────────┘

CIPHER SUITES (the crypto recipe):
  TLS_AES_128_GCM_SHA256
  │   │           │    │
  │   Key exchange│    Hash for HMAC (SHA-256)
  │   (ECDHE)     │
  TLS            AES-128-GCM (authenticated encryption)

Modern strong cipher suites (TLS 1.3):
  TLS_AES_256_GCM_SHA384        ← most common
  TLS_CHACHA20_POLY1305_SHA256  ← best for mobile (no hardware AES)
  TLS_AES_128_GCM_SHA256        ← slightly less secure but faster

WHAT TLS PROTECTS AGAINST:
  ✓ Eavesdropping (encryption)
  ✓ Man-in-the-middle (certificate verification)
  ✓ Replay attacks (sequence numbers, nonces)
  ✓ Downgrade attacks (TLS 1.3 prevents negotiating old versions)

WHAT TLS DOESN'T PROTECT:
  ✗ Server IP and domain (visible in SNI field during handshake)
  ✗ Traffic analysis (timing, sizes)
  ✗ Bugs in the application (SQLi, XSS, etc.)
  ✗ Compromised certificate authorities
```

**Practical TLS Commands:**

```bash
# Check a website's TLS certificate
openssl s_client -connect github.com:443

# See certificate details (expiry, issuer, etc.)
echo | openssl s_client -connect github.com:443 2>/dev/null | openssl x509 -noout -text

# Test which TLS versions a server supports
nmap --script ssl-enum-ciphers -p 443 github.com

# Quick TLS test
curl -v https://github.com 2>&1 | grep -E "SSL|TLS|cipher|certificate"
```

### 2.2.9 Protocol Design Principles

```
PROTOCOL ENGINEERING — DESIGNING PROTOCOLS THAT LAST:

8 KEY DESIGN PRINCIPLES:

1. LAYERING (Separation of concerns)
   Each layer provides well-defined services to layer above
   Changes in one layer shouldn't break others
   ✓ HTTP doesn't know if TCP uses TLS or not

2. ROBUSTNESS PRINCIPLE (Postel's Law)
   "Be liberal in what you accept, conservative in what you send"
   Accept slightly malformed input; send strictly correct output
   Reality: this principle has caused security issues (too permissive)

3. STATELESSNESS (when possible)
   HTTP was designed stateless → enables horizontal scaling
   REST APIs: each request contains all needed information
   Session state in cookies, tokens → server stays stateless

4. IDEMPOTENCY
   Same request multiple times = same result as once
   GET, PUT, DELETE = idempotent
   POST = NOT idempotent (creates new resource each time)
   Critical for: retries, crash recovery, distributed systems

5. VERSIONING
   Plan for evolution from day one
   HTTP/1.0 → 1.1 → 2 → 3 (backward compatible at content level)
   Bad example: changing protocol format breaks all clients

6. EXTENSIBILITY
   Reserved fields for future use
   Options/extensions mechanism
   Unknown extensions → safely ignored

7. ERROR REPORTING
   Clear, specific error codes (HTTP status codes are great example)
   Include enough info for debugging but not security info (no stack traces)

8. SECURITY BY DESIGN
   Authentication, authorization, encryption from the start
   Not bolted on later! (FTP learned this the hard way)

REAL-WORLD EXAMPLE — Why HTTP/2 needed HTTP/3:
  HTTP/2 fixed many HTTP/1.1 issues with multiplexing
  But: used TCP, which has head-of-line blocking at transport layer!
  One lost TCP packet → ALL HTTP/2 streams stop and wait
  
  HTTP/3 solution: Use QUIC (UDP-based)
  QUIC multiplexes independently at transport level
  Lost packet in stream 1 → streams 2 and 3 continue normally!
```

---

## 🔬 Hands-On Exercises — Module 2.2

**Exercise A: Capture and Analyze a TLS Handshake in Wireshark**

```
Steps:
1. Open Wireshark
2. Start capture on your main network interface
3. In your browser, navigate to any HTTPS website
4. Stop capture
5. Filter: "ssl" or "tls"

What to find:
a) "Client Hello" packet → expand TLS layer → 
   find "Supported Cipher Suites" — count how many your browser supports
   
b) "Server Hello" → find which cipher suite was selected

c) "Certificate" packet → expand → 
   find "Certificate Signature Algorithm" — what algorithm?
   find "Validity: Not After" — when does cert expire?

d) After "Finished" → all subsequent packets are "Application Data"
   You CANNOT read these — TLS encryption is working!
```

**Exercise B: HTTP Request Anatomy**

```bash
# Make an HTTP request and examine all headers:

# Basic HTTP request
curl -v http://httpbin.org/get

# HTTPS with full certificate info
curl -v https://httpbin.org/get

# Custom headers
curl -H "Accept: application/json" \
     -H "User-Agent: MyApp/1.0" \
     https://httpbin.org/headers

# POST request with JSON body
curl -X POST \
     -H "Content-Type: application/json" \
     -d '{"name":"Alice","age":30}' \
     https://httpbin.org/post

# Examine redirect behavior
curl -v -L https://httpbin.org/redirect/3

# Check HTTP status codes
curl -o /dev/null -s -w "HTTP Status: %{http_code}\nTime: %{time_total}s\n" \
     https://github.com
```

**Exercise C: Email Protocol Analysis**

```bash
# SMTP: Test connection to an email server (won't send, just tests):
telnet smtp.gmail.com 587
# You should see: "220 smtp.gmail.com ESMTP"
# Type: EHLO test.local
# You should see capabilities including STARTTLS

# DNS: Find where to deliver email for a domain:
dig gmail.com MX
dig yahoo.com MX

# Check SPF record:
dig gmail.com TXT | grep spf

# Check DMARC record:
dig _dmarc.gmail.com TXT
```

---

## ⚠️ Common Mistakes — Module 2.2

| Mistake | Reality |
|---------|---------|
| "HTTPS means the site is safe" | HTTPS = encrypted connection; NOT that the site itself is legitimate |
| "TCP is always better than UDP" | UDP is essential for real-time apps where reliability adds worse latency |
| "OSI and TCP/IP are the same" | OSI has 7 layers; TCP/IP has 4; OSI is reference model, TCP/IP is what we use |
| "TLS 1.0 and TLS 1.3 are both fine" | TLS 1.0/1.1 have serious vulnerabilities; TLS 1.3 is the minimum modern standard |
| "Port 80 is HTTP, port 443 is HTTPS — always" | Ports are just conventions; anything can run on any port |

---

## 💡 Best Practices — Module 2.2

- Always use TLS 1.3 for new deployments; disable TLS 1.0/1.1
- Use HTTP/2 or HTTP/3 — the performance improvement is significant (especially mobile)
- Use SNMPv3 — never SNMPv1 or SNMPv2c in production
- For new APIs: REST over HTTPS is the default; gRPC (HTTP/2 + Protobuf) for performance-critical
- For email: implement SPF + DKIM + DMARC — without these, your email goes to spam
- SFTP or HTTPS for file transfer — never plain FTP in production

---

# 📌 Quick Reference Cheat Sheet — Modules 2.0–2.2

```
╔══════════════════════════════════════════════════════════════════════════════╗
║                    NETWORKING QUICK REFERENCE                                ║
╠══════════════════════════════════════════════════════════════════════════════╣
║                                                                              ║
║  PRIVATE IP RANGES:                                                          ║
║    10.0.0.0/8     (10.x.x.x)                                               ║
║    172.16.0.0/12  (172.16–31.x.x)                                          ║
║    192.168.0.0/16 (192.168.x.x) ← most common home networks                ║
║    127.0.0.1      = localhost (yourself)                                     ║
║                                                                              ║
║  COMMON PORTS:                                                               ║
║    20/21 FTP    22 SSH    23 Telnet   25 SMTP   53 DNS                      ║
║    67/68 DHCP   80 HTTP   110 POP3    143 IMAP  161/162 SNMP               ║
║    389 LDAP     443 HTTPS  465 SMTPS  993 IMAPS 5060/5061 SIP              ║
║    3389 RDP     8080 HTTP-alt                                                ║
║                                                                              ║
║  OSI LAYERS (7→1): App, Presentation, Session, Transport, Network,          ║
║                    Data Link, Physical                                       ║
║  TCP/IP LAYERS:    Application, Transport, Internet, Network Access          ║
║                                                                              ║
║  TCP vs UDP:                                                                 ║
║    TCP: reliable, ordered, connection, flow control → web, email, files     ║
║    UDP: fast, no guarantee, connectionless → DNS, games, streaming, VoIP    ║
║                                                                              ║
║  DNS RECORD TYPES:                                                           ║
║    A=IPv4, AAAA=IPv6, CNAME=alias, MX=mail, NS=nameserver,                 ║
║    TXT=verification/SPF, PTR=reverse lookup                                  ║
║                                                                              ║
║  DHCP DORA: Discover → Offer → Request → Acknowledge                        ║
║                                                                              ║
║  SUBNETTING:                                                                 ║
║    /24 = 254 hosts | /16 = 65,534 hosts | /8 = 16M hosts                   ║
║    Hosts = 2^(32-prefix) - 2                                                ║
║                                                                              ║
║  TLS GUARANTEES: Authentication + Confidentiality + Integrity                ║
║  TLS 1.3: 1-RTT handshake | Perfect Forward Secrecy | 0-RTT resume         ║
║                                                                              ║
║  HTTP STATUS CODES:                                                          ║
║    1xx=Info, 2xx=Success, 3xx=Redirect, 4xx=Client Error, 5xx=Server Error ║
║    200=OK, 201=Created, 301=Moved, 404=Not Found, 500=Server Error          ║
║                                                                              ║
║  EMAIL SECURITY: SPF (allowed senders) + DKIM (signed) + DMARC (policy)    ║
║                                                                              ║
║  5G USE CASES: eMBB (fast), mMTC (many IoT), URLLC (low latency)           ║
║                                                                              ║
║  ROUTING PROTOCOLS:                                                          ║
║    OSPF = within organization (link-state, fast convergence)                 ║
║    BGP = between organizations (path-vector, glues the internet)             ║
║                                                                              ║
╚══════════════════════════════════════════════════════════════════════════════╝
```

---

# 📚 Appendix A — Glossary

| Term | Definition |
|------|-----------|
| **ACK** | Acknowledgment — TCP segment confirming receipt of data |
| **ARP** | Address Resolution Protocol — maps IP address to MAC address on local network |
| **AS** | Autonomous System — independently managed network with its own routing policy |
| **ASN** | Autonomous System Number — unique identifier for each AS on the internet |
| **BGP** | Border Gateway Protocol — routing protocol that connects the internet's ASes |
| **CIDR** | Classless Inter-Domain Routing — IP addressing notation: 192.168.1.0/24 |
| **DHCP** | Dynamic Host Configuration Protocol — automatically assigns IP addresses |
| **DMZ** | Demilitarized Zone — semi-trusted network segment for public-facing servers |
| **DNS** | Domain Name System — translates domain names to IP addresses |
| **DKIM** | DomainKeys Identified Mail — email signing for authentication |
| **DMARC** | Domain-based Message Authentication — email policy for SPF/DKIM failures |
| **DTLS** | Datagram TLS — TLS for UDP; used in WebRTC, QUIC |
| **Ethernet** | Most common wired LAN technology (IEEE 802.3) |
| **FTP** | File Transfer Protocol — file transfer, old and insecure |
| **HTTPS** | HTTP over TLS — encrypted web browsing |
| **ICMP** | Internet Control Message Protocol — error reporting; used by ping |
| **IMAP** | Internet Message Access Protocol — email retrieval (keeps messages on server) |
| **IoT** | Internet of Things — network of physical devices with sensors/connectivity |
| **IP** | Internet Protocol — logical addressing and routing |
| **IPSec** | IP Security — encryption/authentication at the network layer |
| **IPS** | Intrusion Prevention System — detects and blocks network threats |
| **IPv4** | 32-bit addresses; 4.3 billion total; exhausted |
| **IPv6** | 128-bit addresses; 340 undecillion total; replacing IPv4 |
| **ISP** | Internet Service Provider — company providing internet access |
| **LAN** | Local Area Network — network within a building or campus |
| **Latency** | Time for data to travel from source to destination and back (RTT) |
| **MAC** | Media Access Control — unique hardware address burned into NIC |
| **MIME** | Multipurpose Internet Mail Extensions — email attachment encoding |
| **mmWave** | Millimeter Wave — high-frequency 5G spectrum (24–100 GHz) |
| **MQTT** | Message Queue Telemetry Transport — lightweight IoT protocol |
| **MTU** | Maximum Transmission Unit — max packet size on a network (Ethernet: 1500 bytes) |
| **NAT** | Network Address Translation — maps private IPs to one public IP |
| **NIC** | Network Interface Card — hardware connecting device to network |
| **NMS** | Network Management System — software monitoring network devices |
| **OSPF** | Open Shortest Path First — link-state routing protocol within an organization |
| **OSI** | Open Systems Interconnection — 7-layer network reference model |
| **PKI** | Public Key Infrastructure — system of digital certificates |
| **POP3** | Post Office Protocol 3 — email retrieval (downloads and deletes from server) |
| **Port** | 16-bit number identifying a specific application/service on a host |
| **QoS** | Quality of Service — prioritizing certain traffic over others |
| **QUIC** | Quick UDP Internet Connections — protocol underlying HTTP/3 |
| **REST** | Representational State Transfer — architectural style for web APIs |
| **RFC** | Request for Comments — documents defining internet standards |
| **Router** | Device connecting different networks, routing packets by IP address |
| **RTT** | Round Trip Time — time for packet to travel to destination and back |
| **SCTP** | Stream Control Transmission Protocol — multi-stream, multi-homed transport |
| **SDN** | Software-Defined Networking — separating control plane from data plane |
| **SFTP** | SSH File Transfer Protocol — secure file transfer over SSH |
| **SIP** | Session Initiation Protocol — call setup for VoIP |
| **SMTP** | Simple Mail Transfer Protocol — sending email between servers |
| **SNMP** | Simple Network Management Protocol — monitoring network devices |
| **SPF** | Sender Policy Framework — DNS record listing authorized email senders |
| **SRTP** | Secure Real-time Transport Protocol — encrypted audio/video |
| **SSH** | Secure Shell — encrypted remote access protocol |
| **SSL** | Secure Sockets Layer — predecessor to TLS (deprecated) |
| **Subnet** | Logical subdivision of a network |
| **Switch** | Device connecting devices within a LAN, using MAC addresses |
| **TCP** | Transmission Control Protocol — reliable, ordered transport |
| **TLS** | Transport Layer Security — encryption for network communications |
| **TTL** | Time To Live — prevents packets from looping forever |
| **UDP** | User Datagram Protocol — fast, unreliable transport |
| **VPN** | Virtual Private Network — encrypted tunnel over public internet |
| **VLAN** | Virtual LAN — logical network segmentation within a switch |
| **VoIP** | Voice over IP — telephone calls over internet |
| **WAN** | Wide Area Network — network spanning large geographic area |
| **WebRTC** | Web Real-Time Communication — browser-to-browser audio/video |
| **Wi-Fi** | Wireless LAN based on IEEE 802.11 standard |

---

# 📋 Appendix B — Interview Questions

## Networking (Beginner → Expert)

**Beginner:**

1. *What is the difference between a switch and a router?*
   Switch connects devices within the same network using MAC addresses. Router connects different networks using IP addresses. Your home router does both.

2. *What is DHCP and what does DORA stand for?*
   DHCP automatically assigns IP addresses. DORA = Discover, Offer, Request, Acknowledge — the four messages in the assignment process.

3. *What is the purpose of a subnet mask?*
   Defines which part of the IP address is the network and which is the host. /24 (255.255.255.0) means first 3 octets = network, last = host.

**Intermediate:**

4. *Explain the TCP three-way handshake.*
   SYN → SYN-ACK → ACK. Client sends SYN; server responds SYN-ACK (with its sequence number); client confirms with ACK. Establishes both-way communication before data flows.

5. *How does DNS resolution work? What is a recursive vs authoritative resolver?*
   Recursive resolver: queries on your behalf (your ISP or 8.8.8.8). Authoritative: the definitive source for a domain. Resolution path: client → recursive → root → TLD → authoritative → answer.

6. *What are the differences between HTTP/1.1, HTTP/2, and HTTP/3?*
   1.1: persistent connections, pipelining. 2: multiplexing (multiple streams on one TCP connection). 3: built on QUIC (UDP), eliminates TCP head-of-line blocking, faster handshake.

7. *Explain how NAT works and what problem it solves.*
   NAT lets many private IPs share one public IP. Router maintains a table mapping private_IP:port → public_IP:port for each connection. Solves IPv4 address exhaustion.

**Expert:**

8. *What is BGP and why does it underpin the entire internet?*
   BGP (Border Gateway Protocol) is the routing protocol connecting ~80,000 autonomous systems into the internet. Path-vector protocol; policy-based routing enables ISP business agreements (peering, transit). Without BGP, each AS would be isolated.

9. *Explain TLS 1.3 forward secrecy and why it matters.*
   TLS 1.3 requires ECDHE (Elliptic Curve Diffie-Hellman Ephemeral) key exchange. Session keys are fresh for every connection, not derived from the server's long-term private key. If a server's private key is compromised in the future, past sessions cannot be decrypted.

10. *What is QUIC and how does it improve on HTTP/2's approach?*
    QUIC is a multiplexed transport protocol built on UDP. HTTP/2 on TCP has transport-level HOL blocking (one lost TCP packet stalls all streams). QUIC implements independent streams at the transport level, so packet loss in stream 1 doesn't stall stream 2. Also: 0-RTT connection resumption, built-in TLS 1.3.

11. *Explain the difference between OSPF and BGP. When is each appropriate?*
    OSPF = Interior Gateway Protocol; uses Dijkstra's algorithm on a link-state map; fast convergence (seconds); used within one organization. BGP = Exterior Gateway Protocol; policy-based path selection; slow convergence (minutes); used between organizations. Enterprise uses OSPF internally; connects to ISP via BGP.

12. *What is the purpose of DNSSEC and what attack does it prevent?*
    DNSSEC (DNS Security Extensions) adds cryptographic signatures to DNS records. Prevents DNS cache poisoning (Kaminsky attack) where an attacker injects forged DNS responses to redirect traffic. Resolvers verify signatures against a chain of trust rooted at the DNS root zone.

---

# 🏆 Appendix C — Certifications Guide

```
NETWORKING CERTIFICATION ROADMAP:

BEGINNER LEVEL:
  CompTIA Network+ ─────────────────────────────────────
  Vendor-neutral foundation
  Topics: OSI model, TCP/IP, routing, switching, security
  Recommended for: First networking job, helpdesk → network
  
  Cisco CCNA ──────────────────────────────────────────
  Industry gold standard entry-level
  Topics: Routing, switching, VLANs, OSPF, ACLs, basic security
  Recommended for: Anyone in network engineering

INTERMEDIATE:
  Cisco CCNP Enterprise ────────────────────────────────
  Advanced routing, switching, SD-WAN, automation
  
  Juniper JNCIS-ENT ────────────────────────────────────
  Juniper-focused; common in ISP environments
  
  AWS/Azure/GCP Networking Specialty ──────────────────
  Cloud networking: VPC, load balancers, CDN, VPN

ADVANCED:
  Cisco CCIE (Expert) ──────────────────────────────────
  8-hour practical lab exam; most prestigious in networking
  Requires years of experience
  
  Certified Ethical Hacker (CEH) / OSCP ───────────────
  Security-focused; penetration testing, network attacks

SECURITY-FOCUSED:
  CompTIA Security+ ── CISSP ── CISM ── CEH ── OSCP
```

---

# 🔨 Appendix D — Projects and Code Templates

## Project 1: Network Scanner (Python)

```python
"""
network_scanner.py
Scans local network and identifies active hosts
Demonstrates IP addressing, ICMP, and ARP concepts
"""
import subprocess
import socket
import ipaddress
from concurrent.futures import ThreadPoolExecutor
import platform

def ping_host(ip):
    """Send ICMP ping to check if host is alive."""
    # -c 1 (Linux/Mac) or -n 1 (Windows) = one ping only
    # -W 1 (Linux) or -w 500 (Windows) = 1 second timeout
    system = platform.system()
    
    if system == "Windows":
        cmd = ["ping", "-n", "1", "-w", "500", str(ip)]
    else:
        cmd = ["ping", "-c", "1", "-W", "1", str(ip)]
    
    try:
        result = subprocess.run(
            cmd,
            capture_output=True,
            timeout=2
        )
        return result.returncode == 0  # 0 = success
    except (subprocess.TimeoutExpired, subprocess.CalledProcessError):
        return False

def get_hostname(ip):
    """Try to resolve hostname for IP address (reverse DNS)."""
    try:
        return socket.gethostbyaddr(str(ip))[0]
    except socket.herror:
        return "unknown"

def scan_network(network_cidr):
    """
    Scan all IPs in a network range.
    
    Args:
        network_cidr: e.g., "192.168.1.0/24"
    """
    network = ipaddress.IPv4Network(network_cidr, strict=False)
    active_hosts = []
    
    print(f"\nScanning {network_cidr}")
    print(f"Total hosts to scan: {network.num_addresses - 2}")
    print("-" * 60)
    
    # Use thread pool for parallel scanning
    with ThreadPoolExecutor(max_workers=50) as executor:
        # Map ping_host to all IPs in network (excluding network/broadcast)
        results = list(executor.map(ping_host, network.hosts()))
    
    # Collect active hosts
    for ip, is_alive in zip(network.hosts(), results):
        if is_alive:
            hostname = get_hostname(ip)
            active_hosts.append((str(ip), hostname))
            print(f"  ALIVE  {str(ip):<18} ({hostname})")
    
    print(f"\nFound {len(active_hosts)} active hosts")
    return active_hosts

def get_my_network():
    """Find the local network automatically."""
    # Connect to 8.8.8.8 (doesn't actually send data)
    # Just to find which interface has the default route
    s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
    try:
        s.connect(("8.8.8.8", 80))
        local_ip = s.getsockname()[0]
    finally:
        s.close()
    
    # Assume /24 subnet (common for home networks)
    parts = local_ip.split(".")
    network = f"{parts[0]}.{parts[1]}.{parts[2]}.0/24"
    return local_ip, network

if __name__ == "__main__":
    my_ip, my_network = get_my_network()
    print(f"Your IP: {my_ip}")
    print(f"Your network: {my_network}")
    
    # Scan local network
    hosts = scan_network(my_network)
    
    print("\n=== Active Hosts Summary ===")
    for ip, hostname in sorted(hosts):
        print(f"  {ip:<20} {hostname}")
```

---

## Project 2: Simple HTTP Server with Protocol Inspection

```python
"""
http_server.py
A minimal HTTP server showing how HTTP works at the protocol level
Run with: python http_server.py
Then visit: http://localhost:8080
"""
import socket
import threading
import datetime

def handle_client(conn, addr):
    """Handle one HTTP request — shows raw protocol exchange."""
    try:
        # Receive the raw HTTP request
        raw_request = conn.recv(4096).decode('utf-8')
        
        if not raw_request:
            return
        
        # Parse the request line
        lines = raw_request.split('\r\n')
        request_line = lines[0]  # e.g., "GET / HTTP/1.1"
        method, path, version = request_line.split(' ', 2)
        
        # Parse headers
        headers = {}
        for line in lines[1:]:
            if ':' in line:
                key, value = line.split(':', 1)
                headers[key.strip()] = value.strip()
        
        print(f"\n[{addr[0]}] {method} {path}")
        print(f"  User-Agent: {headers.get('User-Agent', 'unknown')}")
        
        # Prepare response based on path
        if path == '/':
            body = f"""<!DOCTYPE html>
<html>
<head><title>Protocol Demo Server</title></head>
<body>
  <h1>HTTP Protocol Demo</h1>
  <p>You connected from: {addr[0]}:{addr[1]}</p>
  <p>Request method: {method}</p>
  <p>Server time: {datetime.datetime.now().isoformat()}</p>
  <p>Try: <a href="/headers">Your Headers</a> | <a href="/status/404">404 Page</a></p>
</body>
</html>"""
            status = "200 OK"
            content_type = "text/html"
        
        elif path == '/headers':
            # Show all request headers
            header_html = "\n".join([f"<tr><td>{k}</td><td>{v}</td></tr>" 
                                     for k, v in headers.items()])
            body = f"""<!DOCTYPE html>
<html><body>
  <h1>Your Request Headers</h1>
  <table border="1">
    <tr><th>Header</th><th>Value</th></tr>
    {header_html}
  </table>
</body></html>"""
            status = "200 OK"
            content_type = "text/html"
        
        elif path == '/api/time':
            import json
            body = json.dumps({
                "time": datetime.datetime.now().isoformat(),
                "client_ip": addr[0]
            })
            status = "200 OK"
            content_type = "application/json"
        
        else:
            body = f"<html><body><h1>404 Not Found</h1><p>{path}</p></body></html>"
            status = "404 Not Found"
            content_type = "text/html"
        
        # Build and send HTTP response
        response = f"HTTP/1.1 {status}\r\n"
        response += f"Content-Type: {content_type}; charset=utf-8\r\n"
        response += f"Content-Length: {len(body.encode('utf-8'))}\r\n"
        response += f"Server: PythonDemo/1.0\r\n"
        response += f"Date: {datetime.datetime.utcnow().strftime('%a, %d %b %Y %H:%M:%S GMT')}\r\n"
        response += f"Connection: close\r\n"
        response += f"\r\n"  # blank line separates headers from body
        response += body
        
        conn.sendall(response.encode('utf-8'))
    
    except Exception as e:
        print(f"Error handling {addr}: {e}")
    finally:
        conn.close()

def start_server(host='0.0.0.0', port=8080):
    """Start the HTTP server."""
    server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    server.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
    server.bind((host, port))
    server.listen(5)
    
    print(f"HTTP server listening on http://localhost:{port}")
    print(f"Try in browser: http://localhost:{port}")
    print(f"Try: curl -v http://localhost:{port}/api/time")
    print("Press Ctrl+C to stop\n")
    
    try:
        while True:
            conn, addr = server.accept()
            # Handle each client in separate thread
            thread = threading.Thread(target=handle_client, args=(conn, addr))
            thread.daemon = True
            thread.start()
    except KeyboardInterrupt:
        print("\nServer stopped")
    finally:
        server.close()

if __name__ == "__main__":
    start_server()
```

---

## Project 3: DNS Resolver (Demonstrates Protocol Internals)

```python
"""
dns_demo.py
Demonstrates DNS resolution process and record types
"""
import socket
import subprocess
import time

def resolve_dns(domain, record_type='A', dns_server='8.8.8.8'):
    """
    Use the OS to resolve DNS (shows the result of full resolution).
    For learning: also shows the query time.
    """
    start = time.perf_counter()
    
    try:
        if record_type == 'A':
            # Standard IPv4 lookup
            ip = socket.gethostbyname(domain)
            elapsed = (time.perf_counter() - start) * 1000
            return f"{domain} A → {ip} ({elapsed:.1f}ms)"
        
        elif record_type == 'AAAA':
            # IPv6 lookup
            results = socket.getaddrinfo(domain, None, socket.AF_INET6)
            ipv6 = results[0][4][0] if results else "No AAAA record"
            elapsed = (time.perf_counter() - start) * 1000
            return f"{domain} AAAA → {ipv6} ({elapsed:.1f}ms)"
        
    except socket.gaierror as e:
        return f"{domain} → Error: {e}"

def dig_lookup(domain, record_type='A'):
    """Run dig command to show detailed DNS information."""
    try:
        result = subprocess.run(
            ['dig', '+noall', '+answer', f'-t{record_type}', domain],
            capture_output=True, text=True, timeout=5
        )
        return result.stdout.strip()
    except (subprocess.TimeoutExpired, FileNotFoundError):
        return "(dig not available — install bind-utils)"

def measure_dns_performance():
    """Compare DNS resolver performance."""
    test_domain = "github.com"
    dns_servers = [
        ("Google", "8.8.8.8"),
        ("Cloudflare", "1.1.1.1"),
        ("OpenDNS", "208.67.222.222"),
    ]
    
    print(f"DNS Performance Test for: {test_domain}")
    print("-" * 50)
    
    for name, server in dns_servers:
        # Flush cache effect by using unique domains each time
        start = time.perf_counter()
        try:
            socket.gethostbyname(test_domain)
        except socket.gaierror:
            pass
        elapsed = (time.perf_counter() - start) * 1000
        print(f"  {name:12} ({server}): {elapsed:6.1f}ms")

def demonstrate_dns_records():
    """Show different DNS record types for various domains."""
    print("\n=== DNS Record Types Demo ===\n")
    
    domains = ["github.com", "google.com", "cloudflare.com"]
    
    for domain in domains:
        print(f"\n{domain}:")
        print(f"  A record:   {resolve_dns(domain, 'A')}")
        print(f"  AAAA record:{resolve_dns(domain, 'AAAA')}")
        
        # MX records (need dig)
        print(f"  MX records (mail servers):")
        mx = dig_lookup(domain, 'MX')
        for line in mx.split('\n')[:3]:
            if line.strip():
                print(f"    {line.strip()}")

if __name__ == "__main__":
    demonstrate_dns_records()
    print("\n" + "="*50)
    measure_dns_performance()
```

---

## Project 4: TLS Certificate Inspector

```python
"""
tls_inspector.py
Connect to HTTPS servers and inspect their TLS configuration
"""
import ssl
import socket
import datetime

def inspect_tls(hostname, port=443):
    """
    Connect to a server and inspect its TLS certificate and configuration.
    """
    print(f"\n{'='*60}")
    print(f"TLS Inspection: {hostname}:{port}")
    print(f"{'='*60}")
    
    # Create SSL context with modern security settings
    context = ssl.create_default_context()
    
    try:
        with socket.create_connection((hostname, port), timeout=10) as sock:
            with context.wrap_socket(sock, server_hostname=hostname) as ssock:
                
                # TLS Protocol Version
                print(f"\n📋 TLS Protocol: {ssock.version()}")
                
                # Cipher Suite being used
                cipher = ssock.cipher()
                print(f"🔐 Cipher Suite: {cipher[0]}")
                print(f"   Protocol:     {cipher[1]}")
                print(f"   Key bits:     {cipher[2]}")
                
                # Server Certificate Details
                cert = ssock.getpeercert()
                
                print(f"\n📜 Certificate Details:")
                
                # Subject (who is this cert for?)
                subject = dict(x[0] for x in cert['subject'])
                print(f"   Subject: {subject.get('commonName', 'N/A')}")
                
                # Issuer (who signed this cert?)
                issuer = dict(x[0] for x in cert['issuer'])
                print(f"   Issuer: {issuer.get('organizationName', 'N/A')}")
                
                # Validity period
                not_before = ssl.cert_time_to_seconds(cert['notBefore'])
                not_after = ssl.cert_time_to_seconds(cert['notAfter'])
                
                now = datetime.datetime.utcnow().timestamp()
                days_remaining = int((not_after - now) / 86400)
                
                print(f"   Valid from: {cert['notBefore']}")
                print(f"   Valid until: {cert['notAfter']}")
                
                if days_remaining > 30:
                    status = "✅ VALID"
                elif days_remaining > 0:
                    status = "⚠️  EXPIRING SOON"
                else:
                    status = "❌ EXPIRED"
                    
                print(f"   Status: {status} ({days_remaining} days remaining)")
                
                # SANs (Subject Alternative Names)
                sans = cert.get('subjectAltName', [])
                if sans:
                    print(f"\n🌐 Subject Alternative Names (SANs):")
                    for san_type, san_value in sans[:5]:
                        print(f"   {san_value}")
                    if len(sans) > 5:
                        print(f"   ... and {len(sans)-5} more")
    
    except ssl.SSLCertVerificationError as e:
        print(f"❌ Certificate Verification Failed: {e}")
    except ssl.SSLError as e:
        print(f"❌ TLS Error: {e}")
    except ConnectionRefusedError:
        print(f"❌ Connection refused to {hostname}:{port}")
    except socket.timeout:
        print(f"❌ Connection timed out")

def compare_tls_configs(hostnames):
    """Compare TLS configurations across multiple hosts."""
    print("\n📊 TLS Configuration Comparison")
    print(f"{'Host':<30} {'TLS Version':<12} {'Cipher':<45} {'Days Left'}")
    print("-" * 100)
    
    context = ssl.create_default_context()
    
    for hostname in hostnames:
        try:
            with socket.create_connection((hostname, 443), timeout=5) as sock:
                with context.wrap_socket(sock, server_hostname=hostname) as ssock:
                    cert = ssock.getpeercert()
                    cipher = ssock.cipher()
                    version = ssock.version()
                    
                    not_after = ssl.cert_time_to_seconds(cert['notAfter'])
                    days = int((not_after - datetime.datetime.utcnow().timestamp()) / 86400)
                    
                    print(f"{hostname:<30} {version:<12} {cipher[0]:<45} {days}")
        except Exception as e:
            print(f"{hostname:<30} Error: {e}")

if __name__ == "__main__":
    # Individual inspection
    sites = ["github.com", "cloudflare.com", "google.com"]
    for site in sites:
        inspect_tls(site)
    
    # Comparison table
    compare_tls_configs(sites)
```

---

## Project 5: Simple Chat Application (TCP Networking)

```python
"""
chat_server.py / chat_client.py
Demonstrates TCP socket programming, connection handling, and protocol design

Run server: python chat.py server
Run clients: python chat.py client <nickname>
"""
import socket
import threading
import sys
import datetime

# ── SERVER ──────────────────────────────────────────────────────────────────

class ChatServer:
    def __init__(self, host='0.0.0.0', port=9999):
        self.host = host
        self.port = port
        self.clients = {}  # socket → nickname
        self.lock = threading.Lock()
    
    def broadcast(self, message, sender_socket=None):
        """Send message to all connected clients except sender."""
        timestamp = datetime.datetime.now().strftime("%H:%M:%S")
        full_msg = f"[{timestamp}] {message}\n"
        
        with self.lock:
            for client_socket in list(self.clients.keys()):
                if client_socket != sender_socket:
                    try:
                        client_socket.sendall(full_msg.encode())
                    except BrokenPipeError:
                        # Client disconnected
                        self.remove_client(client_socket)
    
    def remove_client(self, client_socket):
        """Remove a disconnected client."""
        nickname = self.clients.pop(client_socket, "unknown")
        try:
            client_socket.close()
        except:
            pass
        return nickname
    
    def handle_client(self, client_socket, addr):
        """Handle messages from one client."""
        # First message = nickname
        try:
            nickname = client_socket.recv(1024).decode().strip()
            with self.lock:
                self.clients[client_socket] = nickname
            
            print(f"[+] {nickname} joined from {addr[0]}:{addr[1]}")
            self.broadcast(f"*** {nickname} has joined the chat ***")
            
            # Receive messages in a loop
            while True:
                data = client_socket.recv(4096).decode()
                if not data:
                    break  # Client disconnected
                
                message = data.strip()
                if message:
                    print(f"  {nickname}: {message}")
                    self.broadcast(f"{nickname}: {message}", client_socket)
        
        except (ConnectionResetError, BrokenPipeError):
            pass
        finally:
            nickname = self.remove_client(client_socket)
            print(f"[-] {nickname} disconnected")
            self.broadcast(f"*** {nickname} has left the chat ***")
    
    def start(self):
        """Start the chat server."""
        server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        server.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
        server.bind((self.host, self.port))
        server.listen(10)
        
        print(f"Chat server started on port {self.port}")
        print(f"Connect with: python chat.py client <nickname>")
        
        try:
            while True:
                client_socket, addr = server.accept()
                thread = threading.Thread(
                    target=self.handle_client,
                    args=(client_socket, addr)
                )
                thread.daemon = True
                thread.start()
        except KeyboardInterrupt:
            print("\nServer shutting down")
        finally:
            server.close()

# ── CLIENT ──────────────────────────────────────────────────────────────────

class ChatClient:
    def __init__(self, nickname, host='localhost', port=9999):
        self.nickname = nickname
        self.host = host
        self.port = port
        self.socket = None
    
    def receive_messages(self):
        """Background thread: continuously receive and display messages."""
        while True:
            try:
                data = self.socket.recv(4096).decode()
                if not data:
                    print("\nDisconnected from server")
                    break
                print(data, end='', flush=True)
            except (ConnectionResetError, OSError):
                break
    
    def connect(self):
        """Connect to server and start chatting."""
        self.socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        
        try:
            self.socket.connect((self.host, self.port))
        except ConnectionRefusedError:
            print(f"Cannot connect to {self.host}:{self.port}")
            print("Is the server running? Start with: python chat.py server")
            return
        
        # Send nickname first
        self.socket.sendall(f"{self.nickname}\n".encode())
        
        print(f"Connected as '{self.nickname}'. Type messages and press Enter.")
        print("Press Ctrl+C to quit\n")
        
        # Start receive thread
        recv_thread = threading.Thread(target=self.receive_messages)
        recv_thread.daemon = True
        recv_thread.start()
        
        # Main thread: send messages
        try:
            while True:
                message = input()
                if message.strip():
                    self.socket.sendall(f"{message}\n".encode())
        except (KeyboardInterrupt, EOFError):
            print("\nDisconnecting...")
        finally:
            self.socket.close()

# ── MAIN ────────────────────────────────────────────────────────────────────

if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage:")
        print("  python chat.py server")
        print("  python chat.py client <nickname>")
        sys.exit(1)
    
    mode = sys.argv[1].lower()
    
    if mode == "server":
        server = ChatServer()
        server.start()
    
    elif mode == "client":
        if len(sys.argv) < 3:
            nickname = input("Enter your nickname: ")
        else:
            nickname = sys.argv[2]
        
        client = ChatClient(nickname)
        client.connect()
    
    else:
        print(f"Unknown mode: {mode}")
```

---

## 🔧 Troubleshooting Guide

| Problem | Diagnosis Steps | Solution |
|---------|-----------------|---------|
| Cannot ping 8.8.8.8 | ping 192.168.1.1 (router) | Router reachable → ISP issue; not → local network issue |
| Can ping IP, can't browse | nslookup google.com | DNS failure; change DNS to 8.8.8.8 |
| Slow internet | traceroute google.com | Find which hop is slow; speedtest.net for bandwidth |
| SSL/HTTPS errors | curl -v https://site | Certificate expired/invalid; check system time |
| Port not reachable | telnet host port | Service not running or firewall blocking |
| "Connection refused" | netstat -tlnp \| grep port | Check if service is listening |
| "No route to host" | ip route show | Check routing table; default route configured? |

---

## 📚 Appendix E — Resources

### Books
| Book | Author | Level |
|------|--------|-------|
| *Computer Networks* | Tanenbaum & Wetherall | Beginner–Advanced |
| *TCP/IP Illustrated Vol. 1* | W. Richard Stevens | Intermediate–Advanced |
| *High Performance Browser Networking* | Ilya Grigorik (free online) | Intermediate |
| *Network Programmability and Automation* | Edelman et al. | Advanced |
| *QUIC and HTTP/3* | Robin Marx (online) | Advanced |

### Online Resources
| Resource | URL | Content |
|----------|-----|---------|
| RFC Editor | rfc-editor.org | Official protocol specifications |
| Cloudflare Blog | blog.cloudflare.com | Excellent technical networking articles |
| IETF | ietf.org | Working groups on future protocols |
| PacketLife | packetlife.net | Cheat sheets, Wireshark captures |
| Julia Evans | jvns.ca | Networking explained accessibly |
| High Performance Browser Networking | hpbn.co | Free online book (must read) |

### Tools Reference
| Tool | Platform | Install |
|------|---------|---------|
| Wireshark | All | wireshark.org |
| nmap | All | nmap.org |
| curl | All | curl.se |
| dig | Linux/Mac | `apt install dnsutils` / `brew install bind` |
| mtr | Linux/Mac | `apt install mtr` |
| iperf3 | All | `apt install iperf3` |
| tcpdump | Linux/Mac | `apt install tcpdump` |

---

