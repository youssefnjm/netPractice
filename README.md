# 🌐 NETPRACTICE

> *A comprehensive guide to understanding IP addresses, subnetting, and network fundamentals*

---

## 📡 What is IP?

**IP (Internet Protocol)** is a protocol that defines how devices identify and locate each other on a network, and how data packets are delivered between them.

---

## 🔄 Versions of IP

| Version | Size | Format | Problem | Extras |
|---------|------|--------|---------|--------|
| **IPv4 (v4)** 🟢 | `32 bits` <br> *~4.3B addresses* | `192.168.1.10` <br> *(dotted decimal)* | ⚠️ Addresses running out |
| **IPv6 (v6)** 🔵 | `128 bits` <br> *~340 undecillion addresses* | `2001:0db8:85a3::8a2e:0370:7334` <br> *(hex with colons)* | ✅ Virtually unlimited |

---

## 🏗️ IP Address Structure

- All IPv4 addresses have the same structure: **`192.186.1.1`**
- `[192, 186, 1, 1]` are called **octets** 📦
- Each octet length is **8 bits** → IP length = `8 × 4 = 32 bits` 
- Each octet ranges between **0 and 255** 📊

### 🎯 Two Essential Parts

An IP address has two main components:

- **🌐 Network Address** → *defines the network*
- **💻 Host Address** → *defines the device within that network*

---

## 🎭 Network Address vs Host Address

To distinguish between **network address** and **host address**, we use a **subnet mask**.

### ✨ Key Properties:
- 📏 Subnet mask is a **32-bit (4 bytes)** address
- ✅ Bits set to `1` → **network address**
- ❌ Bits set to `0` → **host address**
- 🎯 Defines the range of IP addresses that can be used within a network or subnet

---

## 🔍 Using Subnet Masks to Find the Network Address

### 📋 **Example:**

The device **A1** has the following properties:
- 📍 **IP Address:** `104.198.241.125`
- 🎭 **Mask:** `255.255.255.128`

### 🔧 **Step 1: Convert mask to binary**

```
Mask: 11111111.11111111.11111111.10000000
```
*Bits of `1` → network part, bits of `0` → host part.*

### ⚙️ **Step 2: Convert IP to binary & apply mask (bitwise AND)**

```
IP:   01101000.11000110.11110001.01111101
Mask: 11111111.11111111.11111111.10000000
────────────────────────────────────────────
Net:  01101000.11000110.11110001.00000000
```

**🎯 Result:** Network address = **`104.198.241.0`**

---

## 🌐 Finding the Range of Host Addresses

We use the bits of our IP address dedicated to the **host address**.

```
IP address    | 01101000 . 11000110 . 11110001 . 01111101
Mask          | 11111111 . 11111111 . 11111111 . 10000000
```

The possible range of our host addresses is expressed through the **last 7 bits** of the mask (all `0`):

| Format | Range |
|--------|-------|
| **BINARY** | `0000000` - `1111111` |
| **DECIMAL** | `0` - `127` |

### 🎯 **Final IP Range**

To get the range of possible IP addresses for our network, we add the range of host addresses to the network address:

**📊 Our range of possible IP addresses:** `104.198.241.0` - `104.198.241.127`

---

<div align="center">

### 🎉 *Happy Networking!* 🎉

*Master the fundamentals and conquer any network challenge*

---

**Made with ❤️ for network enthusiasts**

</div>
