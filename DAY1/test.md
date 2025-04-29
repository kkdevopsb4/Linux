
# Networking Basics and VPC Setup Guide for Students

---

## 1. IPv4 vs IPv6

| Feature         | IPv4                             | IPv6                                               |
|-----------------|----------------------------------|----------------------------------------------------|
| Address Size    | 32-bit                           | 128-bit                                            |
| Address Format  | Decimal (e.g., 192.168.1.1)       | Hexadecimal (e.g., 2001:0db8:85a3:0000:0000:8a2e:0370:7334) |
| Total Addresses | ~4.3 billion                     | Virtually unlimited (~340 undecillion)             |
| Header Complexity | Simple                        | More Complex                                       |
| Example Usage   | Home Networks, Enterprises       | Modern Internet, IoT Devices                       |
| NAT Required    | Yes                              | No (designed to eliminate NAT)                     |

**Theory:**
- **IPv4**: Still widely used but address exhaustion is a concern.
- **IPv6**: Designed to solve address shortage, improved routing and security.

---

## 2. IP Address Classes (IPv4)

| Class | Range | Usage |
|:-----:|:-----:|:-----:|
| A     | 1.0.0.0 - 126.255.255.255 | Large networks |
| B     | 128.0.0.0 - 191.255.255.255 | Medium networks |
| C     | 192.0.0.0 - 223.255.255.255 | Small networks |
| D     | 224.0.0.0 - 239.255.255.255 | Multicasting |
| E     | 240.0.0.0 - 255.255.255.255 | Reserved for research |

**Important Points:**
- **Class A:** 16 million hosts.
- **Class B:** 65,534 hosts.
- **Class C:** 254 hosts.

---

## 3. Public IPs vs Private IPs

| Type       | Example     | Usage                      |
|------------|-------------|-----------------------------|
| Public IP  | 8.8.8.8     | Accessible over the Internet |
| Private IP | 192.168.0.1 | Internal network communication |

**Private IP Ranges:**
- 10.0.0.0/8
- 172.16.0.0/12
- 192.168.0.0/16

**Theory:**
- **Public IPs** are globally unique.
- **Private IPs** are reused internally inside LANs, VPNs, and VPCs.

---

## 4. CIDR - Classless Inter-Domain Routing

**Theory:**
- Replaces old Class A, B, C system.
- Provides flexible subnetting and efficient IP address usage.
- Format: `IP Address/Prefix Length` (e.g., `192.168.1.0/24`).

**Example:**
- `/24` → 256 addresses (254 usable hosts)
- `/16` → 65,536 addresses

---

## 5. Subnetting

**Theory:**
- Dividing a network into smaller networks (subnets).
- Helps optimize performance, management, and security.

**Example:**
- Split `192.168.1.0/24` into two subnets:
  - `192.168.1.0/25` → 128 addresses
  - `192.168.1.128/25` → 128 addresses

**Subnetting Formulas:**
- Number of Subnets = 2^n (n = number of borrowed bits)
- Hosts per Subnet = 2^(host bits) - 2

---

## 6. What is Loopback Address?

**Theory:**
- Reserved IP address to test internal networking.
- **IPv4 Loopback:** `127.0.0.1`
- **IPv6 Loopback:** `::1`

**Usage:**
- Checking network stack.
- Running local servers for development or testing.

```bash
ping 127.0.0.1
```
(Verifies that TCP/IP stack is operational.)

---

## 7. Sample VPC Setup in AWS (Step-by-Step Guide)

### Objective:
Create a Virtual Private Cloud (VPC) to deploy cloud resources securely.

---

### Steps:

✅ **Step 1: Login to AWS Console**
- Go to VPC Dashboard under Networking & Content Delivery.

✅ **Step 2: Create VPC**
- Click \"Create VPC\" → Select \"VPC Only\"
- Name: `MyVPC`
- IPv4 CIDR: `10.0.0.0/16`
- Tenancy: Default
- Create

✅ **Step 3: Create Subnets**
- Create Public Subnet:
  - Name: `Public-Subnet`
  - VPC: `MyVPC`
  - CIDR Block: `10.0.1.0/24`
  - AZ: (e.g., ap-south-1a)
- Create Private Subnet:
  - Name: `Private-Subnet`
  - VPC: `MyVPC`
  - CIDR Block: `10.0.2.0/24`

✅ **Step 4: Create Internet Gateway**
- Create IGW.
- Attach it to `MyVPC`.

✅ **Step 5: Route Tables**
- Create a Public Route Table:
  - Add Route: `0.0.0.0/0` → IGW
  - Associate with `Public-Subnet`.

✅ **Step 6: Launch an EC2 Instance**
- In Public Subnet.
- Assign a Public IP.
- Use Key Pair for SSH access.

✅ **Step 7: Validate**
SSH into the instance:

```bash
ssh -i my-key.pem ec2-user@<public-ip>
```

✅ **Optional:**
- Create NAT Gateway for Internet access from Private Subnets.

---

# 📋 Summary
Today we learned:
- IP basics (IPv4, IPv6, Classes, Public/Private)
- CIDR and Subnetting concepts
- Practical AWS VPC Setup

---

# 🚀 Tomorrow's Topic
\"Security Groups, NACLs, and AWS Networking Security.\"

---

**End of Document**

---

Would you also like me to provide a **ready `.md` file download link** so you can save it directly? 🚀  
(If yes, I can create and give it now.)  
Would you also like a **simple VPC diagram** to attach to this file? 🎯 (Very useful for explaining!)
