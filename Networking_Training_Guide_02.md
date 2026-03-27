# Computer Architecture: Networking
## Comprehensive Training Guide 



---

## 📋 Table of Contents

1. [Prerequisites & Quick Start](#prerequisites)
2. [Module 2.3 — IP Addressing & Network Topology](#module-23)
   - Assignment 1: Draw Your Home Network
   - IPv4 vs. IPv6
   - Subnetting Basics
   - Network Address Translation (NAT)
3. [Module 2.4 — Wireless and Wired Networks](#module-24)
   - Wired vs. Wireless Comparison
   - WiFi, Ethernet, and Emerging Technologies
   - Powerline and Optical Fiber
4. [Module 2.5 — Network Security](#module-25)
   - Assignment 2: Security Challenges
   - Basic Security Measures
   - Firewalls and VPNs
5. [Glossary](#glossary)
6. [Quick Reference Cheat Sheets](#cheatsheets)
7. [Project Ideas](#projects)
8. [Interview Questions](#interview)
9. [Certifications & Next Steps](#certifications)

---

## 🚀 Prerequisites & Quick Start {#prerequisites}

### Prerequisites Checklist

Before you begin, you need:

- [ ] A computer (Windows, Mac, or Linux — any will work)
- [ ] Basic understanding of what the internet is (you use it daily!)
- [ ] Curiosity and willingness to learn
- [ ] No programming experience required



### Tools You Will Use (All Free)

| Tool | Purpose | Where to Get It |
|------|---------|----------------|
| Draw.io / diagrams.net | Network diagrams | app.diagrams.net |
| Wireshark | Packet analysis (Day 3) | wireshark.org |
| ipconfig / ifconfig | Check your IP address | Built into your OS |
| ping | Test connectivity | Built into your OS |
| tracert / traceroute | Trace network paths | Built into your OS |
| Cisco Packet Tracer | Network simulation | netacad.com (free) |

---

---

# MODULE 2.3: IP Addressing, Subnetting & NAT {#module-23}

## 🎯 Learning Objectives

By the end of Module 2.3, you will be able to:

- Draw and explain a home network topology with all its components
- Explain the difference between IPv4 and IPv6, and why IPv6 matters
- Perform basic subnetting calculations without breaking a sweat
- Explain what NAT does and why every home router uses it

---

## Assignment 1: Draw Your Home Network Topology

### Introduction

Every network — from your home Wi-Fi to the internet itself — has a *topology*, which is simply the arrangement of devices and how they connect. Before learning advanced concepts, mapping your own home network builds an intuitive understanding that makes everything else click into place.

This assignment trains you to see the invisible: the cables, signals, and addresses that make your devices communicate. It also introduces you to the vocabulary of networking that professionals use every day.

Think of your home network like a neighborhood. Each house has an address (IP address), roads connect the houses (cables and Wi-Fi), and a post office (router) routes letters between your neighborhood and the outside world (the internet).

### What Is a Network Topology?

A **network topology** is a map showing:
- **Devices** (nodes): computers, phones, TVs, printers, smart speakers
- **Connections** (links): Ethernet cables, Wi-Fi signals, fiber lines
- **Network equipment**: routers, switches, access points, modems

### Common Topology Types

```
STAR TOPOLOGY (Most Home Networks)
         
         [Laptop]   [Phone]
             \         /
     [TV]----[ROUTER]----[Smart Speaker]
             /         \
         [PC]       [Tablet]

All devices connect to one central point (the router).
Pros: Easy to add devices, one failure doesn't break others.
Cons: If the router fails, everything goes down.

─────────────────────────────────────────────────────────

BUS TOPOLOGY (Old-style, rarely used today)

[PC1]───[PC2]───[PC3]───[PC4]───[PC5]
   └──────────────────────────────┘
         One shared cable

Pros: Simple, cheap.
Cons: One break kills everything, slow with many devices.

─────────────────────────────────────────────────────────

MESH TOPOLOGY (Enterprise / Advanced Home)

[PC1]───[PC2]
  │  ╲ ╱  │
  │   ╳   │
  │  ╱ ╲  │
[PC3]───[PC4]

Every device connects to every other device.
Pros: Extremely reliable, multiple paths.
Cons: Expensive, complex.

─────────────────────────────────────────────────────────

RING TOPOLOGY (Older Token Ring networks)

[PC1]──[PC2]
  │         │
[PC4]──[PC3]

Data travels in one direction around the ring.
```

### How a Typical Home Network Looks

```
INTERNET (The Big Cloud)
       │
       │ (Fiber / Cable / DSL line from ISP)
       │
  ┌────┴────┐
  │  MODEM  │  ← Converts ISP signal to Ethernet
  └────┬────┘
       │ (Ethernet cable)
  ┌────┴────┐
  │  ROUTER │  ← Assigns IP addresses, routes traffic
  └──┬──┬───┘
     │  │
     │  └──────────────────── Wi-Fi Signal ────────────────────┐
     │                                                          │
  ┌──┴──┐                                                       │
  │SWITCH│  ← Optional: adds more Ethernet ports          [Phones]
  └──┬───┘                                               [Tablets]
     │                                                   [Laptops]
  ┌──┴────────────┐
  │               │
[Desktop PC]  [Smart TV]   [Printer]
(via Ethernet)
```

### Step-by-Step: How to Draw Your Home Network

**Step 1: Inventory your devices**

Walk around your home and list every device that connects to the internet. Common devices:

| Device Type | Examples |
|------------|---------|
| Computers | Desktop PC, Laptop, MacBook |
| Mobile | iPhone, Android phone, iPad, Kindle |
| Entertainment | Smart TV, Roku, Chromecast, PlayStation, Xbox |
| Smart Home | Alexa, Google Home, smart bulbs, Ring doorbell |
| Network Equipment | Router, modem, Wi-Fi extenders, switches |

**Step 2: Identify connection types**

For each device, note how it connects:
- **Wired (Ethernet)**: Device has a cable plugged into it
- **Wireless (Wi-Fi)**: Device connects without cables
- **Powerline**: Adapters plugged into electrical outlets

**Step 3: Find your router/modem**

Usually found near where the internet cable enters your home. In many homes today, the modem and router are combined into one device from your ISP.

**Step 4: Draw the diagram**

Use symbols:
```
  ☁  = Internet / Cloud
  ◻  = Router
  ◼  = Switch  
  ○  = Computer / Laptop
  📱 = Phone / Tablet
  📺 = Smart TV / Streaming device
  🖨️ = Printer
  ──  = Wired connection (Ethernet cable)
  ~~  = Wireless connection (Wi-Fi)
```

### Sample Home Network Diagram (Annotated)

```
        ☁ INTERNET (Your ISP: Comcast, AT&T, etc.)
              │
              │ Fiber/Cable comes into your home
              │
    ┌─────────┴──────────┐
    │   MODEM/ROUTER     │  IP from ISP: 103.45.67.89 (Public IP)
    │   (Combined Unit)  │  Your home devices see: 192.168.1.x (Private)
    └──┬──────┬──────────┘
       │      │
       │      │ Wi-Fi (2.4GHz and 5GHz bands)
       │      │
  Ethernet    ├──── 📱 iPhone        (192.168.1.101)
  (Cat6)      ├──── 📱 Android Phone (192.168.1.102)
       │      ├──── 💻 Laptop        (192.168.1.103)
       │      └──── 📺 Smart TV      (192.168.1.104)
       │
  ┌────┴────┐
  │  SWITCH │  (Unmanaged 5-port switch)
  └──┬──┬───┘
     │  │
     │  └──── 🖨️ Printer    (192.168.1.201)
     │
     └──── 🖥️ Desktop PC   (192.168.1.200)
```

### ✏️ Assignment 1 — Your Deliverable

Complete the following:

1. **Draw your home network** using the symbols above (paper or Draw.io)
2. **Label each device** with its name and connection type
3. **Write a brief explanation** covering:
   - How many devices are connected?
   - Which are wired, which are wireless?
   - What is your router's local IP address? (Check: 192.168.1.1 or 192.168.0.1 in a browser)
   - What topology type does your home use?

**Bonus Challenge**: Use the `ipconfig` (Windows) or `ifconfig` (Mac/Linux) command in your terminal/command prompt to find your computer's IP address and write it on your diagram.

```bash
# Windows — open Command Prompt and type:
ipconfig

# Look for "IPv4 Address" under your network adapter
# Example output:
# IPv4 Address. . . . . . . . . . . : 192.168.1.100
# Subnet Mask . . . . . . . . . . . : 255.255.255.0
# Default Gateway . . . . . . . . . : 192.168.1.1
```

---

## IPv4 vs. IPv6

### Introduction

IP addresses are like street addresses for devices on a network. Without them, data packets would have no idea where to go. The internet has used two versions of the IP addressing system: IPv4 (the original) and IPv6 (the modern upgrade). Understanding their differences is essential for anyone working with networks today.

The world is currently in a transition period between IPv4 and IPv6. Many networks run both simultaneously (called "dual stack"). Knowing why IPv6 was created and how it works prepares you for the future of networking.

Think of IPv4 addresses like a city with a fixed number of street addresses. When the city grew too large, they had to invent a new, much larger addressing system — that's IPv6.

### IPv4 — The Original Address System

**Format**: Four groups of numbers separated by dots
```
Example: 192.168.1.100
         │   │   │ │
         │   │   │ └── Host number (device on the network)
         │   │   └──── Network part
         │   └──────── Network part
         └──────────── Network part
```

Each group is called an **octet** (8 bits), ranging from 0 to 255.

**Total IPv4 addresses**: About 4.3 billion (2³²)

> **The Problem**: With smartphones, smart TVs, IoT devices, and billions of people online, 4.3 billion addresses ran out. The internet faced an address shortage crisis.

### IPv4 Address Classes (The Original Organization)

```
CLASS A: 1.0.0.0 – 126.255.255.255
┌────────────────────────────────────────────────────────┐
│ Network (8 bits) │     Host (24 bits)                  │
│   1 – 126        │     16 million hosts per network     │
│ Used by: Large corporations, ISPs (IBM: 9.x.x.x)       │
└────────────────────────────────────────────────────────┘

CLASS B: 128.0.0.0 – 191.255.255.255
┌────────────────────────────────────────────────────────┐
│ Network (16 bits)     │ Host (16 bits)                  │
│ 128.0 – 191.255       │ 65,534 hosts per network        │
│ Used by: Universities, medium organizations             │
└────────────────────────────────────────────────────────┘

CLASS C: 192.0.0.0 – 223.255.255.255
┌────────────────────────────────────────────────────────┐
│ Network (24 bits)          │ Host (8 bits)              │
│ 192.0.0 – 223.255.255      │ 254 hosts per network      │
│ Used by: Small businesses, home networks ← YOU ARE HERE │
└────────────────────────────────────────────────────────┘
```

### Special IPv4 Addresses

| Address Range | Purpose |
|--------------|---------|
| 10.0.0.0 – 10.255.255.255 | Private network (home/office) |
| 172.16.0.0 – 172.31.255.255 | Private network |
| 192.168.0.0 – 192.168.255.255 | Private network (most home routers) |
| 127.0.0.1 | Loopback (your own computer — "localhost") |
| 255.255.255.255 | Broadcast (send to ALL devices) |
| 0.0.0.0 | Unspecified / default route |

### IPv6 — The Modern Solution

**Why IPv6 was created**: IPv4 could only support ~4.3 billion addresses. The internet needed more.

**IPv6 provides**: 340 undecillion addresses (340,000,000,000,000,000,000,000,000,000,000,000,000)

**Format**: Eight groups of four hexadecimal digits separated by colons

```
Full IPv6 address:
2001:0db8:85a3:0000:0000:8a2e:0370:7334
 │    │    │    │    │    │    │    │
 │    │    │    │    │    │    │    └── 16 bits (group 8)
 │    │    │    │    │    │    └─────── 16 bits (group 7)
 │    │    │    │    │    └──────────── 16 bits (group 6)
 │    │    │    │    └───────────────── 16 bits (group 5)
 │    │    │    └────────────────────── 16 bits (group 4)
 │    │    └─────────────────────────── 16 bits (group 3)
 │    └──────────────────────────────── 16 bits (group 2)
 └───────────────────────────────────── 16 bits (group 1)

Shorthand (compress leading zeros and consecutive zero groups):
2001:db8:85a3::8a2e:370:7334
             ││
             └─ :: means one or more groups of all zeros
```

### IPv4 vs. IPv6 Side-by-Side Comparison

```
┌──────────────────┬─────────────────────┬─────────────────────────┐
│ Feature          │ IPv4                │ IPv6                    │
├──────────────────┼─────────────────────┼─────────────────────────┤
│ Address Length   │ 32 bits             │ 128 bits                │
│ Address Format   │ Dotted decimal      │ Hexadecimal with colons │
│ Example          │ 192.168.1.1         │ 2001:db8::1             │
│ Total Addresses  │ ~4.3 billion        │ ~340 undecillion        │
│ Header Size      │ 20-60 bytes         │ Fixed 40 bytes          │
│ Configuration    │ Manual or DHCP      │ Auto-config (SLAAC)     │
│ Security         │ Optional (IPSec)    │ Built-in (IPSec)        │
│ NAT Required?    │ Yes (address saver) │ No (enough addresses)   │
│ Broadcast        │ Yes                 │ No (uses multicast)     │
│ Fragmentation    │ Routers and hosts   │ Sending host only       │
│ Adoption (2024)  │ ~60% of traffic     │ ~40% of traffic         │
└──────────────────┴─────────────────────┴─────────────────────────┘
```

### Real-World: Checking Your IPv6 Address

```bash
# Windows
ipconfig
# Look for "IPv6 Address" — starts with 2001: or fe80:

# Mac / Linux
ifconfig
# or
ip addr show

# Check online (visits a website that shows your IPs):
# Visit: https://whatismyipaddress.com
# You may see BOTH an IPv4 and IPv6 address if your ISP supports IPv6
```

### 💡 Pro Tip: The Transition Is Happening Now

As of 2024, Google reports over 45% of its traffic comes over IPv6. Your ISP may already give you an IPv6 address alongside your IPv4 address. The two systems run side-by-side in what's called **dual-stack** mode. You don't have to choose — they coexist.

### ⚠️ Common Mistakes

- **Confusing private and public IPs**: Your router's address (192.168.x.x) is private and only works inside your home network. Your public IP is assigned by your ISP and is what the internet sees.
- **Thinking IPv6 is just a bigger IPv4**: IPv6 also includes security, auto-configuration, and quality-of-service improvements.
- **Ignoring the loopback address (127.0.0.1)**: This special address always points to your own computer. "Can you ping yourself?" is a common diagnostic question.

### 🏋️ Exercise: IP Address Identification

Classify each of the following IP addresses:

1. `192.168.0.1` — What class? Public or private?
2. `8.8.8.8` — What is this address? (Hint: Google)
3. `127.0.0.1` — What special purpose does this serve?
4. `2001:4860:4860::8888` — IPv4 or IPv6? (This is Google's DNS too!)
5. `10.0.0.1` — Public or private?

**Answers**:
1. Class C, Private (your home router likely uses this)
2. Google's public DNS server, Public IPv4
3. Loopback address — your own computer
4. IPv6 — Google's DNS in IPv6 format
5. Private (Class A private range)

---

## Subnetting Basics

### Introduction

Subnetting is the practice of dividing a large network into smaller, more manageable sub-networks (subnets). It's one of the most important skills in networking, and it's also the topic that intimidates beginners the most — but it doesn't have to.

Think of subnetting like dividing an apartment building. The building has one street address (the network address), but each apartment has its own unit number (the host address). A subnet is like a floor of the building — it groups related apartments together.

Subnetting is used to organize networks, improve performance, and add security by keeping different parts of a network separated from each other.

### Why Subnet?

```
WITHOUT SUBNETTING:
┌────────────────────────────────────────────────────────┐
│  Company network: 192.168.1.0/24 (254 addresses)       │
│                                                        │
│  HR, Finance, Engineering, and Sales all on ONE network│
│  → Security risk: HR can "see" Engineering computers   │
│  → Performance: All broadcast traffic hits every device│
└────────────────────────────────────────────────────────┘

WITH SUBNETTING:
┌──────────────────────────┐  ┌──────────────────────────┐
│  HR Subnet               │  │  Finance Subnet           │
│  192.168.1.0/26          │  │  192.168.1.64/26          │
│  (62 usable addresses)   │  │  (62 usable addresses)    │
└──────────────────────────┘  └──────────────────────────┘
┌──────────────────────────┐  ┌──────────────────────────┐
│  Engineering Subnet      │  │  Sales Subnet             │
│  192.168.1.128/26        │  │  192.168.1.192/26         │
│  (62 usable addresses)   │  │  (62 usable addresses)    │
└──────────────────────────┘  └──────────────────────────┘
  → Departments can't directly communicate without going through a router
  → Better security, better performance, cleaner organization
```

### The Subnet Mask: Your Key Tool

A subnet mask tells devices which part of an IP address is the **network** and which part is the **host**.

**Dotted Decimal Format** (human-readable):
```
IP Address:  192.168.1.100
Subnet Mask: 255.255.255.0
             ─────────────────
             Network │ Host
             (first 3)│(last octet)
```

**CIDR Notation** (modern, compact format):
```
192.168.1.100/24
             └── /24 means 24 bits are the network part
                 (same as subnet mask 255.255.255.0)
```

### Common Subnet Masks Reference Table

```
┌──────────┬─────────────────┬────────────┬──────────────────────┐
│ CIDR     │ Subnet Mask     │ # of Hosts │ Use Case             │
├──────────┼─────────────────┼────────────┼──────────────────────┤
│ /8       │ 255.0.0.0       │ 16,777,214 │ Very large companies │
│ /16      │ 255.255.0.0     │ 65,534     │ Large companies      │
│ /24      │ 255.255.255.0   │ 254        │ Home / small office  │
│ /25      │ 255.255.255.128 │ 126        │ Split /24 in half    │
│ /26      │ 255.255.255.192 │ 62         │ Small department     │
│ /27      │ 255.255.255.224 │ 30         │ Small team           │
│ /28      │ 255.255.255.240 │ 14         │ Tiny group           │
│ /30      │ 255.255.255.252 │ 2          │ Router-to-router link│
│ /32      │ 255.255.255.255 │ 1          │ Single host (no subnet)│
└──────────┴─────────────────┴────────────┴──────────────────────┘
```

> **Formula for usable hosts**: 2^(32 - CIDR) - 2
> The "- 2" removes the Network Address (all zeros) and Broadcast Address (all ones)

### Subnetting Step-by-Step Example

**Goal**: Subnet 192.168.10.0/24 into 4 equal subnets

**Step 1**: Determine how many bits we need to borrow
- We need 4 subnets → 2² = 4 → borrow 2 bits
- New prefix: /24 + 2 = /26

**Step 2**: Calculate the "block size" (how many addresses per subnet)
- Block size = 256 ÷ 4 = 64 addresses per subnet

**Step 3**: List the subnets

```
Subnet 1: 192.168.10.0/26
  Network address:   192.168.10.0    (unusable — identifies the network)
  First usable host: 192.168.10.1
  Last usable host:  192.168.10.62
  Broadcast:         192.168.10.63   (unusable — sends to all devices)
  Usable hosts: 62

Subnet 2: 192.168.10.64/26
  Network address:   192.168.10.64
  First usable host: 192.168.10.65
  Last usable host:  192.168.10.126
  Broadcast:         192.168.10.127
  Usable hosts: 62

Subnet 3: 192.168.10.128/26
  Network address:   192.168.10.128
  First usable host: 192.168.10.129
  Last usable host:  192.168.10.190
  Broadcast:         192.168.10.191
  Usable hosts: 62

Subnet 4: 192.168.10.192/26
  Network address:   192.168.10.192
  First usable host: 192.168.10.193
  Last usable host:  192.168.10.254
  Broadcast:         192.168.10.255
  Usable hosts: 62
```

**Visual representation**:
```
192.168.10.0                                        192.168.10.255
│                                                              │
├──────────┬──────────┬──────────┬──────────────────────────┤
│ Subnet 1 │ Subnet 2 │ Subnet 3 │ Subnet 4                 │
│ /26      │ /26      │ /26      │ /26                      │
│ .0–.63   │ .64–.127 │ .128–.191│ .192–.255                │
└──────────┴──────────┴──────────┴──────────────────────────┘
```

### Binary and Subnetting (The "Why Behind the Math")

IP addresses are actually binary numbers. Subnetting manipulates these bits.

```
192.168.1.100 in binary:

192  = 11000000
168  = 10101000
  1  = 00000001
100  = 01100100

Full binary: 11000000.10101000.00000001.01100100

Subnet mask /24 = 11111111.11111111.11111111.00000000
                  ─────────────────────────── ────────
                  Network part (24 ones)      Host part
```

The subnet mask acts like a filter: wherever there's a `1` in the mask, that bit belongs to the **network**. Wherever there's a `0`, that bit belongs to the **host**.

### 💡 Pro Tips for Subnetting

1. **Memorize the powers of 2**: 2, 4, 8, 16, 32, 64, 128, 256. These are your block sizes.
2. **The magic number trick**: 256 minus the last non-255 octet of the mask = block size
   - Mask 255.255.255.192 → 256 - 192 = 64 (block size is 64)
3. **Practice with small numbers first**: Work with /25, /26, /27 before trying /19 or /20
4. **Use online calculators to check your work**: subnet-calculator.com or jodies.de/ipcalc

### 🏋️ Subnetting Exercise

Given the network `10.0.0.0/24`, create 8 subnets. For each subnet, write the:
- Network address
- First usable host
- Last usable host
- Broadcast address

(Hint: 8 subnets from /24 means borrowing 3 bits → /27, block size = 32)

**Solution** (Subnet 1 shown, complete the rest):
```
Subnet 1: 10.0.0.0/27
  Network:   10.0.0.0
  First:     10.0.0.1
  Last:      10.0.0.30
  Broadcast: 10.0.0.31

Subnet 2: 10.0.0.32/27  (starts at 32 because block size = 32)
  Network:   10.0.0.32
  First:     10.0.0.33
  ...continue for all 8 subnets...
```

---

## Network Address Translation (NAT)

### Introduction

NAT is one of the most important inventions in the history of networking. Without it, the internet would have run out of IPv4 addresses years before it actually did. NAT allows an entire network of devices — your home with 20 devices — to share a single public IP address when communicating with the internet.

Imagine you work in an office building. The building has one street address, but hundreds of employees work inside. When someone sends a letter to the building, the receptionist (NAT) looks at which department (port number) it's addressed to and routes it to the right person. When someone inside sends a letter out, the receptionist puts the building's return address (public IP) on it, not the individual employee's desk number.

NAT is why you can have a phone, laptop, tablet, and smart TV — all with different internal addresses — appearing to the internet as a single public IP address.

### How NAT Works: Step by Step

```
YOUR HOME NETWORK                    INTERNET
─────────────────                    ────────
                    ┌───────────┐
📱 Phone             │           │           ┌─────────┐
192.168.1.101:49001 ─┤   NAT     │           │ Google  │
                    │  ROUTER   │──────────▶│ Server  │
💻 Laptop            │           │           │ 142.250 │
192.168.1.102:49002 ─┤           │           └─────────┘
                    │ Public IP:│
🖥️  Desktop          │ 103.45.67.89
192.168.1.103:49003 ─┤           │
                    └───────────┘

Step 1: Your phone (192.168.1.101) requests google.com
Step 2: Router records the translation in its NAT table:
        Internal IP:Port → External IP:Port
        192.168.1.101:49001 → 103.45.67.89:49001

Step 3: Router sends the request to Google using its PUBLIC IP
Step 4: Google responds to 103.45.67.89:49001
Step 5: Router looks up its NAT table, finds 192.168.1.101, delivers to phone
```

### The NAT Translation Table

The router keeps a table in memory tracking all active connections:

```
┌──────────────────┬─────────┬────────────────┬────────────┬────────┐
│ Inside Local     │ Inside  │ Outside Global │ Outside    │ Proto  │
│ (Private IP:Port)│ Global  │ (Router IP)    │ Local      │        │
├──────────────────┼─────────┼────────────────┼────────────┼────────┤
│ 192.168.1.101:   │ 103.45. │ 103.45.67.89:  │ 142.250.   │ TCP    │
│ 49001            │ 67.89   │ 49001          │ 185.68:443 │        │
├──────────────────┼─────────┼────────────────┼────────────┼────────┤
│ 192.168.1.102:   │ 103.45. │ 103.45.67.89:  │ 52.86.12.  │ TCP    │
│ 52341            │ 67.89   │ 52341          │ 33:80      │        │
└──────────────────┴─────────┴────────────────┴────────────┴────────┘
```

### Types of NAT

**1. Static NAT** — One-to-one mapping
```
Private IP 192.168.1.10 ←──always──→ Public IP 203.0.113.10
Private IP 192.168.1.11 ←──always──→ Public IP 203.0.113.11

Use case: Web servers that need a permanent public IP address
```

**2. Dynamic NAT** — Pool of public IPs shared as needed
```
Pool of Public IPs: 203.0.113.10 – 203.0.113.20

Device A gets  203.0.113.10 (when it connects)
Device B gets  203.0.113.11 (when it connects)
Device A done → 203.0.113.10 released back to pool
Device C gets  203.0.113.10 (reused)

Use case: Companies with multiple public IPs but more internal devices
```

**3. PAT / NAT Overload** (What your home router uses!)
```
Many private IPs → ONE public IP, differentiated by PORT NUMBER

192.168.1.101:49001 ──┐
192.168.1.102:52341 ──┼──▶ 103.45.67.89 (one IP, multiple ports)
192.168.1.103:61234 ──┘

Use case: Home networks, small offices — most common NAT type
```

### NAT: Benefits and Limitations

```
┌─────────────────────────────────┬──────────────────────────────────┐
│ BENEFITS                        │ LIMITATIONS                      │
├─────────────────────────────────┼──────────────────────────────────┤
│ ✅ Address conservation         │ ❌ Breaks end-to-end connectivity │
│    Thousands of devices share   │    Devices behind NAT can't be   │
│    one public IP                │    directly reached from outside  │
│                                 │                                  │
│ ✅ Security by obscurity        │ ❌ Complicates P2P applications   │
│    External hosts can't         │    Gaming, video calls, torrents │
│    directly reach internal IPs  │    need workarounds (UPnP, STUN) │
│                                 │                                  │
│ ✅ Flexibility                  │ ❌ Not true security              │
│    Change internal addressing   │    NAT alone ≠ firewall           │
│    without changing public IP   │                                  │
│                                 │                                  │
│ ✅ Hides network structure      │ ❌ Adds processing overhead       │
│    ISP and hackers can't see    │    Router must maintain table     │
│    your internal layout         │    and translate every packet     │
└─────────────────────────────────┴──────────────────────────────────┘
```

### Port Forwarding: Punching Through NAT

When you run a game server or web server at home, external users can't reach you because NAT hides you. **Port forwarding** creates a static rule in your router:

```
Rule: "All traffic on port 25565 → forward to 192.168.1.100"

INTERNET ──▶ Router:25565 ──▶ 192.168.1.100:25565 (Minecraft Server)

Without port forwarding: External connection blocked by NAT
With port forwarding: Router knows exactly where to send it
```

You can configure port forwarding in your router's admin interface (usually at 192.168.1.1).

### ⚠️ Common Mistakes with NAT

- **"NAT is a firewall"**: NAT provides some incidental security but is NOT a true firewall. Always use a proper firewall too.
- **"NAT is going away with IPv6"**: True — IPv6 has enough addresses that NAT isn't needed. But NAT will be around for many years during the IPv4/IPv6 transition.
- **Forgetting port forwarding when hosting servers**: If your game server or web app isn't reachable, check port forwarding first.

### 🏋️ NAT Exercise

A home router has the public IP `78.62.15.200`. Three devices are connected:
- Device A: `192.168.0.10` visiting YouTube on port `51234`
- Device B: `192.168.0.20` visiting Google on port `62901`
- Device C: `192.168.0.30` downloading a file on port `44112`

**Question**: Draw the NAT translation table that the router would maintain.

**Answer**:
```
┌─────────────────┬──────────────────┬─────────────────┐
│ Internal        │ External         │ Destination      │
├─────────────────┼──────────────────┼─────────────────┤
│ 192.168.0.10:   │ 78.62.15.200:    │ YouTube:443      │
│ 51234           │ 51234            │                  │
├─────────────────┼──────────────────┼─────────────────┤
│ 192.168.0.20:   │ 78.62.15.200:    │ Google:443       │
│ 62901           │ 62901            │                  │
├─────────────────┼──────────────────┼─────────────────┤
│ 192.168.0.30:   │ 78.62.15.200:    │ File server:80   │
│ 44112           │ 44112            │                  │
└─────────────────┴──────────────────┴─────────────────┘
```

---

## Module 2.3 Quick Reference Cheat Sheet

```
╔══════════════════════════════════════════════════════════════╗
║             MODULE 2.3 QUICK REFERENCE                      ║
╠══════════════════════════════════════════════════════════════╣
║ NETWORK TOPOLOGIES                                          ║
║  Star: All devices → one central router/switch             ║
║  Bus:  All devices on one cable (legacy)                   ║
║  Mesh: Every device connects to every other                ║
║  Ring: Devices form a loop                                 ║
╠══════════════════════════════════════════════════════════════╣
║ PRIVATE IP RANGES                                           ║
║  10.0.0.0/8         (Class A private)                      ║
║  172.16.0.0/12      (Class B private)                      ║
║  192.168.0.0/16     (Class C private — home networks)      ║
╠══════════════════════════════════════════════════════════════╣
║ IPv4 vs IPv6                                                ║
║  IPv4: 32 bits, dotted decimal (192.168.1.1)               ║
║  IPv6: 128 bits, hex colon (2001:db8::1)                   ║
║  IPv4 addresses: ~4.3 billion                              ║
║  IPv6 addresses: 340 undecillion                           ║
╠══════════════════════════════════════════════════════════════╣
║ SUBNETTING QUICK FORMULA                                    ║
║  Usable hosts = 2^(32-prefix) - 2                         ║
║  /24 → 254 hosts   /25 → 126 hosts   /26 → 62 hosts       ║
║  /27 → 30 hosts    /28 → 14 hosts    /30 → 2 hosts        ║
╠══════════════════════════════════════════════════════════════╣
║ NAT TYPES                                                   ║
║  Static NAT:   1 private IP ↔ 1 public IP                 ║
║  Dynamic NAT:  pool of public IPs shared                   ║
║  PAT (Overload): MANY private IPs → 1 public IP (home NAT)║
╚══════════════════════════════════════════════════════════════╝
```

---

---

# MODULE 2.4: Wireless and Wired Networks {#module-24}

## 🎯 Learning Objectives

By the end of Module 2.4, you will be able to:

- Explain the key differences between wired and wireless networking
- Describe the specifications and use cases for different WiFi standards
- Explain how Ethernet works and choose the right cable category
- Describe powerline networking and fiber optic communication
- Identify emerging networking technologies and their applications

---

## Wired vs. Wireless Networking

### Introduction

The choice between wired and wireless networking isn't just about convenience. It involves tradeoffs in speed, reliability, security, and cost. Understanding both technologies helps you make the right choice for different situations — and in modern networks, both types almost always coexist.

Consider this: a hospital's critical monitoring equipment runs on wired Ethernet because reliability is non-negotiable. But the same hospital has Wi-Fi for nurses' tablets and visitor phones. Both technologies serve different needs in the same building.

As you design networks — even your home network — understanding these tradeoffs helps you make better decisions about which devices should be wired and which can be wireless.

### Head-to-Head Comparison

```
┌─────────────────┬─────────────────────────┬─────────────────────────┐
│ Characteristic  │ WIRED (Ethernet)        │ WIRELESS (Wi-Fi)        │
├─────────────────┼─────────────────────────┼─────────────────────────┤
│ Speed           │ Up to 100 Gbps          │ Up to 46 Gbps (Wi-Fi 7) │
│                 │ (typically 1 Gbps home) │ (typically 600 Mbps)    │
├─────────────────┼─────────────────────────┼─────────────────────────┤
│ Latency         │ Very low (1-5ms)        │ Higher (5-50ms+)        │
│                 │ Excellent for gaming    │ Variable, less consistent│
├─────────────────┼─────────────────────────┼─────────────────────────┤
│ Reliability     │ Very high               │ Affected by interference│
│                 │ No interference         │ walls, microwaves, etc. │
├─────────────────┼─────────────────────────┼─────────────────────────┤
│ Security        │ High                    │ Lower (signals radiate) │
│                 │ Physical access needed  │ Can be intercepted      │
├─────────────────┼─────────────────────────┼─────────────────────────┤
│ Mobility        │ None (physically tethered)│ Full (move anywhere)  │
├─────────────────┼─────────────────────────┼─────────────────────────┤
│ Setup Cost      │ Higher (cables, patching)│ Lower (no cable runs)  │
├─────────────────┼─────────────────────────┼─────────────────────────┤
│ Capacity        │ Per port (dedicated)    │ Shared among users      │
├─────────────────┼─────────────────────────┼─────────────────────────┤
│ Best For        │ Gaming, NAS, desktops,  │ Phones, tablets, laptops│
│                 │ printers, servers       │ IoT devices, guests     │
└─────────────────┴─────────────────────────┴─────────────────────────┘
```

### Decision Flowchart: Wired or Wireless?

```
Start: New device to connect to the network
              │
              ▼
  Does the device MOVE (phone, tablet, laptop)?
         │              │
        YES             NO
         │              │
         ▼              ▼
   Use WIRELESS    Does it need low latency?
                   (gaming, video calls, servers)
                         │              │
                        YES             NO
                         │              │
                         ▼              ▼
                    Use WIRED      Is there a cable port
                                   near the device?
                                         │              │
                                        YES             NO
                                         │              │
                                         ▼              ▼
                                    Use WIRED    Consider powerline
                                               adapter OR wireless
```

### When to Use Each

**Use Wired Ethernet for:**
- Desktop computers (they don't move)
- Gaming consoles (PlayStation, Xbox — lower latency wins games)
- Smart TVs and streaming devices (if they have an Ethernet port)
- Network-attached storage (NAS) — for fast backup/file transfer
- Servers and printers
- IP cameras in fixed locations

**Use Wireless Wi-Fi for:**
- Smartphones and tablets (must be wireless)
- Laptops that move between rooms
- IoT devices (smart plugs, sensors)
- Guest networks
- Devices too far from the router for cable routing

---

## WiFi, Ethernet, and Emerging Technologies

### The Evolution of WiFi Standards

WiFi standards are defined by the IEEE (Institute of Electrical and Electronics Engineers) and named 802.11 followed by a letter. The Wi-Fi Alliance has also introduced friendlier "Wi-Fi X" marketing names.

```
WIFI STANDARDS TIMELINE
═══════════════════════

1997  ┤ 802.11    ─── 2 Mbps    2.4 GHz   (The beginning)
      │
1999  ┤ 802.11b   ─── 11 Mbps   2.4 GHz   (First mainstream WiFi)
      │
1999  ┤ 802.11a   ─── 54 Mbps   5 GHz     (Faster but shorter range)
      │
2003  ┤ 802.11g   ─── 54 Mbps   2.4 GHz   (Replaced 802.11b)
      │
2009  ┤ 802.11n   ─── 600 Mbps  2.4/5 GHz (Wi-Fi 4 — first dual-band)
      │
2013  ┤ 802.11ac  ─── 3.5 Gbps  5 GHz     (Wi-Fi 5 — gigabit WiFi)
      │
2019  ┤ 802.11ax  ─── 9.6 Gbps  2.4/5 GHz (Wi-Fi 6 — current standard)
      │
2021  ┤ 802.11ax  ─── 9.6 Gbps  6 GHz     (Wi-Fi 6E — adds 6 GHz band)
      │
2024  ┤ 802.11be  ─── 46 Gbps   2.4/5/6GHz(Wi-Fi 7 — latest)
```

### Understanding WiFi Frequencies

WiFi operates on different frequency bands, and choosing the right one matters:

```
2.4 GHz BAND
┌─────────────────────────────────────────────────┐
│ ● Longer range (travels further, through walls) │
│ ● Slower speeds                                  │
│ ● More interference (microwaves, Bluetooth,     │
│   neighbors' WiFi, baby monitors all use 2.4GHz)│
│ ● Only 3 non-overlapping channels (1, 6, 11)    │
│ Best for: IoT devices, devices far from router  │
└─────────────────────────────────────────────────┘

5 GHz BAND
┌─────────────────────────────────────────────────┐
│ ● Shorter range (walls absorb signal more)      │
│ ● Much faster speeds                            │
│ ● Less interference (fewer devices use it)      │
│ ● 23 non-overlapping channels                   │
│ Best for: Streaming, gaming, close devices      │
└─────────────────────────────────────────────────┘

6 GHz BAND (Wi-Fi 6E and Wi-Fi 7 only)
┌─────────────────────────────────────────────────┐
│ ● Shortest range (needs line of sight almost)   │
│ ● Fastest speeds                                │
│ ● Almost zero interference (brand new band)     │
│ ● 59 non-overlapping channels                   │
│ Best for: VR headsets, 8K streaming, AR         │
└─────────────────────────────────────────────────┘
```

### WiFi 6 (802.11ax) — The Current King

Wi-Fi 6 introduced major improvements beyond just speed:

**OFDMA (Orthogonal Frequency Division Multiple Access)**
```
Old Wi-Fi (one device at a time):
Router: ──────[Device A]──────[Device B]──────[Device C]──────

Wi-Fi 6 with OFDMA (multiple devices simultaneously):
Router: ──[A][B][C]──[A][B][C]──[A][B][C]──
        All 3 served in same time slot!
```

**MU-MIMO (Multi-User, Multiple Input Multiple Output)**
```
Wi-Fi 4/5: Router has "conversations" one at a time
           ┌────────────────────────┐
           │  Router: "Hey A, your  │
           │          turn. Now B.  │
           │          Now C."       │
           └────────────────────────┘

Wi-Fi 6: Router has simultaneous conversations
           ┌────────────────────────┐
           │  Router antenna 1 → A  │
           │  Router antenna 2 → B  │
           │  Router antenna 3 → C  │
           │  (all at same time!)   │
           └────────────────────────┘
```

**BSS Coloring** — Reduces interference from neighboring networks
```
Your network and neighbor's on same channel:
Without BSS Coloring: Devices get confused, pause, retry → SLOW
With BSS Coloring: Packets labeled with a color (network ID)
                   Devices ignore traffic from different colored networks
```

### Ethernet — The Backbone of Wired Networking

Ethernet is the standard technology for wired local area networks. It was invented at Xerox PARC in 1973 and has been the dominant LAN technology ever since.

### Ethernet Cable Categories

```
ETHERNET CABLE COMPARISON
═════════════════════════

Cat5
├── Max speed: 100 Mbps
├── Bandwidth: 100 MHz
├── Max length: 100 meters
└── Status: Obsolete (don't buy)

Cat5e (e = enhanced)
├── Max speed: 1 Gbps
├── Bandwidth: 100 MHz (better noise rejection)
├── Max length: 100 meters
└── Status: Still common in older installations

Cat6
├── Max speed: 1 Gbps (10 Gbps up to 55m)
├── Bandwidth: 250 MHz
├── Max length: 100 meters (55m for 10Gbps)
├── Physical difference: Thicker, has internal divider
└── Status: Current standard for new installations

Cat6a (a = augmented)
├── Max speed: 10 Gbps
├── Bandwidth: 500 MHz
├── Max length: 100 meters (full 10Gbps)
├── Physical difference: Even thicker, usually shielded
└── Status: Recommended for new buildings

Cat7
├── Max speed: 10 Gbps+
├── Bandwidth: 600 MHz
├── Requires different connectors (not standard RJ45)
└── Status: Niche use, often skipped in favor of Cat6a

Cat8
├── Max speed: 25-40 Gbps
├── Bandwidth: 2000 MHz
├── Max length: 30 meters
└── Status: Data centers only
```

### How Ethernet Works: The CSMA/CD Process

**CSMA/CD** = Carrier Sense Multiple Access / Collision Detection

```
STEP 1: Device wants to send data
        "Is anyone else talking on the network?"
                │
        YES     ▼    NO
        Wait    OK to send data
                │
        STEP 2: Send the data frame
                │
        STEP 3: Listen for collisions
                Did two devices send at the same time?
                │              │
               YES             NO
                │              │
         STEP 4: Both stop     Data received successfully ✓
         Send JAM signal
         Wait random time
         Try again from Step 1
```

> **Modern Ethernet switches eliminate most collisions** by creating dedicated paths between sender and receiver. CSMA/CD is mostly a legacy concept now, but understanding it explains why Ethernet was designed the way it was.

### Ethernet Frame Structure

When data travels over Ethernet, it's wrapped in a "frame" — like putting a letter in an envelope with address info:

```
ETHERNET FRAME
═══════════════

 ┌──────────┬──────────┬──────┬──────────────┬─────┐
 │Preamble  │Dest. MAC │Src.  │  DATA        │ FCS │
 │(8 bytes) │(6 bytes) │MAC   │(46-1500 bytes│(4B) │
 │          │          │(6B)  │              │     │
 └──────────┴──────────┴──────┴──────────────┴─────┘
      │           │       │          │           │
   Sync        Where    Where     Actual       Error
  signal      it goes  it's      payload     check
              (MAC     from
             address) (MAC
                      address)
```

### MAC Addresses — The Hardware Identity

While IP addresses are logical (they can change), **MAC addresses** are physical identifiers burned into network hardware:

```
MAC Address Example: 00:1A:2B:3C:4D:5E
                     ──────── ────────
                     OUI      Device ID
                     (Vendor  (Unique to
                     code)    this device)

OUI Examples:
  00:1A:2B = Cisco Systems
  00:50:56 = VMware
  F4:5C:89 = Apple
  DC:A6:32 = Raspberry Pi Foundation
```

MAC addresses are used for **local** delivery (within your network). IP addresses are used for **global** routing (across the internet). They work together — ARP (Address Resolution Protocol) translates between them.

### Emerging Technologies in Networking

### Wi-Fi 7 (802.11be) — Just Released

Wi-Fi 7 represents a significant leap forward:

```
Wi-Fi 7 Key Features:
┌─────────────────────────────────────────────────────────┐
│ Multi-Link Operation (MLO)                              │
│   Device connects to 2.4GHz + 5GHz + 6GHz simultaneously│
│   Picks fastest path for each packet                    │
│   ↓ 40% lower latency than Wi-Fi 6                      │
├─────────────────────────────────────────────────────────┤
│ 320 MHz Channel Width                                   │
│   Double the channel width of Wi-Fi 6                   │
│   More data per transmission                            │
├─────────────────────────────────────────────────────────┤
│ 4096-QAM                                                │
│   Packs more data into each signal                      │
│   (Wi-Fi 6 used 1024-QAM)                              │
├─────────────────────────────────────────────────────────┤
│ Max Speed: 46 Gbps (theoretical)                        │
│ Real-world: 2–5 Gbps (still a major improvement)       │
└─────────────────────────────────────────────────────────┘
```

### 5G — The Wireless Revolution for Everything

5G is not just "faster 4G." It's a new architecture with different modes:

```
5G MODES:
                        
Sub-6 GHz (Sub-6)       mmWave (millimeter wave)
─────────────────       ────────────────────────
Range: Miles            Range: Hundreds of feet
Speed: ~1 Gbps          Speed: 10+ Gbps
Penetration: Good       Penetration: Poor (blocked by glass)
Coverage: Wide area     Coverage: Dense urban only
Use case: Most 5G       Use case: Stadiums, airports, downtown

5G Key Specs vs Previous Generations:
┌────────────────┬─────────┬────────┬────────┐
│ Feature        │ 3G      │ 4G LTE │ 5G     │
├────────────────┼─────────┼────────┼────────┤
│ Peak Download  │ 7 Mbps  │100 Mbps│10 Gbps │
│ Latency        │ 100ms   │ 30ms   │ <1ms   │
│ Connections/km²│ 100k    │ 100k   │ 1M     │
└────────────────┴─────────┴────────┴────────┘
```

---

## Powerline and Optical Fiber Communication

### Powerline Networking — Internet Through Your Electrical Outlets

Powerline adapters are a clever solution when you can't run Ethernet cables and Wi-Fi signal is too weak.

### How Powerline Works

```
YOUR HOME ELECTRICAL WIRING

Electrical outlet in living room          Electrical outlet in bedroom
       │                                              │
  ┌────┴─────┐    Electrical wiring    ┌──────────────┴─────┐
  │ Powerline│══════════════════════════│ Powerline           │
  │ Adapter 1│ (data signal piggybacks  │ Adapter 2           │
  └────┬─────┘  on electrical current) └──────┬──────────────┘
       │                                       │
  Ethernet to Router                     Ethernet to TV/PC

Data travels through your home's electrical wires!
No new cables needed — uses wires already in the walls.
```

### Powerline Adapter Setup

```
SETUP STEPS:
┌──────────────────────────────────────────────────────┐
│ 1. Plug Adapter 1 into outlet near your router       │
│ 2. Connect Adapter 1 to router with Ethernet cable   │
│ 3. Plug Adapter 2 into outlet near your target device│
│ 4. Connect Adapter 2 to device with Ethernet cable   │
│ 5. Press pairing buttons (first-time setup only)     │
│ Done! Network extends through electrical wiring.     │
└──────────────────────────────────────────────────────┘
```

### Powerline Pros, Cons, and Real-World Tips

```
┌────────────────────────────┬───────────────────────────────┐
│ ADVANTAGES                 │ DISADVANTAGES                 │
├────────────────────────────┼───────────────────────────────┤
│ ✅ No new cable runs needed │ ❌ Speed varies wildly by home │
│ ✅ Works through walls      │    (old wiring = slow speeds) │
│ ✅ Better than Wi-Fi for    │ ❌ Doesn't cross circuit      │
│    distant rooms            │    breakers (rooms on different│
│ ✅ Plug-and-play easy       │    circuits may not connect)  │
│ ✅ Speeds up to 2 Gbps     │ ❌ Power strips degrade signal │
│    (AV2 standard)           │    (plug into wall directly)  │
│ ✅ Great for smart TVs      │ ❌ Electrical noise interferes │
│    and gaming consoles      │ ❌ Not as fast as real Ethernet│
└────────────────────────────┴───────────────────────────────┘

💡 Pro Tip: Always plug powerline adapters directly into wall 
outlets, NEVER into surge protectors or power strips. The 
filtering in power strips blocks the data signal.
```

### Powerline Standards

| Standard | Max Speed | Notes |
|---------|-----------|-------|
| HomePlug 1.0 | 14 Mbps | Very old, obsolete |
| HomePlug AV | 200 Mbps | Still found in older homes |
| HomePlug AV2 | 500 Mbps – 1 Gbps | Current standard |
| G.hn | Up to 2 Gbps | Newest, less common |

### MoCA — Data Through Coaxial Cable

If your home has coaxial cable (for cable TV), **MoCA** (Multimedia over Coax Alliance) adapters work similarly to powerline but are faster and more reliable:

- Speeds up to 2.5 Gbps
- Very low latency
- Not affected by electrical noise
- Popular with TiVo and Verizon FiOS users

---

### Optical Fiber — Light Speed Networking

Fiber optic cables transmit data as **pulses of light** rather than electrical signals. This is the technology behind the fastest internet connections on earth and the backbone of the internet itself.

### How Fiber Optics Work

```
HOW LIGHT CARRIES DATA THROUGH FIBER

Light pulse = 1 (data bit)
No light   = 0 (data bit)

Light source          Fiber optic cable            Receiver
(LED or Laser) ──▶ ═══════════════════════════ ──▶ (Photodetector)
                   │    Glass or plastic core   │
                   │   ↗ Total internal         │
                   │     reflection keeps        │
                   │     light bouncing          │
                   │     along the cable ↘       │
                   └─────────────────────────────┘

Data travels at roughly 2/3 the speed of light!
That's about 200,000 km per second.
```

### Types of Fiber Optic Cable

```
SINGLE-MODE FIBER (SMF)
┌──────────────────────────────────────────────────────────┐
│ Core diameter: 8-10 micrometers (width of a human hair!) │
│ Light path: Straight through the center (single mode)   │
│ Range: Up to 80 km (100km+ with amplifiers)              │
│ Speed: 100 Gbps+ per wavelength                          │
│ Cost: More expensive (requires laser light source)        │
│ Color coding: Yellow jacket typically                    │
│ Use case: Long-distance, between cities, ISP backbones   │
└──────────────────────────────────────────────────────────┘

MULTI-MODE FIBER (MMF)
┌──────────────────────────────────────────────────────────┐
│ Core diameter: 50 or 62.5 micrometers                    │
│ Light path: Multiple paths, some bounce (multiple modes) │
│ Range: Up to 2 km (400m for higher speeds)               │
│ Speed: 10-100 Gbps                                       │
│ Cost: Less expensive (LED light source works)            │
│ Color coding: Orange or aqua jacket                      │
│ Use case: Buildings, data centers, campus networks       │
└──────────────────────────────────────────────────────────┘
```

### Types of Fiber Internet Service

```
FIBER TO THE HOME / PREMISES DEPLOYMENT

ISP Central Office ──fiber──▶ Neighborhood ──fiber──▶ Your Home
                                                      (FTTH/FTTP)
                                           ↕ copper last mile
                              Your Home                (FTTN - slower)

FTTH/FTTP  = Fiber To The Home/Premises  (fastest, pure fiber all the way)
FTTB       = Fiber To The Building       (fiber to apt building)
FTTN       = Fiber To The Node/Cabinet  (fiber + copper last mile, slower)
HFC        = Hybrid Fiber-Coax           (cable internet — fiber backbone + coax)
```

### Fiber vs. Copper vs. Wireless Comparison

```
┌───────────────┬──────────────┬──────────────┬──────────────┐
│ Technology    │ Fiber Optic  │ Copper (Cat) │ Wireless     │
├───────────────┼──────────────┼──────────────┼──────────────┤
│ Max Speed     │ 100+ Tbps    │ 40 Gbps      │ 46 Gbps      │
│               │ (theoretical)│ (Cat8)       │ (Wi-Fi 7)    │
├───────────────┼──────────────┼──────────────┼──────────────┤
│ Max Distance  │ 80 km        │ 100 m        │ 100-300 m    │
│               │ (SMF)        │              │ (indoors)    │
├───────────────┼──────────────┼──────────────┼──────────────┤
│ Latency       │ Very low     │ Very low     │ Higher       │
├───────────────┼──────────────┼──────────────┼──────────────┤
│ Interference  │ None         │ EMI          │ High         │
│               │ (immune)     │ interference │              │
├───────────────┼──────────────┼──────────────┼──────────────┤
│ Security      │ Very High    │ High         │ Lower        │
│               │ Hard to tap  │              │              │
├───────────────┼──────────────┼──────────────┼──────────────┤
│ Cost          │ High         │ Medium       │ Low-Medium   │
│               │ (installation)│              │              │
├───────────────┼──────────────┼──────────────┼──────────────┤
│ Weight/Size   │ Very light,  │ Heavy, bulky │ N/A          │
│               │ thin         │              │              │
└───────────────┴──────────────┴──────────────┴──────────────┘
```

### The Internet's Backbone: Submarine Cables

Most internet traffic between continents travels through undersea fiber optic cables:

```
GLOBAL SUBMARINE CABLE NETWORK (simplified)

  North America ═══════════════════════════════════ Europe
       ║                                               ║
       ║                                               ║
       ║═════════════════════════════════════════════ Middle East
       ║                                               ║
  South America ══════════════════════════════════ Africa ═ Asia
                                                          ║
                                                    Australia

Key facts:
• Over 500 active submarine cable systems
• Total length: Over 1.3 million km of cables
• Each cable carries 100+ Tbps of data
• A single cable cut can disrupt an entire region's internet
• Sharks have been known to bite fiber cables (they detect electrical fields)
```

### Emerging Technology: Li-Fi (Light Fidelity)

Li-Fi is an experimental technology that uses **visible light** from LED lamps to transmit data:

```
LI-FI CONCEPT
              💡 LED Light (flickers faster than human eye can see)
              │
    ┌─────────┴──────────┐
    │   Data encoded in   │
    │   light pulses      │  ← Rate: billions per second
    │   (on/off = 1/0)   │
    └─────────┬──────────┘
              │ Light travels to device
              ▼
          📱 Phone with Li-Fi receiver

Claimed speeds: Up to 224 Gbps (laboratory)
Real-world: 1-10 Gbps

Advantages:
  ✅ Cannot penetrate walls (more secure)
  ✅ No radio interference
  ✅ Huge bandwidth potential

Disadvantages:
  ❌ Requires line-of-sight
  ❌ Blocked by anything that blocks light
  ❌ Not widely available
  ❌ Sunlight interference outdoors
```

### Module 2.4 Quick Reference Cheat Sheet

```
╔══════════════════════════════════════════════════════════════╗
║             MODULE 2.4 QUICK REFERENCE                      ║
╠══════════════════════════════════════════════════════════════╣
║ WIFI STANDARDS QUICK GUIDE                                  ║
║  Wi-Fi 4 (802.11n):  600 Mbps, 2.4/5 GHz, 2009            ║
║  Wi-Fi 5 (802.11ac): 3.5 Gbps, 5 GHz, 2013                ║
║  Wi-Fi 6 (802.11ax): 9.6 Gbps, 2.4/5 GHz, 2019            ║
║  Wi-Fi 6E:           9.6 Gbps, adds 6 GHz band, 2021       ║
║  Wi-Fi 7 (802.11be): 46 Gbps, all 3 bands, 2024            ║
╠══════════════════════════════════════════════════════════════╣
║ ETHERNET CABLE GUIDE                                        ║
║  Cat5e:  1 Gbps, 100m — minimum for new installs           ║
║  Cat6:   10 Gbps/55m, 1 Gbps/100m — recommended            ║
║  Cat6a:  10 Gbps/100m — best for future-proofing           ║
╠══════════════════════════════════════════════════════════════╣
║ FIBER TYPES                                                 ║
║  Single-mode (yellow):  Long distance, 80km+               ║
║  Multi-mode (orange):   Short distance, buildings           ║
╠══════════════════════════════════════════════════════════════╣
║ FREQUENCY BANDS                                             ║
║  2.4 GHz: Long range, slower, more interference            ║
║  5 GHz:   Medium range, faster, less interference          ║
║  6 GHz:   Short range, fastest, almost no interference     ║
╚══════════════════════════════════════════════════════════════╝
```

---

---

# MODULE 2.5: Network Security {#module-25}

## 🎯 Learning Objectives

By the end of Module 2.5, you will be able to:

- Identify the most common network security threats and how they work
- Explain how firewalls filter traffic using rules
- Describe how VPNs protect data using encryption and tunneling
- Apply basic security best practices to your home or small office network
- Complete Assignment 2 with a comprehensive understanding of network security fundamentals

---

## Assignment 2: Introduction to Network Security Challenges

### Introduction

Network security is not just for large corporations. Every connected device — your smartphone, your home router, your smart TV — is a potential target. The global cost of cybercrime reached $8 trillion in 2023 and is projected to reach $10.5 trillion by 2025.

But security isn't just about attacks and defenses. It's about understanding the fundamental challenges that arise when systems communicate: How do you verify who someone is? How do you keep data private? How do you ensure data hasn't been tampered with? These questions have driven decades of innovation in networking security.

This module gives you the foundation to understand why security measures work the way they do, and how to make informed decisions about protecting networks — starting with your own home.

### The Security Triad: CIA

All of network security revolves around three core goals, abbreviated as **CIA**:

```
THE CIA TRIAD

          Confidentiality
               ╱▲╲
              ╱  │  ╲
             ╱   │   ╲
            ╱    │    ╲
           ╱─────┼─────╲
          ╱      │      ╲
  Integrity ─────┼───── Availability
                 │
       The three pillars of security

CONFIDENTIALITY: Data is only accessible to authorized parties
  Example: Your bank account details are encrypted in transit
  Attack: Eavesdropping, man-in-the-middle

INTEGRITY: Data is not modified without authorization
  Example: Files you download are checksummed (MD5/SHA256)
  Attack: Data tampering, man-in-the-middle

AVAILABILITY: Systems are accessible when needed
  Example: Your bank's website is up 99.99% of the time
  Attack: Denial of Service (DoS), ransomware
```

### Common Network Security Threats

### 1. Man-in-the-Middle Attack (MitM)

```
NORMAL COMMUNICATION:
[You] ─────────────────────────────── [Bank Website]
         "Here's my password"

MAN-IN-THE-MIDDLE ATTACK:
[You] ──── [Hacker] ──────────────── [Bank Website]
         ↗           ↘
 Intercepts your    Forwards (modified?)
 password           to bank

How it happens:
  • Unsecured public WiFi (coffee shop attack)
  • ARP poisoning on local network
  • DNS spoofing

Prevention:
  ✅ HTTPS (look for padlock in browser)
  ✅ VPN on public WiFi
  ✅ Certificate pinning in apps
```

### 2. Denial of Service (DoS) and Distributed DoS (DDoS)

```
NORMAL TRAFFIC:
[User 1] ──┐
[User 2] ──┤──▶ [Web Server]  ← Handles requests normally
[User 3] ──┘

DoS ATTACK:
[Attacker] ──(millions of fake requests)──▶ [Web Server]  ← OVERWHELMED
                                                            Server crashes!

DDoS (Distributed) — Much Worse:
[Botnet Device 1] ──┐
[Botnet Device 2] ──┤
[Botnet Device 3] ──┼──(millions of requests)──▶ [Web Server] ← DEAD
[... 100,000     ] ──┤
[compromised PCs] ──┘

Scale: Major DDoS attacks can exceed 1 Tbps of traffic
Record: 3.47 Tbps attack (Microsoft Azure, 2021)
```

### 3. Phishing and Social Engineering

```
PHISHING ATTACK FLOW:

1. Attacker sends email:
   ┌─────────────────────────────────────────────────────┐
   │ From: security@paypa1.com (note the "1" not "l")    │
   │ Subject: URGENT: Your account has been suspended!   │
   │                                                     │
   │ Click here to verify your account immediately:      │
   │ https://paypa1.com/verify/account                   │
   └─────────────────────────────────────────────────────┘

2. Victim clicks link → Goes to fake website

3. Fake website looks identical to real PayPal

4. Victim enters credentials

5. Attacker has credentials!

Red flags to watch for:
  ❌ Urgent language creating panic
  ❌ Email domain looks slightly wrong
  ❌ Generic greeting ("Dear Customer")
  ❌ Link URL doesn't match company
  ❌ Requests sensitive info via email
```

### 4. Malware Types

```
MALWARE TAXONOMY
═════════════════

VIRUS            WORM            TROJAN
Attaches to      Self-replicates  Looks legitimate
files, needs     through          but contains
human to         networks         hidden malware
spread           alone

RANSOMWARE       SPYWARE         ROOTKIT
Encrypts         Silently         Hides itself
your files,      monitors and     deep in OS,
demands ransom   reports you      very hard to
for decryption   to attacker      detect/remove

BOTNET           KEYLOGGER
Turns your PC    Records every
into a zombie    keystroke you
that attacks     type (passwords,
others           credit cards)
```

### 5. ARP Poisoning — A Local Network Attack

```
ARP POISONING ATTACK

Normal ARP:
"Who has IP 192.168.1.1?" → Router answers: "That's MAC AA:BB:CC:DD"
All devices learn this mapping

ARP Poisoning Attack:
Attacker broadcasts: "Hey everyone! 192.168.1.1 has MAC XX:YY:ZZ:00"
(XX:YY:ZZ:00 is the attacker's MAC address!)

Now ALL traffic meant for the router goes through the attacker first!
The attacker is now a silent man-in-the-middle.

Prevention:
  ✅ Dynamic ARP Inspection on managed switches
  ✅ Static ARP entries for critical devices
  ✅ Network monitoring tools
  ✅ VLANs to isolate network segments
```

### 6. DNS Spoofing / DNS Cache Poisoning

```
NORMAL DNS PROCESS:
You type: www.mybank.com
   ▼
DNS Server: "That's 203.0.113.45"
   ▼
Your browser connects to 203.0.113.45 (real bank)

DNS SPOOFING:
Attacker poisons DNS cache:
"www.mybank.com = 10.10.10.99" (attacker's fake server!)
   ▼
You type: www.mybank.com
   ▼
Poisoned DNS: "That's 10.10.10.99"
   ▼
Your browser connects to FAKE bank! Credentials stolen!

Prevention:
  ✅ DNSSEC (DNS Security Extensions)
  ✅ DNS-over-HTTPS (DoH)
  ✅ Trusted DNS servers (8.8.8.8, 1.1.1.1)
```

### Network Security Risk Assessment Exercise

For Assignment 2, evaluate your home network using this checklist:

```
HOME NETWORK SECURITY AUDIT
════════════════════════════

ROUTER SECURITY
□ Changed default admin username/password?
□ Running latest firmware?
□ WPA3 or WPA2 encryption enabled?
□ WPS (WiFi Protected Setup) disabled?
□ Remote management disabled?
□ Guest network separate from main network?

DEVICE SECURITY
□ All devices have latest OS updates?
□ Antivirus software installed on PCs?
□ Default passwords changed on IoT devices?
□ Unnecessary services/ports closed?

NETWORK PRACTICES
□ Using HTTPS websites (padlock in browser)?
□ VPN used on public WiFi?
□ Two-factor authentication on important accounts?
□ Strong unique passwords (password manager)?

SCORE: ___/16 checks passed
12-16: Good security posture
8-11: Needs improvement
Below 8: Significant security risks
```

---

## Basic Security Measures: Firewalls

### Introduction

A firewall is a network security system that monitors and controls incoming and outgoing network traffic based on predetermined security rules. It's the gatekeeper between your trusted internal network and the untrusted external internet.

Firewalls are one of the oldest and most fundamental security tools — the concept dates to the late 1980s. Despite their age, firewalls remain essential in every security architecture.

Think of a firewall like a club bouncer: they have a list (ruleset) of who can come in and who gets turned away. No rule match? Different firewalls handle this differently — some deny by default (deny-all), others allow by default (not recommended).

### Types of Firewalls

```
FIREWALL EVOLUTION
══════════════════

GENERATION 1: PACKET FILTER (1980s-1990s)
┌─────────────────────────────────────────┐
│ Checks: Source IP, Destination IP, Port  │
│                                         │
│ Rules example:                          │
│  ALLOW TCP from ANY to 192.168.1.5:80   │
│  DENY  TCP from ANY to 192.168.1.5:22   │
│                                         │
│ Weakness: Doesn't understand connections│
│ Can't tell: new vs. established traffic │
└─────────────────────────────────────────┘

GENERATION 2: STATEFUL FIREWALL (1990s-present)
┌─────────────────────────────────────────┐
│ Tracks connection state:                │
│   NEW → ESTABLISHED → RELATED → INVALID │
│                                         │
│ Benefits:                               │
│  ✅ Allows return traffic automatically │
│  ✅ Blocks unsolicited inbound packets  │
│  ✅ Understands TCP handshakes          │
│                                         │
│ Most home/office firewalls are stateful │
└─────────────────────────────────────────┘

GENERATION 3: APPLICATION LAYER / NGFW (2000s-present)
┌─────────────────────────────────────────┐
│ Inspects actual content (Deep Packet    │
│ Inspection):                            │
│                                         │
│ Can detect:                             │
│  • "This is HTTP on port 443" (good)   │
│  • "This is malware disguised as HTTP" │
│  • Specific applications (Facebook,    │
│    Netflix, BitTorrent)                │
│  • User identity (knows it's "Bob")    │
│                                         │
│ Next-Gen Firewalls (NGFW) add:          │
│  • IPS (Intrusion Prevention System)   │
│  • SSL inspection                      │
│  • Application control                 │
│  • URL filtering                       │
└─────────────────────────────────────────┘
```

### How Firewall Rules Work

Firewall rules are processed **top to bottom** — the first matching rule wins. Order matters!

```
FIREWALL RULE TABLE EXAMPLE

Priority │ Action │ Source        │ Destination   │ Port  │ Protocol
─────────┼────────┼───────────────┼───────────────┼───────┼─────────
1        │ ALLOW  │ 192.168.1.0/24│ ANY           │ 443   │ TCP (HTTPS)
2        │ ALLOW  │ 192.168.1.0/24│ ANY           │ 80    │ TCP (HTTP)
3        │ ALLOW  │ 192.168.1.0/24│ ANY           │ 53    │ UDP (DNS)
4        │ BLOCK  │ ANY           │ 192.168.1.5   │ 22    │ TCP (SSH)
5        │ ALLOW  │ 10.0.0.5      │ 192.168.1.5   │ 22    │ TCP (SSH)
100      │ DENY   │ ANY           │ ANY           │ ANY   │ ANY (default)

Rule 4 blocks SSH from everywhere,
BUT Rule 5 should be BEFORE Rule 4!
(The admin IP 10.0.0.5 never gets to Rule 5 because Rule 4 matches first)

LESSON: ORDER YOUR RULES CAREFULLY! Specific rules before general rules.
```

### Firewall Zones

Professional firewalls use zones to organize security:

```
FIREWALL ZONE ARCHITECTURE

        INTERNET (Untrusted)
              │
              │
         ┌────┴────┐
         │FIREWALL │
         └────┬────┘
              │
    ┌─────────┼──────────┐
    │         │          │
    ▼         ▼          ▼
  DMZ        LAN       MGMT
(Semi-trust)(Trusted) (Admin only)
    │         │          │
 [Web      [PCs,     [Firewall
  Server]   Files,    Admin
 [Mail      Printers] Console]
  Server]

DMZ = DeMilitarized Zone
  • Hosts public-facing servers
  • Internet can reach DMZ servers
  • DMZ cannot directly reach LAN
  • Best of both worlds: accessible but isolated

Example: Your company website lives in DMZ
         Your employee computers live in LAN
         If the web server is hacked, attacker 
         can't easily pivot to the LAN
```

### Common Firewall Rules for Home Networks

Your home router has a built-in firewall. These are sensible default rules:

```
RECOMMENDED HOME FIREWALL RULES
═════════════════════════════════

INBOUND (from Internet to your home):
  1. BLOCK  ALL inbound (default — NAT handles this)
  2. ALLOW  specific port forwards only as needed
     (e.g., port 443 if hosting a web server)

OUTBOUND (from your home to Internet):
  1. ALLOW  80 (HTTP)
  2. ALLOW  443 (HTTPS)
  3. ALLOW  53 (DNS)
  4. ALLOW  25/465/587 (email)
  5. ALLOW  123 (NTP/time sync)
  6. CONSIDER blocking:
     • Port 23 (Telnet — unencrypted, use SSH instead)
     • Port 137-139 (NetBIOS — Windows file sharing, shouldn't leave network)
     • Outbound to known malware command-and-control IPs
```

### Host-Based vs. Network Firewalls

```
NETWORK FIREWALL                    HOST-BASED FIREWALL
(Router/Dedicated Appliance)        (On each computer)

INTERNET                            
    │                               
┌───┴───┐                           ┌─────┐  ← Windows Defender
│Router │                           │ PC  │     Firewall protects
│Firewall│                          └─────┘     this specific PC
└───┬───┘                           
    │                               ┌─────┐  ← iptables/ufw on Linux
    ├──── PC1 (protected)           │Linux│
    ├──── PC2 (protected)           └─────┘
    └──── PC3 (protected)           
                                    
Protects entire network             Protects individual device
Great for blocking Internet threats Great for blocking lateral
                                    movement within network
Both should be used together!       (Defense in Depth)
```

---

## Basic Security Measures: VPNs

### Introduction

A Virtual Private Network (VPN) creates an encrypted tunnel between your device and a VPN server, protecting your data from eavesdroppers on the local network and concealing your traffic from your ISP and websites.

VPNs were originally created for corporate remote workers to access company resources securely over the public internet — as if they were physically in the office. Today, consumer VPNs are used widely for privacy, accessing geo-restricted content, and securing connections on public WiFi.

### How a VPN Works

```
WITHOUT VPN:
Your device ──(unencrypted or ISP can see)──▶ Website
    │
    Your ISP sees: "User visited youtube.com at 9pm"
    Hackers on public WiFi can intercept traffic

WITH VPN:
Your device ──(encrypted tunnel)──▶ VPN Server ──▶ Website
    │                    │               │
    Your ISP sees:   VPN Server      Website sees:
    "User connected  decrypts,        VPN Server's
    to VPN at 9pm"   re-encrypts,     IP, not yours
    (can't see       and forwards
    where you go)

HOW THE TUNNEL IS BUILT:
1. Your device and VPN server perform cryptographic handshake
2. Session keys are exchanged (unique to this session)
3. All traffic encrypted before leaving your device
4. Encrypted data travels through internet (looks like random data)
5. VPN server decrypts, sees real destination, forwards request
6. Response travels back encrypted to you
```

### VPN Protocols — The "How" of VPN Tunneling

```
VPN PROTOCOL COMPARISON
═══════════════════════

OpenVPN
├── Type: Open source
├── Speed: Good
├── Security: Very strong (OpenSSL)
├── Port: UDP 1194 or TCP 443
├── Firewall friendly: Yes (can use port 443)
└── Best for: Desktop clients, privacy-focused use

WireGuard
├── Type: Open source, newer
├── Speed: Excellent (fastest)
├── Security: Modern cryptography (ChaCha20, Curve25519)
├── Port: UDP 51820
├── Code size: 4,000 lines (vs 400,000 for OpenVPN — easier to audit)
└── Best for: Mobile, performance-critical applications

IKEv2/IPSec
├── Type: Industry standard
├── Speed: Very good
├── Security: Strong
├── Special feature: MOBIKE — reconnects automatically when switching
│                     networks (WiFi to cellular)
└── Best for: Mobile devices, corporate use

L2TP/IPSec
├── Type: Old standard
├── Speed: Slower (double encapsulation)
├── Security: Decent when paired with IPSec
└── Best for: Legacy compatibility only

PPTP (AVOID!)
├── Type: Very old
├── Speed: Fast
├── Security: BROKEN — multiple known vulnerabilities
└── Status: Do not use! Only for compatibility with ancient systems

RECOMMENDED: WireGuard for speed, OpenVPN for compatibility
```

### VPN Architectures

```
TYPE 1: REMOTE ACCESS VPN (for individuals/remote workers)
                                                    
Employee at home ──VPN tunnel──▶ Company VPN Server ──▶ Company LAN
                                                    
   • Employee acts as if physically in the office
   • Can access internal file servers, printers, intranet
   • Most consumer VPNs work this way too

─────────────────────────────────────────────────────────────────

TYPE 2: SITE-TO-SITE VPN (connecting office branches)

 NYC Office                           London Office
┌──────────┐                          ┌──────────┐
│ 10.1.0.0 │──VPN tunnel over Internet│ 10.2.0.0 │
│  /24     │══════════════════════════│  /24     │
│  devices │                          │  devices │
└──────────┘                          └──────────┘

   • Permanent tunnel between two networks
   • Users in both offices can reach each other's resources
   • Appears as one big network, logically

─────────────────────────────────────────────────────────────────

TYPE 3: SPLIT TUNNELING

Regular traffic  ──────────────────────────────▶ Netflix (direct)
VPN tunnel traffic ──▶ VPN Server ──────────────▶ Work resources

   • Only some traffic goes through VPN
   • Local internet traffic goes direct (faster, lower latency)
   • Work traffic is protected
   • Saves VPN bandwidth
```

### Consumer VPN: Practical Use Cases

```
WHEN TO USE A CONSUMER VPN:

✅ USE IT FOR:
  • Public WiFi (coffee shop, airport, hotel)
    Reason: Protects against eavesdropping and MITM
    
  • Accessing content in other countries
    (streaming services, news sites with geo-restrictions)
    
  • Preventing ISP from selling your browsing data
    (ISPs in many countries can legally sell this)
    
  • Downloading/torrenting (check legality in your region)
  
  • Avoiding bandwidth throttling by ISP

❌ DON'T EXPECT IT TO:
  • Make you completely anonymous (VPN provider can see traffic)
  • Protect from malware (that's antivirus's job)
  • Prevent website fingerprinting (browser cookies, Canvas, WebRTC)
  • Fully hide your identity if you're logged into Google/Facebook
  • Replace good security practices
```

### Setting Up a Simple VPN: OpenVPN on a Home Server

While consumer VPN services are easier, running your own gives you full control:

```bash
# On a Linux server (Ubuntu/Debian)
# This is the overview — full guide at: openvpn.net

# Step 1: Install OpenVPN and EasyRSA (key management)
sudo apt update && sudo apt install openvpn easy-rsa -y

# Step 2: Set up Certificate Authority
make-cadir ~/openvpn-ca
cd ~/openvpn-ca
./easyrsa init-pki
./easyrsa build-ca  # Creates your CA certificate

# Step 3: Generate server certificate
./easyrsa gen-req server nopass
./easyrsa sign-req server server

# Step 4: Generate Diffie-Hellman parameters (key exchange security)
./easyrsa gen-dh

# Step 5: Generate client certificate
./easyrsa gen-req client1 nopass
./easyrsa sign-req client client1

# Step 6: Create client config file (.ovpn)
# Include CA cert, client cert, client key, and server IP
```

### Zero-Trust Security — The Modern Approach

Traditional security trusts everything inside the network. **Zero-Trust** challenges this:

```
TRADITIONAL MODEL (Castle and Moat):
Outside Network → FIREWALL (moat) → Inside Network
                                   → TRUSTED!
Problem: Once inside, attacker can move freely

ZERO-TRUST MODEL:
"Never trust, always verify"

Every access request is verified:
  • Who is the user? (Identity)
  • What device are they on? (Device health)
  • What are they allowed to access? (Least privilege)
  • Is this behavior normal? (Analytics)

Result: Even an attacker inside the network 
        can't move freely without re-authenticating
        at every resource

Zero-Trust is the future of enterprise security.
Big tech companies (Google's BeyondCorp) pioneered this.
```

### Network Security Best Practices

```
DEFENSE IN DEPTH — Multiple layers of security
═══════════════════════════════════════════════

Layer 7: USERS (Security training, phishing awareness)
    ▲
Layer 6: APPLICATIONS (Secure coding, WAF)
    ▲
Layer 5: ENDPOINT (Antivirus, EDR, patch management)
    ▲
Layer 4: NETWORK (Firewall, IDS/IPS, network monitoring)
    ▲
Layer 3: PERIMETER (DMZ, edge firewall, DDoS protection)
    ▲
Layer 2: PHYSICAL (Locked server rooms, cable locks)
    ▲
Layer 1: POLICIES (Security policy, access control policy)

"Defense in Depth": No single layer is perfect.
Multiple layers mean an attacker must break through ALL of them.
```

### Practical Security Checklist for Your Home Network

```
IMMEDIATE ACTIONS (Do today):
□ Change router admin password (default: admin/admin is KNOWN)
□ Update router firmware (check manufacturer's website)
□ Enable WPA2 or WPA3 on WiFi (not WEP or open!)
□ Change WiFi password from the default
□ Disable WPS (WiFi Protected Setup has known vulnerabilities)

SHORT TERM (This week):
□ Enable firewall on all computers
□ Keep OS and software updated (patches fix vulnerabilities)
□ Install antivirus software
□ Use unique passwords for every account (use a password manager)
□ Enable 2FA on email, banking, social media

ADVANCED (Once basics are done):
□ Set up a separate guest WiFi network for visitors and IoT
□ Change DNS to secure provider (1.1.1.1 or 8.8.8.8 with DoH)
□ Consider a VPN for sensitive browsing
□ Review which devices are on your network (router admin panel)
□ Enable logging on your router to detect unusual activity
```

### Assignment 2 Deliverables

Complete the following for Assignment 2:

**Part A: Threat Analysis**
For each of the following scenarios, identify the attack type and describe a mitigation:
1. You connect to "CoffeeShop_Free_WiFi" and notice your bank login fails but someone else successfully logs in later
2. Your company website goes down due to receiving 500,000 requests per second
3. You receive an email from "support@amaz0n.com" asking you to click a link

**Part B: Firewall Rule Design**
Design a firewall ruleset for a small office network with:
- 30 employees who need web browsing (HTTP/HTTPS)
- A web server accessible from the internet
- Email server accessible from outside
- Internal file server NOT accessible from internet
- Admin SSH access only from specific IP

**Part C: Security Audit**
Complete the Home Network Security Audit checklist (shown above) and write a 1-page report on what you found and what you plan to improve.

---

## Module 2.5 Quick Reference Cheat Sheet

```
╔══════════════════════════════════════════════════════════════╗
║             MODULE 2.5 QUICK REFERENCE                      ║
╠══════════════════════════════════════════════════════════════╣
║ COMMON ATTACKS                                              ║
║  MitM:        Intercepts communication between two parties  ║
║  DoS/DDoS:    Overwhelms server with fake traffic           ║
║  Phishing:    Tricks users into giving credentials          ║
║  ARP Poison:  Redirects local traffic through attacker      ║
║  DNS Spoof:   Redirects domain to wrong IP                  ║
╠══════════════════════════════════════════════════════════════╣
║ FIREWALL TYPES                                              ║
║  Packet filter:    Checks IP/port (Layer 3/4)              ║
║  Stateful:         Tracks connection state (most common)    ║
║  Application/NGFW: Inspects content (Layer 7)              ║
╠══════════════════════════════════════════════════════════════╣
║ VPN PROTOCOLS                                               ║
║  WireGuard:   Fastest, modern, recommended                  ║
║  OpenVPN:     Flexible, widely supported                    ║
║  IKEv2:       Good for mobile (reconnects automatically)    ║
║  PPTP:        AVOID — cryptographically broken             ║
╠══════════════════════════════════════════════════════════════╣
║ COMMON PORTS TO KNOW                                        ║
║  21 FTP  22 SSH  23 Telnet  25 SMTP  53 DNS               ║
║  80 HTTP  110 POP3  143 IMAP  443 HTTPS  3389 RDP         ║
╚══════════════════════════════════════════════════════════════╝
```

---

---

# 📚 Glossary {#glossary}

| Term | Definition |
|------|-----------|
| **ARP** | Address Resolution Protocol — maps IP addresses to MAC addresses on local network |
| **BGP** | Border Gateway Protocol — how routers on the internet exchange routing information |
| **CIDR** | Classless Inter-Domain Routing — method for allocating IP addresses using prefix notation (/24) |
| **DHCP** | Dynamic Host Configuration Protocol — automatically assigns IP addresses to devices |
| **DMZ** | Demilitarized Zone — network segment between trusted and untrusted zones |
| **DNS** | Domain Name System — translates domain names (google.com) to IP addresses |
| **DoS/DDoS** | Denial of Service / Distributed Denial of Service — attacks that overwhelm a target |
| **Ethernet** | Standard technology for wired local area networks |
| **Firewall** | System that monitors and controls network traffic based on rules |
| **Gateway** | Router that connects one network to another |
| **HTTP/HTTPS** | Hypertext Transfer Protocol (Secure) — web communication protocols |
| **ICMP** | Internet Control Message Protocol — used by ping and traceroute |
| **IEEE** | Institute of Electrical and Electronics Engineers — defines WiFi standards |
| **IP** | Internet Protocol — defines addressing and routing of packets |
| **IPv4** | IP version 4 — 32-bit addressing (192.168.x.x) |
| **IPv6** | IP version 6 — 128-bit addressing (2001:db8::1) |
| **IPS/IDS** | Intrusion Prevention/Detection System — monitors for malicious activity |
| **ISP** | Internet Service Provider — company providing internet access |
| **LAN** | Local Area Network — network within a home or building |
| **Latency** | Delay in data transmission, measured in milliseconds |
| **MAC Address** | Media Access Control — unique hardware identifier for network devices |
| **MitM** | Man-in-the-Middle — attacker intercepts communication between two parties |
| **Modem** | Modulator-Demodulator — converts between digital data and ISP's signal |
| **NAT** | Network Address Translation — maps private IPs to public IPs |
| **NGFW** | Next-Generation Firewall — deep packet inspection firewall |
| **NIC** | Network Interface Card — hardware that connects a device to a network |
| **OFDMA** | Orthogonal Frequency Division Multiple Access — WiFi 6 multi-user technology |
| **OSI Model** | Open Systems Interconnection — 7-layer model for network communication |
| **PAT** | Port Address Translation — type of NAT using port numbers |
| **Ping** | Test connectivity by sending ICMP echo request and awaiting reply |
| **Port** | Number identifying a specific application/service (0-65535) |
| **Protocol** | Set of rules for how devices communicate |
| **Router** | Device that routes packets between different networks |
| **SSID** | Service Set Identifier — your WiFi network name |
| **SSH** | Secure Shell — encrypted remote command-line access |
| **SSL/TLS** | Secure Sockets Layer / Transport Layer Security — encryption protocols |
| **Subnet** | Logical subdivision of an IP network |
| **Subnet Mask** | 32-bit number that separates network and host portions of an IP address |
| **Switch** | Network device that connects devices within a LAN |
| **TCP** | Transmission Control Protocol — reliable, ordered data delivery |
| **Topology** | Physical or logical arrangement of network devices |
| **UDP** | User Datagram Protocol — fast, connectionless data delivery |
| **VLAN** | Virtual LAN — logical separation of network traffic |
| **VPN** | Virtual Private Network — encrypted tunnel over public network |
| **WAN** | Wide Area Network — network spanning large geographic area |
| **WAP/AP** | Wireless Access Point — device that creates a wireless network |
| **WPA/WPA2/WPA3** | WiFi Protected Access — WiFi encryption standards |
| **Zero-Trust** | Security model that verifies every access request regardless of location |

---

# 🗂️ Quick Reference Cheat Sheets {#cheatsheets}

## Network Commands Cheat Sheet

```bash
# FIND YOUR IP ADDRESS
Windows:   ipconfig
Mac/Linux: ifconfig    OR    ip addr show

# TEST CONNECTIVITY
ping 8.8.8.8           # Can you reach Google's DNS?
ping google.com         # Does DNS work too?
ping 192.168.1.1        # Can you reach your router?

# TRACE NETWORK PATH
Windows:   tracert google.com
Mac/Linux: traceroute google.com

# SHOW ACTIVE CONNECTIONS
Windows:   netstat -an
Mac/Linux: netstat -an    OR    ss -an

# DNS LOOKUP
nslookup google.com
dig google.com          # Linux/Mac
nslookup -type=MX gmail.com   # Look up mail servers

# SCAN YOUR NETWORK (who's connected?)
# Install nmap first: nmap.org
nmap -sn 192.168.1.0/24    # Ping scan your entire subnet

# CHECK OPEN PORTS ON LOCALHOST
netstat -tulpn             # Linux
netstat -an | findstr LISTENING   # Windows
```

## Port Numbers Cheat Sheet

```
COMMON WELL-KNOWN PORTS
═══════════════════════

PORT  │ PROTOCOL    │ SERVICE
──────┼─────────────┼────────────────────────────────────
20/21 │ TCP         │ FTP (File Transfer Protocol)
22    │ TCP         │ SSH (Secure Shell) — admin access
23    │ TCP         │ Telnet (AVOID — unencrypted!)
25    │ TCP         │ SMTP (Email sending)
53    │ TCP/UDP     │ DNS (Domain Name System)
67/68 │ UDP         │ DHCP (IP address assignment)
80    │ TCP         │ HTTP (Web, unencrypted)
110   │ TCP         │ POP3 (Email retrieval, old)
123   │ UDP         │ NTP (Network Time Protocol)
143   │ TCP         │ IMAP (Email retrieval, modern)
443   │ TCP         │ HTTPS (Web, encrypted) ← USE THIS
465   │ TCP         │ SMTPS (Email sending, encrypted)
993   │ TCP         │ IMAPS (Email, encrypted)
1194  │ UDP         │ OpenVPN
3389  │ TCP         │ RDP (Windows Remote Desktop)
5900  │ TCP         │ VNC (Remote desktop)
8080  │ TCP         │ HTTP alternate (dev servers)
51820 │ UDP         │ WireGuard VPN
```

## Subnetting Quick Reference

```
CIDR  │ MASK            │ HOSTS  │ BLOCK SIZE
──────┼─────────────────┼────────┼───────────
/24   │ 255.255.255.0   │ 254    │ 1 network
/25   │ 255.255.255.128 │ 126    │ 128
/26   │ 255.255.255.192 │ 62     │ 64
/27   │ 255.255.255.224 │ 30     │ 32
/28   │ 255.255.255.240 │ 14     │ 16
/29   │ 255.255.255.248 │ 6      │ 8
/30   │ 255.255.255.252 │ 2      │ 4 (point-to-point)
/32   │ 255.255.255.255 │ 1      │ host route

Formula: Usable hosts = 2^(32 - prefix) - 2
```

---

# 🛠️ Project Ideas {#projects}

## Project 1: Complete Home Network Audit and Documentation

**Difficulty**: Beginner | **Time**: 2-3 hours

**Description**: Create a professional-quality documentation package for your home network.

**Steps**:
1. Draw your network topology using Draw.io (app.diagrams.net)
2. Label every device with its name, IP, and connection type
3. Run `nmap -sn 192.168.x.0/24` to discover all connected devices
4. Document your router's configuration (security settings, DHCP range, DNS)
5. Perform the security audit checklist from Module 2.5
6. Write a 2-page network improvement plan

**Deliverable**: A professional PDF network documentation package

---

## Project 2: Build a Home VPN Server

**Difficulty**: Intermediate | **Time**: 4-6 hours

**Description**: Set up your own WireGuard VPN server on a Raspberry Pi or cheap VPS.

**Steps**:
1. Get a Raspberry Pi (Model 3 or 4) or a $5/month VPS (DigitalOcean, Linode)
2. Install Ubuntu Server
3. Install WireGuard: `sudo apt install wireguard`
4. Generate key pairs for server and client
5. Create server config file (`/etc/wireguard/wg0.conf`)
6. Configure port forwarding on your router (if using Pi)
7. Create client config and connect your phone/laptop
8. Test: Check that your IP address changes when connected

**Why this matters**: You control your VPN — no subscription, no logs, no trust needed

---

## Project 3: Network Packet Capture and Analysis

**Difficulty**: Intermediate | **Time**: 2-4 hours

**Description**: Use Wireshark to capture and analyze real network traffic.

**Steps**:
1. Download and install Wireshark (wireshark.org)
2. Capture traffic on your network interface for 2 minutes
3. Apply filter: `http` — analyze unencrypted web traffic
4. Apply filter: `dns` — see every domain name lookup
5. Apply filter: `tcp.flags.syn == 1` — see all connection attempts
6. Find the ARP packets and explain the mapping process
7. Find a DHCP exchange and trace the 4-step process

**Deliverable**: A written analysis of what you found, including screenshots

---

## Project 4: Subnet a Company Network

**Difficulty**: Intermediate | **Time**: 2-3 hours

**Description**: Design a complete network for a fictional 200-person company.

**Scenario**: TechCorp Inc. has:
- 100 engineers (need fast access to internal code servers)
- 50 sales reps (need internet and CRM access)
- 30 HR/Finance employees (need strict access controls)
- 20 IT admins (need access to everything)
- 5 public-facing web servers
- Network: `172.16.0.0/16`

**Tasks**:
1. Create subnets for each department
2. Design VLANs for each group
3. Plan firewall rules between departments
4. Design the DMZ for web servers
5. Document IP addressing plan in a spreadsheet

---

## Project 5: Set Up a Secure Home WiFi Network

**Difficulty**: Beginner-Intermediate | **Time**: 1-2 hours

**Description**: Completely reconfigure your home WiFi for maximum security.

**Steps**:
1. Log into your router (usually 192.168.1.1 or 192.168.0.1)
2. Change admin username and password
3. Update router firmware
4. Enable WPA3 (or WPA2 if router is older)
5. Set a strong WiFi password (20+ characters)
6. Create a separate guest network (completely isolated)
7. Create an IoT VLAN for smart devices (if router supports it)
8. Disable UPnP (security risk)
9. Disable WPS (security risk)
10. Enable router's built-in firewall and DNS filtering

**Deliverable**: Before/after comparison of your network security

---

# 🎓 Interview Questions {#interview}

## Beginner Level

1. **What is an IP address and why does every device need one?**
   - Key points: Unique identifier, used for routing, logical address

2. **What's the difference between a router and a switch?**
   - Router: Routes between different networks (works at Layer 3)
   - Switch: Connects devices within same network (works at Layer 2)

3. **What is a MAC address and when is it used?**
   - Hardware identifier, used for local delivery within a LAN segment

4. **Explain the difference between TCP and UDP.**
   - TCP: Reliable, ordered, connection-oriented (web, email, file transfer)
   - UDP: Fast, connectionless, no guarantee (video streaming, DNS, gaming)

5. **What is DHCP and what problem does it solve?**
   - Automatically assigns IP addresses, so you don't have to configure each device manually

## Intermediate Level

6. **How does NAT work and why was it invented?**
   - Maps multiple private IPs to one public IP using port numbers, invented due to IPv4 address exhaustion

7. **What is subnetting and what are the benefits?**
   - Divides large networks into smaller ones; benefits include security isolation, reduced broadcast traffic, better organization

8. **Explain the difference between IPv4 and IPv6.**
   - IPv4: 32-bit, ~4.3B addresses, still dominant; IPv6: 128-bit, 340 undecillion addresses, built-in security

9. **What is the OSI model and what are the 7 layers?**
   - Physical, Data Link, Network, Transport, Session, Presentation, Application

10. **How does a stateful firewall differ from a packet filter?**
    - Packet filter: Checks individual packets; Stateful: Tracks connection state, knows if packet belongs to established session

## Advanced Level

11. **Explain a man-in-the-middle attack and three ways to prevent it.**
    - Attacker intercepts communication; Prevent: HTTPS, certificate pinning, VPN, network monitoring

12. **What is the difference between symmetric and asymmetric encryption? When is each used in networking?**
    - Symmetric: Same key both ways (fast, used for bulk data); Asymmetric: Public/private key pair (slow, used for key exchange)

13. **Explain BGP and its role in internet routing.**
    - Border Gateway Protocol: How autonomous systems (ISPs) advertise and exchange routing information; the internet's routing protocol

14. **What is Zero-Trust architecture and why is it replacing the traditional perimeter model?**
    - Never trust any connection implicitly; verify every access; better for cloud and remote work

15. **How does DNS-over-HTTPS (DoH) improve privacy?**
    - Encrypts DNS queries so ISP and eavesdroppers can't see which domains you're looking up

---

# 🏆 Certifications Guide {#certifications}

## Entry Level

**CompTIA Network+**
- Most popular vendor-neutral networking certification
- Covers: Network concepts, infrastructure, operations, security, troubleshooting
- Exam: N10-008, 90 questions, 90 minutes
- Cost: ~$338 USD
- Study time: 3-6 months
- Resources: Professor Messer (free), CompTIA CertMaster

**Cisco CCNA**
- Industry gold standard for networking
- Covers: Routing, switching, VLANs, troubleshooting, basic security
- Exam: 200-301, 120 questions, 120 minutes
- Cost: ~$330 USD
- Study time: 6-12 months
- Resources: Cisco NetAcad (free), Jeremy's IT Lab (free on YouTube)

## Intermediate Level

**CompTIA Security+**
- Most popular entry-level security certification
- Covers: Threats, cryptography, PKI, identity, network security
- Prerequisite: CompTIA Network+ recommended
- Cost: ~$392 USD

**Cisco CCNP Enterprise**
- Advanced Cisco networking
- Prerequisite: CCNA
- Focus: Enterprise networks at scale

## Advanced Level

**CISSP** — Certified Information Systems Security Professional
- The gold standard in cybersecurity
- Requires 5 years of professional experience
- Eight domains including network security

**CEH** — Certified Ethical Hacker
- Focuses on penetration testing and offensive security

## Learning Roadmap

```
BEGINNER → INTERMEDIATE → ADVANCED
     │              │              │
  Network+      CCNA/Security+   CISSP/CEH
  (3-6 months)  (6-12 months)   (1-2 years)
     │              │              │
  Learn TCP/IP  Practice lab    Real-world
  and subnetting environments   projects &
               (Cisco PKT,      experience
               GNS3)
```

---

# 📖 Additional Resources {#resources}

## Free Online Courses
- **Cisco NetAcad** (netacad.com) — Networking Essentials, Packet Tracer labs
- **Professor Messer** (professormesser.com) — CompTIA Network+ free course
- **Jeremy's IT Lab** (youtube.com/@JeremysITLab) — Free CCNA course
- **Khan Academy** — Basic networking concepts

## Books
- *Computer Networking: A Top-Down Approach* — Kurose & Ross (university textbook, excellent)
- *Network Warrior* — Gary Donahue (practical, real-world focus)
- *The Practice of Network Security Monitoring* — Richard Bejtlich
- *CompTIA Network+ Study Guide* — Mike Meyers

## Tools and Simulators
- **Cisco Packet Tracer** — Free network simulator, excellent for CCNA prep
- **GNS3** — Professional network simulator, runs real Cisco IOS
- **Wireshark** — Packet capture and analysis
- **nmap** — Network scanner and security tool
- **Angry IP Scanner** — Simple network discovery
- **pfSense** — Free open-source firewall/router OS

## Websites
- **Subnet Calculator**: jodies.de/ipcalc or subnet-calculator.com
- **IANA** (iana.org) — Internet addressing authority
- **RFC Editor** (rfc-editor.org) — Original internet standards documents
- **Shodan** (shodan.io) — Search engine for internet-connected devices (educational)

---
