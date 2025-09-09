# 🌐 NETPRACTICE

> *A comprehensive guide to understanding IP addresses, subnetting, and network fundamentals*

---

## 📡 What is IP?

**IP (Internet Protocol)** is a protocol that defines how devices identify and locate each other on a network, and how data packets are delivered between them.

---

## 🔄 Versions of IP

| Version | Size | Format | Problem | Extras |
|---------|------|--------|---------|--------|
| **IPv4 (v4)** 🟢 | `32 bits` <br> *~4.3B addresses* | `192.168.1.10` <br> *(dotted decimal)* | ⚠️ Addresses running out | — |
| **IPv6 (v6)** 🔵 | `128 bits` <br> *~340 undecillion addresses* | `2001:0db8:85a3::8a2e:0370:7334` <br> *(hex with colons)* | Virtually unlimited | Built-in IPsec<br>⚡ Efficient routing<br>🔧 Auto-configuration |

---

## 🏗️ IP Address Structure

- All IPv4 addresses have the same structure: **`192.186.1.1`**
- `[192, 186, 1, 1]` are called **octets**
- Each octet length is **8 bits** → IP length = `8 × 4 = 32 bits` 
- Each octet ranges between **0 and 255**

### 🎯 Two Essential Parts

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

## 🎭 What Does a Subnet Mask Really Do?

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

## 💡 Practical Examples

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

## 🗂️ IP Classes

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

### 📌 Quick Summary Table

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

and here comes CIDR to fex the problem, CIDR introduced the “/N” notation (slash notation), where N = number of network bits.

Example:

- 192.168.1.0/24 = 24 network bits, 8 host bits → 254 hosts.
- 192.168.1.0/26 = 26 network bits, 6 host bits → 62 hosts.

This gave flexibility: networks could be exactly the size needed, no waste.

---

## Public vs Private IPs

### Public IP

An IP address that is unique and reachable across the whole internet (the “face” of your network on the internet).Assigned by by ISPs (Internet Service Providers).

### Private IP

An IP address that is only valid inside a private network (LAN, office, home Wi-Fi), Not routable on the internet.

### ⚠️ Special Notes

Loopback: 127.0.0.1 is neither public nor private, it’s “me” (your own machine).

#### Special ranges

| Class       | Private Range                   | Example       | Max Hosts |
| ----------- | ------------------------------- | ------------- | --------- |
| 🅰️ Class A | `10.0.0.0 – 10.255.255.255`     | `10.0.5.10`   | \~16M     |
| 🅱️ Class B | `172.16.0.0 – 172.31.255.255`   | `172.16.45.2` | \~1M      |
| 🅲 Class C  | `192.168.0.0 – 192.168.255.255` | `192.168.1.1` | \~65k     |

### How do private IPs talk to the Internet? (NAT)

A device with a private IP cannot directly connect to the internet. Instead, the router (which has a public IP) uses NAT (Network Address Translation) to “translate” all internal requests into its own public IP.

Example:

Your laptop = 192.168.1.5

- Your phone = 192.168.1.8
- Both connect through your router’s public IP = 102.45.88.21
- To the outside world, both appear as one IP (102.45.88.21).

---

<br/>

<div align="center">

### 🎉 *Happy Networking!* 🎉

*Master the fundamentals and conquer any network challenge*

---

**Made with ❤️ for network enthusiasts**

</div>
