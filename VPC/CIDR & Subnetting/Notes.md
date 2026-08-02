# Binary Basics

Before learning CIDR and Subnetting, it is important to understand Binary Numbers.

Computers do not understand decimal numbers (0-9). Instead, they understand only two values:

- 0 (OFF)
- 1 (ON)

This is known as the Binary Number System.

Understanding binary makes CIDR and subnetting much easier.

---

# What is Binary?

Binary is a number system that uses only two digits:

```
0
1
```

Unlike the Decimal Number System, which uses ten digits (0-9), Binary uses only two.

Every computer stores and processes information using Binary.

---

# Why Do Computers Use Binary?

Electronic circuits inside computers have only two states.

```
ON

OFF
```

These are represented as:

```
ON  = 1

OFF = 0
```

Because hardware naturally works with two electrical states, computers use Binary.

---

# Decimal Number System

Humans normally use the Decimal Number System.

Example:

```
0
1
2
3
4
5
6
7
8
9
10
```

Decimal uses:

```
10 Digits

(0-9)
```

---

# Binary Number System

Binary uses only:

```
0

1
```

Example:

```
Decimal     Binary

1           1

2           10

3           11

4           100

5           101
```

---

# What is a Bit?

A Bit (Binary Digit) is the smallest unit of data in a computer.

A bit can contain only one value.

```
0

or

1
```

---

# What is a Byte?

A Byte consists of:

```
8 Bits
```

Example:

```
10101100
```

This is one byte.

---

# Why is 8 Bits Important?

An IPv4 address is divided into four parts.

Each part contains:

```
8 Bits
```

Example:

```
192.168.10.25

↓

192

↓

8 Bits

↓

168

↓

8 Bits

↓

10

↓

8 Bits

↓

25

↓

8 Bits
```

Therefore,

```
IPv4

↓

4 Octets

↓

Each Octet = 8 Bits

↓

Total = 32 Bits
```

---

# Binary Place Values

Each bit has a fixed decimal value.

```
128   64   32   16   8   4   2   1
```

These are called Place Values.

---

# Example

Binary Number:

```
11001010
```

Write place values.

```
128 64 32 16 8 4 2 1

 1   1  0  0 1 0 1 0
```

Now add only the values having 1.

```
128

+

64

+

8

+

2

=

202
```

Therefore,

```
11001010

=

202
```

---

# Decimal to Binary Conversion

Example:

Convert

```
25
```

to Binary.

Use place values.

```
128 64 32 16 8 4 2 1

 0   0  0  1 1 0 0 1
```

Binary becomes:

```
00011001
```

Therefore,

```
25

↓

00011001
```

---

# Binary to Decimal Conversion

Example:

```
10110110
```

Place values.

```
128 64 32 16 8 4 2 1

 1   0  1  1 0 1 1 0
```

Add values.

```
128

+

32

+

16

+

4

+

2

=

182
```

Therefore,

```
10110110

=

182
```

---

# Common Decimal to Binary Table

| Decimal | Binary |
|----------|---------|
| 0 | 00000000 |
| 1 | 00000001 |
| 2 | 00000010 |
| 3 | 00000011 |
| 4 | 00000100 |
| 5 | 00000101 |
| 6 | 00000110 |
| 7 | 00000111 |
| 8 | 00001000 |
| 16 | 00010000 |
| 32 | 00100000 |
| 64 | 01000000 |
| 128 | 10000000 |
| 255 | 11111111 |

---

# Binary in IPv4

Example IP:

```
192.168.1.10
```

Binary Representation

```
192

↓

11000000

168

↓

10101000

1

↓

00000001

10

↓

00001010
```

Complete Binary

```
11000000

10101000

00000001

00001010
```

This is how computers actually store IPv4 addresses.

---

# Why is Binary Important in Networking?

Binary helps determine:

- Network Bits
- Host Bits
- CIDR
- Subnet Mask
- Network Address
- Broadcast Address
- Number of Hosts

Without understanding Binary, subnetting becomes difficult.

---

# AWS Perspective

Whenever you create a VPC like:

```
10.0.0.0/16
```

AWS internally performs calculations using Binary to determine:

- Network Address
- Available IP Addresses
- Subnets
- Routing

Although AWS performs these calculations automatically, understanding Binary helps you design better VPC architectures.

---

# Summary

Binary is the foundation of networking.

Every IPv4 address consists of:

- 32 Bits
- 4 Octets
- 8 Bits per Octet

Networking concepts such as CIDR, Subnetting, Route Tables, and VPC all rely on Binary calculations.

---

# Key Takeaways

- Computers understand only Binary (0 and 1).
- A Bit is the smallest unit of data.
- A Byte consists of 8 Bits.
- An IPv4 address contains 32 Bits.
- Each IPv4 address has 4 Octets.
- Binary is used to calculate CIDR and Subnets.
- Understanding Binary makes subnetting much easier.

# CIDR Notation

Before creating a VPC in AWS, you must define an IP address range.

AWS uses **CIDR (Classless Inter-Domain Routing)** to specify the range of IP addresses available for a VPC or Subnet.

Understanding CIDR is one of the most important networking concepts for AWS, Kubernetes, and DevOps.

---

# What is CIDR?

CIDR stands for:

**Classless Inter-Domain Routing**

CIDR is a method of allocating IP addresses and defining network ranges.

Instead of assigning one IP address at a time, CIDR allows us to allocate a block of IP addresses.

Example:

```
10.0.0.0/16
```

This represents an entire network, not a single IP address.

---

# Why Do We Need CIDR?

Imagine a company has 500 servers.

Assigning IP addresses manually would be difficult.

Instead, we assign a CIDR block such as:

```
10.0.0.0/16
```

Now all servers receive IP addresses from this range.

Benefits:

- Easy IP management
- Efficient routing
- Better network planning
- Reduced IP wastage
- Flexible subnet creation

---

# CIDR Format

CIDR consists of two parts.

```
10.0.0.0/16
```

Breaking it down:

```
10.0.0.0

↓

Network Address

------------------------

/16

↓

Prefix Length
```

The number after the slash (/) tells us how many bits are reserved for the network.

---

# Understanding Prefix Length

An IPv4 address contains:

```
32 Bits
```

Example:

```
10.0.0.0/16
```

Means:

```
Network Bits = 16

Host Bits = 16
```

Because

```
32

-

16

=

16
```

---

# Network Bits

Network Bits identify the network.

All devices inside the same network have identical Network Bits.

Example

```
10.0.x.x
```

All devices belong to the same network.

---

# Host Bits

Host Bits identify individual devices inside the network.

Example

```
10.0.0.10

10.0.0.25

10.0.1.100

10.0.200.5
```

The host portion changes for each device.

---

# CIDR Visualization

Example:

```
10.0.0.0/24
```

```
32 Bits

↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓↓

11111111.11111111.11111111.00000000

^^^^^^^^^^^^^^^^^^^^^^^^

Network

                ^^^^^^^^

                 Host
```

24 bits belong to the Network.

8 bits belong to Hosts.

---

# CIDR Examples

## /8

```
10.0.0.0/8
```

Network Bits

```
8
```

Host Bits

```
24
```

Very large network.

---

## /16

```
10.0.0.0/16
```

Network Bits

```
16
```

Host Bits

```
16
```

Commonly used for AWS VPCs.

---

## /24

```
10.0.1.0/24
```

Network Bits

```
24
```

Host Bits

```
8
```

Common subnet size.

---

## /25

```
10.0.1.0/25
```

Network Bits

```
25
```

Host Bits

```
7
```

Smaller subnet.

---

## /26

Network Bits

```
26
```

Host Bits

```
6
```

---

## /27

Network Bits

```
27
```

Host Bits

```
5
```

---

## /28

Network Bits

```
28
```

Host Bits

```
4
```

---

## /29

Network Bits

```
29
```

Host Bits

```
3
```

---

## /30

Network Bits

```
30
```

Host Bits

```
2
```

Mostly used for point-to-point communication.

---

## /31

Network Bits

```
31
```

Host Bits

```
1
```

Rarely used.

---

## /32

Network Bits

```
32
```

Host Bits

```
0
```

Represents a single IP address.

---

# CIDR Cheat Sheet

| CIDR | Total IPs | Usable IPs |
|-------|----------:|-----------:|
| /8 | 16,777,216 | 16,777,214 |
| /16 | 65,536 | 65,534 |
| /24 | 256 | 254 |
| /25 | 128 | 126 |
| /26 | 64 | 62 |
| /27 | 32 | 30 |
| /28 | 16 | 14 |
| /29 | 8 | 6 |
| /30 | 4 | 2 |
| /31 | 2 | 2* |
| /32 | 1 | 1 |

> **Note:** In general networking, `/31` is commonly used for point-to-point links. In AWS VPCs, subnet sizing rules differ and VPC subnets have additional reserved addresses, which we'll discuss later.

---

# AWS Examples

## Example 1

```
VPC

10.0.0.0/16
```

Possible Subnets

```
10.0.1.0/24

10.0.2.0/24

10.0.3.0/24

10.0.4.0/24
```

---

## Example 2

Production VPC

```
172.16.0.0/16
```

Subnets

```
172.16.1.0/24

172.16.2.0/24

172.16.3.0/24
```

---

# CIDR in AWS VPC

When creating a VPC, AWS asks for a CIDR block.

Example:

```
10.0.0.0/16
```

AWS allocates all IP addresses from this range.

Later, you divide this CIDR block into smaller subnets.

Example:

```
VPC

10.0.0.0/16

↓

Public Subnet

10.0.1.0/24

↓

Private Subnet

10.0.2.0/24

↓

Database Subnet

10.0.3.0/24
```

---

# Common Mistakes

- Confusing CIDR with an individual IP address.
- Assuming `/24` means 24 IP addresses (it means 24 **network bits**, not 24 IPs).
- Choosing a VPC CIDR block that overlaps with another network.
- Allocating a very small CIDR block for a growing environment.

---

# Summary

CIDR defines the IP address range available to a network.

It specifies:

- Network Size
- Number of Host Addresses
- Network Bits
- Host Bits

CIDR is used in:

- AWS VPC
- Subnets
- Route Tables
- Firewalls
- Kubernetes Networking

---

# Key Takeaways

- CIDR stands for **Classless Inter-Domain Routing**.
- An IPv4 address has **32 bits**.
- The number after `/` indicates the **network bits**.
- The remaining bits are **host bits**.
- A larger prefix (for example, `/28`) creates a **smaller network**.
- A smaller prefix (for example, `/16`) creates a **larger network**.
- Every AWS VPC must be created with a CIDR block.
- Subnets are created by dividing the VPC's CIDR block into smaller CIDR ranges.

#  Subnetting

Subnetting is one of the most important networking concepts in AWS.

When creating a VPC, AWS provides a large CIDR block. Instead of using the entire network as one large network, we divide it into smaller networks called **Subnets**.

Subnetting helps improve network organization, security, scalability, and IP address management.

---

# What is Subnetting?

Subnetting is the process of dividing a large network into multiple smaller logical networks called **Subnets**.

Instead of managing one large network, we create multiple smaller networks for different purposes.

Example:

```
VPC

10.0.0.0/16

↓

Subnet 1

10.0.1.0/24

↓

Subnet 2

10.0.2.0/24

↓

Subnet 3

10.0.3.0/24
```

---

# Why Do We Need Subnetting?

Without subnetting:

- Large Broadcast Domains
- Difficult Network Management
- Lower Security
- Poor Performance
- IP Address Wastage

With subnetting:

- Better Security
- Better Performance
- Easy Management
- Efficient IP Address Usage
- Better Scalability

---

# Real World Example

Imagine a company has three departments.

- HR
- Finance
- Development

Instead of connecting all computers to one network:

```
10.0.0.0/16
```

They create separate subnets.

```
HR

10.0.1.0/24

-------------------

Finance

10.0.2.0/24

-------------------

Development

10.0.3.0/24
```

Each department has its own network.

---

# Benefits of Subnetting

- Better Network Organization
- Better Security
- Reduced Broadcast Traffic
- Improved Performance
- Easy Troubleshooting
- Better IP Utilization

---

# Network Address

Every subnet has a **Network Address**.

It identifies the subnet itself.

Example

```
10.0.1.0/24
```

Network Address

```
10.0.1.0
```

This address cannot be assigned to a device.

---

# Broadcast Address

The Broadcast Address is the last IP Address in a subnet.

It is used to send data to all devices inside that subnet.

Example

```
10.0.1.255
```

This address also cannot be assigned to a device.

---

# Host Addresses

Host addresses are the usable IP addresses available for devices.

Example

```
Subnet

10.0.1.0/24
```

Usable Range

```
10.0.1.1

↓

10.0.1.254
```

These addresses can be assigned to:

- EC2 Instances
- Databases
- Load Balancers
- Network Appliances

---

# First Usable IP

The first usable IP Address is immediately after the Network Address.

Example

```
Network

10.0.1.0

↓

First Host

10.0.1.1
```

---

# Last Usable IP

The last usable IP Address is immediately before the Broadcast Address.

Example

```
Broadcast

10.0.1.255

↓

Last Host

10.0.1.254
```

---

# Total Number of IP Addresses

Formula

```
2^(Host Bits)
```

Example

```
/24

Host Bits = 8

↓

2^8

↓

256 IP Addresses
```

---

# Usable IP Addresses

Formula

```
2^(Host Bits)

-

2
```

The two reserved addresses are:

- Network Address
- Broadcast Address

Example

```
/24

↓

256

↓

254 Usable Hosts
```

---

# Common CIDR Examples

| CIDR | Host Bits | Total IPs | Usable IPs |
|-------|-----------|----------:|-----------:|
| /24 | 8 | 256 | 254 |
| /25 | 7 | 128 | 126 |
| /26 | 6 | 64 | 62 |
| /27 | 5 | 32 | 30 |
| /28 | 4 | 16 | 14 |
| /29 | 3 | 8 | 6 |
| /30 | 2 | 4 | 2 |

---

# AWS Example

Suppose we create a VPC.

```
10.0.0.0/16
```

Now create three subnets.

```
Public Subnet

10.0.1.0/24

--------------------

Private Subnet

10.0.2.0/24

--------------------

Database Subnet

10.0.3.0/24
```

Each subnet has its own IP address range.

---

# Public Subnet

A Public Subnet has a route to the Internet Gateway.

Resources placed here can communicate with the Internet.

Examples

- Web Servers
- Bastion Hosts
- Load Balancers

---

# Private Subnet

A Private Subnet does not have a direct route to the Internet.

Resources remain protected from direct internet access.

Examples

- Application Servers
- Databases
- Internal Services

---

# AWS Reserved IP Addresses

AWS reserves the first **4 IP addresses** and the **last IP address** in every subnet.

For example:

```
Subnet

10.0.1.0/24
```

AWS reserves:

```
10.0.1.0

Network Address

--------------------

10.0.1.1

Reserved by AWS

--------------------

10.0.1.2

Reserved by AWS

--------------------

10.0.1.3

Reserved by AWS

--------------------

10.0.1.255

Reserved by AWS
```

Because of this, a `/24` subnet in AWS has:

```
256 Total IPs

↓

251 Usable IPs
```

> **Important:** In standard networking, a `/24` subnet has **254 usable IPs** (excluding the network and broadcast addresses). In AWS VPC, **5 IP addresses are reserved**, so only **251 IPs** are available for your resources.

---

# AWS Subnet Design Example

```
VPC

10.0.0.0/16

│

├── Public Subnet AZ-A

│      10.0.1.0/24

│

├── Private App Subnet AZ-A

│      10.0.2.0/24

│

├── Database Subnet AZ-A

│      10.0.3.0/24

│

├── Public Subnet AZ-B

│      10.0.11.0/24

│

├── Private App Subnet AZ-B

│      10.0.12.0/24

│

└── Database Subnet AZ-B

       10.0.13.0/24
```

This design supports High Availability by distributing resources across multiple Availability Zones.

---

# Common Mistakes

- Creating overlapping subnet CIDR blocks.
- Creating subnets that are too small for future growth.
- Confusing VPC CIDR with Subnet CIDR.
- Assuming all IP addresses are usable in AWS.
- Forgetting AWS reserves 5 IP addresses in each subnet.

---

# Summary

Subnetting divides a large network into smaller logical networks.

Benefits include:

- Better Security
- Better Performance
- Better Scalability
- Efficient IP Management
- Easier Troubleshooting

Subnetting is the foundation of AWS networking and is used in VPC, Route Tables, NAT Gateway, Internet Gateway, and Kubernetes networking.

---

# Key Takeaways

- Subnetting divides a large network into smaller networks.
- Every subnet has a Network Address and a Broadcast Address.
- The first usable IP is after the Network Address.
- The last usable IP is before the Broadcast Address.
- Total IPs = 2^(Host Bits).
- Standard usable IPs = Total IPs − 2.
- In AWS, 5 IP addresses are reserved in every subnet.
- Public Subnets provide internet access, while Private Subnets protect internal resources.

# CIDR & Subnetting Practice

Now that we understand Binary, CIDR, and Subnetting, let's solve practical examples.

These are the same types of questions commonly asked in AWS, DevOps, and Networking interviews.

---

# Formula 1 : Total Number of IP Addresses

```
Total IP Addresses = 2^(Host Bits)
```

---

# Formula 2 : Usable IP Addresses

General Networking

```
Usable IPs = 2^(Host Bits) - 2
```

AWS VPC

```
Usable IPs = Total IPs - 5
```

AWS reserves five IP addresses in every subnet.

---

# Formula 3 : Host Bits

```
Host Bits = 32 - CIDR
```

Example

```
/24

↓

32 - 24

↓

8 Host Bits
```

---

# Formula 4 : Network Bits

```
Network Bits = CIDR Value
```

Example

```
/16

↓

16 Network Bits
```

---

# CIDR Quick Reference

| CIDR | Host Bits | Total IPs | Usable Hosts (General) | Usable Hosts (AWS) |
|------|-----------|-----------|------------------------|--------------------|
| /24 | 8 | 256 | 254 | 251 |
| /25 | 7 | 128 | 126 | 123 |
| /26 | 6 | 64 | 62 | 59 |
| /27 | 5 | 32 | 30 | 27 |
| /28 | 4 | 16 | 14 | 11 |
| /29 | 3 | 8 | 6 | 3 |
| /30 | 2 | 4 | 2 | Not valid for AWS subnet creation |

> **Note:** AWS VPC subnets have minimum size requirements. Very small CIDR blocks such as `/30` are not supported for creating VPC subnets.

---

# Example 1

Network

```
10.0.0.0/24
```

Network Bits

```
24
```

Host Bits

```
8
```

Total IPs

```
2⁸

=

256
```

General Networking

```
Usable Hosts

254
```

AWS

```
Usable Hosts

251
```

---

# Example 2

```
10.0.0.0/25
```

Host Bits

```
7
```

Total IPs

```
128
```

General Networking

```
126
```

AWS

```
123
```

---

# Example 3

```
10.0.0.0/26
```

Host Bits

```
6
```

Total IPs

```
64
```

General Networking

```
62
```

AWS

```
59
```

---

# Example 4

```
10.0.0.0/27
```

Total IPs

```
32
```

AWS

```
27
```

---

# Example 5

```
10.0.0.0/28
```

Total IPs

```
16
```

AWS

```
11
```

---

# Example 6

```
10.0.0.0/29
```

Total IPs

```
8
```

AWS

```
3
```

---

# Example 7

Company Requirement

```
Need around 200 Servers
```

Best Choice

```
/24
```

Reason

```
251 usable IPs in AWS.
```

---

# Example 8

Company Requirement

```
Need around 50 Servers
```

Best Choice

```
/26
```

Reason

```
59 usable IPs.
```

---

# Example 9

Company Requirement

```
Need around 20 Servers
```

Best Choice

```
/27
```

Reason

```
27 usable IPs.
```

---

# Example 10

Company Requirement

```
Need around 8 Servers
```

Best Choice

```
/28
```

Reason

```
11 usable IPs.
```

---

# AWS VPC Example

Create a VPC

```
10.0.0.0/16
```

Divide into Subnets

```
Public

10.0.1.0/24

↓

Private App

10.0.2.0/24

↓

Database

10.0.3.0/24

↓

Management

10.0.4.0/24
```

Every subnet belongs to the same VPC.

---

# Production Example

A Production Application requires:

```
Public Load Balancer

↓

Application Servers

↓

Database
```

Subnet Design

```
VPC

10.0.0.0/16

│

├── Public Subnet

│     10.0.1.0/24

│

├── Private App Subnet

│     10.0.2.0/24

│

└── Database Subnet

      10.0.3.0/24
```

This is one of the most common AWS production architectures.

---

# CIDR Interview Tricks

### Trick 1

Larger CIDR Number

```
↓

Smaller Network
```

Example

```
/28

↓

Smaller Network
```

---

### Trick 2

Smaller CIDR Number

```
↓

Larger Network
```

Example

```
/16

↓

Large Network
```

---

### Trick 3

Never Memorize

Instead remember

```
Host Bits

↓

2^(Host Bits)
```

You'll always find the answer.

---

### Trick 4

AWS Interview Question

Question

```
How many usable IPs are available in a /24 subnet?
```

General Networking

```
254
```

AWS

```
251
```

Always clarify whether the interviewer is asking about **standard networking** or **AWS VPC**.

---

# Common CIDR Mistakes

❌ Thinking `/24` means 24 IP addresses.

Correct:

```
24 Network Bits
```

---

❌ Forgetting AWS reserves five IP addresses.

---

❌ Choosing overlapping CIDR ranges.

Example

```
VPC A

10.0.0.0/16

VPC B

10.0.1.0/24
```

These overlap and cannot be peered without redesign.

---

❌ Creating very small subnets for production.

Always leave room for future growth.

---

# Summary

CIDR determines:

- Network Size
- Host Capacity
- Number of Subnets
- Routing Efficiency

Subnetting divides a large network into multiple smaller networks.

Together, CIDR and Subnetting form the foundation of:

- AWS VPC
- Subnets
- Route Tables
- Internet Gateway
- NAT Gateway
- Kubernetes Networking

---

# Quick Revision

| CIDR | AWS Usable IPs |
|------|---------------:|
| /24 | 251 |
| /25 | 123 |
| /26 | 59 |
| /27 | 27 |
| /28 | 11 |
| /29 | 3 |

---

# Important Interview Points

- CIDR defines the IP range of a network.
- Host Bits determine the number of available IP addresses.
- Total IPs = 2^(Host Bits).
- General usable IPs = Total IPs − 2.
- AWS reserves five IP addresses in every subnet.
- Choose subnet sizes based on future growth, not just current requirements.
- Avoid overlapping CIDR blocks across VPCs.
- Larger CIDR prefix (/28) means a smaller network.
- Smaller CIDR prefix (/16) means a larger network.
