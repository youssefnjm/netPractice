# 🌐 NETPRACTICE

> *A comprehensive guide to understanding IP addresses, subnetting, and network fundamentals*

---

## 📑 Table of Contents

### 🌐 **1. Introduction to IP**
- [📡 What is IP?](#what-is-ip)
- [🔄 Versions of IP (IPv4 vs IPv6)](#versions-of-ip)
- [🏗️ IP Address Structure](#ip-address-structure)
- [🔍 Network vs Host Address](#network-vs-host-address)
- [🔍 how can i know between network address and host address?](#how-can-i-know-between-network-address-and-host-address)
- [🎭 What Does a Subnet Mask Really Do?](#what-does-a-subnet-mask-really-do)
- [💡 Practical Examples](#practical-examples)
- [📚 Historical Context](#ip-classes)
- [🚀 CIDR vs Classes](#are-we-steel-using-classes)
- [🔓 Public vs Private IPs](#public-vs-private-ips)
- [🔄 NAT (Network Address Translation)](#how-do-private-ips-talk-to-the-internet-nat)

### 🌐 **2. Introduction to TCP & UDP**
- [📡 What is tcp?](#what-is-tcp)
- [📡 What is TCP/IP?](#what-is-tcp/ip)
- [📡 How does TCP work?](#how-does-tcp-work)
- [📡 What is udp?](#what-is-udp)
- [📡 How does UDP work?](#how-does-udp-work)

### 🖧 **3. Devices in Networking**
- [📡 Devices in Networking](#devices-in-networking)
- [📡 How They Work Together](#how-they-work-together)

### 🌐 **4. Routing & Gateways**
- [What is Routing?](#what-is-routing)
- [What is a Gateway?](#what-is-a-gateway)
- [How Routing Works Step by Step](#what-is-routing)

---

## What is IP?

**IP (Internet Protocol)** is a protocol that defines how devices identify and locate each other on a network, and how data packets are delivered between them.

---

## Versions of IP

| Version | Size | Format | Problem | Extras |
|---------|------|--------|---------|--------|
| **IPv4 (v4)** 🟢 | `32 bits` <br> *~4.3B addresses* | `192.168.1.10` <br> *(dotted decimal)* | ⚠️ Addresses running out | — |
| **IPv6 (v6)** 🔵 | `128 bits` <br> *~340 undecillion addresses* | `2001:0db8:85a3::8a2e:0370:7334` <br> *(hex with colons)* | Virtually unlimited | Built-in IPsec<br> Efficient routing<br> Auto-configuration |

---

## IP Address Structure

- All IPv4 addresses have the same structure: **`192.186.1.1`**
- `[192, 186, 1, 1]` are called **octets**
- Each octet length is **8 bits** → IP length = `8 × 4 = 32 bits` 
- Each octet ranges between **0 and 255**

### Network vs Host Address

An IP address has two main components:

- **🌐 Network Address** → *defines the network*
- **💻 Host Address** → *defines the device within that network*

---

## how can i know between network address and host address?

To distinguish between **network address** and **host address**, we use a **subnet mask**.

### Key Properties:
- 🎯 Subnet mask defines the range of IP addresses that can be used within a network or subnet
- 📏 Subnet mask is a **32-bit (4 bytes)** address
- ✅ Bits set to `1` → **network address**
- ❌ Bits set to `0` → **host address**

---

## What Does a Subnet Mask Really Do?

Think of an IP address like a **street address**:

- 🏙️ **Network part** = *the city & street name*
- 🏠 **Host part** = *the house number*

The subnet mask is like a **"highlighter"** that tells us:
- ✨ Which part of the address belongs to the **network**
- ✨ Which part is left for the **hosts** (devices)

### 📋 Detailed Example

#### 🎭 **Step 1: Look at the Subnet Mask**

We're given a mask: **`255.255.255.128`**
If we convert it to binary: **`11111111.11111111.11111111.10000000`**

##### 🔍 **What do these bits mean?**
- The **`1`s** *(25 of them)* mark the **network portion** → *these bits never change inside this subnet*
- The **`0`s** *(7 of them)* mark the **host portion** → *these bits can change to give different devices addresses*

That's why we call it a **`/25`** network *(because 25 bits belong to the network)*.

#### ⚙️ **Step 2: What does that mean?**

Think of it like splitting the IP into **two zones**:

##### **🌐 Network = Fixed Part**
- In our IP: `104.198.241.125`
- The first **25 bits** are locked (fixed) 
- This gives us the base network address = **`104.198.241.0`**

##### **💻 Hosts = Changing Part**
- The last **7 bits** are free to vary
- In decimal: **7 bits = 2^7 = 128** possible values *(from 0 to 127)*
- Host portion can be anything between `0000000` and `1111111`

#### 📊 **Step 3: Calculate the range**

Now we can calculate everything we need:
- 🌐 Network Address = 104.198.241.0 (all host bits = 0)
- 📡 Broadcast Address = 104.198.241.127 (all host bits = 1)
- 💻 Usable Hosts = from 104.198.241.1 → 104.198.241.126

#### 🎯 **Final Result**
The subnet can hold **126 usable devices**.

### 📝 **Remember:**
- **Subnet mask** = 32-bit address that acts as a "highlighter"
- **Bits set to `1`** → Network portion (fixed)
- **Bits set to `0`** → Host portion (variable)
- **CIDR notation** (like `/25`) = number of network bits
- **Quick Formula:** **`usable Hosts = 2^(host bits) - 2`** *(-2 because we subtract network and broadcast addresses)*

---

## Practical Examples

🔹 **Example 1:**

***Given:*** `IP: 192.168.1.77` | `Mask: 255.255.255.0 → /24`

 ***Step 1:***
 
 Write mask in binary
`255.255.255.0 = 11111111.11111111.11111111.00000000`
*So: **24 network bits**, **8 host bits***

 ***Step 2:***
 
 Network address
`192.168.1.77 AND 255.255.255.0 = 192.168.1.0`

 ***Step 3:***
 
 Host range
- 📡 *Broadcast:* `192.168.1.255`
- 🌐 *network:* `192.168.1.0`
- ✅ *Usable:* `192.168.1.1` → `192.168.1.254`

🔸 **Example 2:**

***Given*** `IP: 10.0.5.200` | `Mask: 255.255.255.192 → /26`

 ***Step 1 :***
 
 Mask in binary
`255.255.255.192 = 11111111.11111111.11111111.11000000`
*So: 26 network bits**, 6 host bits*

 ***Step 2:***
 
 Network size = 2^6 = 64 addresses
**Subnets of 64:**
- `10.0.5.0` – `10.0.5.63` or `10.0.5.64` – `10.0.5.127` or `10.0.5.128` – `10.0.5.191` or `10.0.5.192` – `10.0.5.255`

 ***Step 3:***
 
 `10.0.5.200` belongs to the last subnet
- 🌐 *Network:* `10.0.5.192`
- 📢 *Broadcast:* `10.0.5.255`
- ✅ *Usable:* `10.0.5.193` → `10.0.5.254`

---

## IP Classes

### Historical Context

Before **CIDR (Classless Inter-Domain Routing)**, IP addresses were divided into **5 classes (A–E)**, based on the **first octet** of the IP address.
and to find the classe you shoul look at the **first octet** to determine the class

---

### Class A

- **🔢 Range:** `1 – 126`
- **🎭 Default subnet mask:** `255.0.0.0` (`/8`)
- **🎯 Use case:** Very large networks *(millions of hosts)*
- **💡 Tip:** Used by big organizations in the early days of the internet

---

### Class B

- **🔢 Range:** `128 – 191`
- **🎭 Default subnet mask:** `255.255.0.0` (`/16`)
- **🎯 Use case:** Medium networks *(~65k hosts)*

---

### Class C

- **🔢 Range:** `192 – 223`
- **🎭 Default subnet mask:** `255.255.255.0` (`/24`)
- **🎯 Use case:** Small networks *(up to 254 hosts)*
- **💡 Tip:** Commonly used in LANs *(like `192.168.x.x`)*

---

### Class D (Multicast)

- **🔢 Range:** `224 – 239`
- **🎯 Use case:** Multicast traffic *(one-to-many communication, like video streaming)*
- **⚠️ Tip:** Not for normal host addressing

---

### Class E (Experimental)

- **🔢 Range:** `240 – 255`
- **🎯 Use case:** Reserved for research/testing
- **⚠️ Tip:** Not used in real networks

---

### Special Case: Loopback

- **🔢 Range:** `127.x.x.x`
- **📍 Example:** `127.0.0.1` = **localhost** *(your computer talks to itself)*
- **💡 Tip:** Useful for developers to test applications without needing a real network

### Quick Summary Table

| Class | 1st Octet Range | Default Mask | Network Size | Notes |
|-------|----------------|--------------|--------------|--------|
| **A** | `1 – 126` | `255.0.0.0` (`/8`) | ~16M hosts | Large networks |
| **B** | `128 – 191` | `255.255.0.0` (`/16`) | ~65k hosts | Medium networks |
| **C** | `192 – 223` | `255.255.255.0` (`/24`) | 254 hosts | Small networks |
| **D** | `224 – 239` | N/A | Multicast | Group communications |
| **E** | `240 – 255` | N/A | Reserved | Research/testing |
| **Loopback** | `127.x.x.x` | N/A | — | Localhost |

### are we steel using classes?

In the early Internet, we only had classful addressing (A, B, C, D, E). but the Problem it was **wasteful**

Example: A company needing 300 IPs could only choose:

- Class C → 254 hosts (too small)
- Class B → 65,536 hosts (way too big, wasteful).

and here comes CIDR to fex the problem, CIDR introduced the "/N" notation (slash notation), where N = number of network bits.

Example:

- 192.168.1.0/24 = 24 network bits, 8 host bits → 254 hosts.
- 192.168.1.0/26 = 26 network bits, 6 host bits → 62 hosts.

This gave flexibility: networks could be exactly the size needed, no waste.

---

## Public vs Private IPs

### Public IP

An IP address that is unique and reachable across the whole internet (the "face" of your network on the internet).Assigned by by ISPs (Internet Service Providers).

### Private IP

An IP address that is only valid inside a private network (LAN, office, home Wi-Fi), Not routable on the internet.

### ⚠️ Special Notes

Loopback: 127.0.0.1 is neither public nor private, it's "me" (your own machine).

#### Special ranges

| Class       | Private Range                   | Example       | Max Hosts |
| ----------- | ------------------------------- | ------------- | --------- |
| 🅰️ Class A | `10.0.0.0 – 10.255.255.255`     | `10.0.5.10`   | \~16M     |
| 🅱️ Class B | `172.16.0.0 – 172.31.255.255`   | `172.16.45.2` | \~1M      |
| 🅲 Class C  | `192.168.0.0 – 192.168.255.255` | `192.168.1.1` | \~65k     |

### How do private IPs talk to the Internet? (NAT)

A device with a private IP cannot directly connect to the internet. Instead, the router (which has a public IP) uses NAT (Network Address Translation) to "translate" all internal requests into its own public IP.

Example:

Your laptop = 192.168.1.5

- Your phone = 192.168.1.8
- Both connect through your router's public IP = 102.45.88.21
- To the outside world, both appear as one IP (102.45.88.21).

---

## What is TCP?

TCP (Transmission Control Protocol) It is a transport layer protocol (layer 4 in the OSI model), Main job reliable data delivery between two devices.

Features:

- 📦 Splits data into segments
- 🔢 Numbers segments so they can be reassembled in order
- ✅ Uses ACKs (acknowledgements) to confirm delivery
- 🔄 Retransmits lost packets
- 🔐 Provides error checking & flow control

---

## What is TCP/IP?

TCP/IP is not one protocol, it’s a protocol suite (a family of protocols).

Two key protocols in the suite:

- IP = addressing & delivery (the "where").

- TCP = reliability & order (the "how"). 

So: TCP/IP = IP handles the path, TCP makes sure the data arrives correctly.

---

## How does TCP work?

- Browser sends HTTP request.
- TCP breaks it into segments, adds sequence numbers.
- TCP gives segments to IP, IP puts them inside packets with source & destination IP addresses.
- Packets travel across routers, possibly out of order, some may get lost.
- TCP on the receiving side collects segments, checks for errors. If something is missing, it asks for retransmission.
- Finally, it reassembles data in the correct order.
- The reassembled data is given to the browser and you see the webpage.

---

## What is UDP?

UDP (User Datagram Protocol), Like TCP, it’s a transport layer protocol (layer 4 in OSI), But: it is connectionless and unreliable (no handshakes, no delivery guarantee).

Features:
- 🚀 Fast — no overhead of acknowledgments/retransmission.
- 📦 Sends data in datagrams (like packets but without sequencing).
- 📡 Useful when speed matters more than reliability.

---

## How does UDP work?

- Application hands data to UDP.
- UDP puts data inside a datagram with source/destination ports.
- Datagram is handed to IP (just like TCP).
- IP delivers it — but if it gets lost, UDP does nothing about it.

---

## Devices in Networking
### 1. Hub (Layer 1 – Physical)

hub is a simple hardware device that connects multiple computers or other devices, acting as a central point for data transmission in a local area network (LAN). 
When a hub receives data, it doesn't analyze or manage it but instead broadcasts that data to all other connected devices.

Example:
- If PC1 sends data to PC2, the hub sends the same data to every PC connected.
- This causes a lot of collisions and wasted bandwidth.

### 2. Switch (Layer 2 – Data Link)

switch is a hardware device that connects multiple devices, like computers, printers, and servers, 
within a local area network (LAN), allowing them to communicate and share information efficiently

Example:
- PC1 sends data to PC2 → the switch looks up PC2’s MAC → forwards only to PC2’s port.
- Reduces collisions, more efficient.


### 3. Router (Layer 3 – Network)

router is a hardware device that connects two or more separate computer networks, such as your home network and the internet, 
allowing them to communicate by forwarding data packets to their intended destinations

Example:
- PC1 = 192.168.1.10
- PC2 = 10.0.0.5
- They are in different networks → must go through a router (gateway).


## How They Work Together

### 1. Inside a LAN:

- PCs connect to a switch.
- Switch forwards data directly to the right PC using MAC addresses.

### 2. Between LANs:

- If two PCs are on different networks, the switch can’t help (it only understands MACs).
- The packet must go to a router (gateway).
- The router checks its routing table and forwards the packet toward the correct network.

### 3. Hub (old tech):

- Rarely used now because it’s too “dumb” (broadcasts everything).
- Replaced by switches in modern networks.

---

## What is Routing?

Routing = deciding the path a packet should take to reach its destination (Think of it as a GPS for packets).

Key ideas:
- Each device knows which networks it can reach directly.
- If the destination is not in my network, I must send it to a router (gateway) that knows the way.

## What is a Gateway?

A Gateway is the “exit door” of your network, It’s usually your router, If your device doesn’t know where to send a packet, it sends it to the default gateway.

Example:

- Your laptop: 192.168.1.10
- Router (gateway): 192.168.1.1
- Destination: 142.250.190.46 (google.com)
- Since Google is not in 192.168.1.x, your laptop sends the packet to the gateway (192.168.1.1).

## How Routing Works Step by Step

- You send a packet to 142.250.190.46 (Google).
- Your PC checks: “Is this IP in my local network?”
- Your IP = 192.168.1.10, mask = /24 → local range = 192.168.1.0–192.168.1.255
- Google (142.250.190.46) is not in this range.
- Your PC says: “I don’t know where it is, so I’ll send it to my gateway (192.168.1.1).”
- The gateway/router then forwards the packet closer to its destination, using its own routing table.
- Eventually, the packet reaches Google’s network.

---

<br/>

<div align="center">

### 🎉 *Happy Networking!* 🎉

*Master the fundamentals and conquer any network challenge*

---

**Made with ❤️ for network enthusiasts**

</div>
