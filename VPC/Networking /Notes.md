# Networking Fundamentals

Before learning AWS VPC, it is important to understand the fundamentals of networking. Every AWS networking service, including VPC, Subnets, Route Tables, Internet Gateway, NAT Gateway, and Security Groups, is built on these concepts.

Understanding networking first makes AWS much easier to learn.

---

# What is Networking?

Networking is the process of connecting two or more devices so they can communicate and exchange data.

These devices may include:

- Computers
- Servers
- Mobile Phones
- Printers
- Routers
- Switches
- IoT Devices

The communication can happen inside a company, within a home, or across the Internet.

---

# Why Do We Need Networking?

Without networking:

- Computers cannot communicate.
- Files cannot be shared.
- Websites cannot be accessed.
- Emails cannot be sent.
- Cloud services like AWS cannot function.

Networking enables communication between devices regardless of their physical location.

---

# Real World Example

Imagine you are working in a company.

Your laptop needs to:

- Access company applications
- Connect to databases
- Access shared folders
- Browse the internet
- Connect to AWS resources

All these operations are possible because of networking.

---

# What is a Network?

A Network is a collection of devices connected together for communication and resource sharing.

Resources may include:

- Files
- Applications
- Internet Connection
- Printers
- Databases

Example:

```
Laptop 1

      │

Laptop 2

      │

Switch

      │

Server
```

All devices are connected and can communicate with each other.

---

# Types of Networks

Networks are classified based on geographical coverage.

AWS networking concepts are built on these networking fundamentals.

---

# 1. PAN (Personal Area Network)

A Personal Area Network connects devices within a very short distance.

Usually within:

```
1 - 10 meters
```

Examples:

- Bluetooth Headphones
- Smart Watch
- Wireless Keyboard
- Wireless Mouse

Real World Example:

Your smartwatch synchronizes with your mobile phone using Bluetooth.

This is a PAN.

---

# 2. LAN (Local Area Network)

A Local Area Network connects devices inside a limited geographical area.

Examples:

- Home Network
- Office Network
- College Campus
- Computer Lab

Distance:

Usually within a building.

Example:

```
Laptop

    │

Switch

    │

Printer

    │

Server
```

Advantages

- High Speed
- Low Cost
- Easy File Sharing
- Secure Communication

---

# 3. MAN (Metropolitan Area Network)

A Metropolitan Area Network connects multiple LANs across a city.

Examples:

- University Campuses
- Government Offices
- Banks
- Large Organizations

Example

```
Office A

      │

City Network

      │

Office B

      │

Office C
```

Coverage:

Entire City

---

# 4. WAN (Wide Area Network)

A Wide Area Network connects devices across countries or continents.

The Internet is the world's largest WAN.

Examples:

- AWS Cloud
- Microsoft Azure
- Google Cloud
- Banking Networks
- International Company Networks

Example

```
India Office

        │

Internet

        │

USA Office

        │

AWS Cloud
```

Coverage:

Worldwide

---

# PAN vs LAN vs MAN vs WAN

| Network | Full Form | Coverage | Example |
|----------|-----------|----------|----------|
| PAN | Personal Area Network | Few Meters | Bluetooth |
| LAN | Local Area Network | Building | Office Network |
| MAN | Metropolitan Area Network | City | University |
| WAN | Wide Area Network | Country / World | Internet |

---

# Client and Server

Networking mainly involves two components.

## Client

A Client is a device that requests services or resources.

Examples

- Laptop
- Mobile Phone
- Browser

Example

When you open Google Chrome and visit:

```
www.amazon.com
```

Your browser acts as a Client.

---

## Server

A Server is a computer that provides services to clients.

Examples

- Web Server
- Database Server
- Mail Server
- Application Server

AWS EC2 instances often act as servers.

---

# Client-Server Architecture

```
Client

(Laptop)

      │

Internet

      │

AWS EC2

(Web Server)
```

The client sends a request.

The server processes the request.

The server sends the response back.

---

# Request and Response

Every communication follows this process.

```
Client

↓

Request

↓

Server

↓

Processing

↓

Response

↓

Client
```

Example

```
Browser

↓

Open google.com

↓

Google Server

↓

Returns Webpage

↓

Browser Displays Website
```

---

# What is Data?

Data is the information transmitted between devices.

Examples:

- Images
- Videos
- Text
- Documents
- API Requests
- Emails

---

# What is a Packet?

Large amounts of data are divided into smaller pieces called Packets before transmission.

Instead of sending an entire file at once, networking devices send multiple packets.

Example

A 100 MB file

↓

Split into thousands of packets

↓

Packets travel across the Internet

↓

Destination reassembles them

---

# Benefits of Packet Transmission

- Faster communication
- Better reliability
- Efficient bandwidth usage
- Error recovery
- Easy routing

---

# Common Network Devices

## Router

A Router connects different networks.

Example

Your home router connects your local network to the Internet.

Functions

- Connects Networks
- Routes Packets
- Provides Internet Access

---

## Switch

A Switch connects devices within the same LAN.

Functions

- Connects Computers
- Connects Servers
- Connects Printers

Switches operate inside local networks.

---

## Hub

A Hub also connects devices.

However, it broadcasts data to every connected device.

Today, switches have almost completely replaced hubs.

---

## Modem

A Modem connects your home or office network to your Internet Service Provider (ISP).

Without a modem, Internet connectivity is not possible.

---

## Firewall

A Firewall protects a network by allowing or blocking traffic based on security rules.

AWS Security Groups and Network ACLs are examples of firewalls.

---

# Summary

Networking is the foundation of cloud computing.

Understanding networking concepts makes it easier to learn:

- AWS VPC
- Subnets
- Route Tables
- Internet Gateway
- NAT Gateway
- Security Groups
- Network ACL
- Load Balancers
- Kubernetes Networking

---

# Key Takeaways

- Networking connects devices for communication.
- A Network is a collection of connected devices.
- PAN covers a few meters.
- LAN covers a building or office.
- MAN covers a city.
- WAN covers countries and the Internet.
- A Client requests services.
- A Server provides services.
- Data is transferred in the form of packets.

#  IP Addressing

An IP Address is one of the most fundamental concepts in networking. Every device connected to a network must have a unique IP Address to communicate with other devices.

Without an IP Address, devices cannot identify each other or exchange data.

---

# What is an IP Address?

IP stands for **Internet Protocol**.

An IP Address is a unique numerical address assigned to every device connected to a network.

It acts like a home address.

Just as a courier needs your home address to deliver a package, a computer needs an IP Address to send data to another device.

---

# Why Do We Need an IP Address?

Imagine there are thousands of computers connected to the Internet.

When one computer sends data, how does it know where the destination computer is?

The answer is the **IP Address**.

Every request sent over a network contains:

- Source IP Address
- Destination IP Address

Without an IP Address, communication is impossible.

---

# Real World Example

Suppose you open:

```
www.amazon.com
```

The communication happens like this:

```
Your Laptop

↓

DNS converts amazon.com into an IP Address

↓

Amazon Server

↓

Response Returned

↓

Website Opens
```

Although users remember domain names, computers communicate using IP Addresses.

---

# What is Internet Protocol (IP)?

Internet Protocol is a set of rules that defines how data is transmitted between devices over a network.

Its primary responsibilities are:

- Assigning IP Addresses
- Identifying Source and Destination
- Routing Packets to the Correct Device

---

# Types of IP Addresses

There are two main versions of IP Addresses:

- IPv4
- IPv6

---

# IPv4

IPv4 stands for **Internet Protocol Version 4**.

It is the most commonly used IP addressing system today.

An IPv4 address consists of **32 bits** divided into **4 octets**.

Example:

```
192.168.10.15
```

Each octet ranges from:

```
0 - 255
```

Example:

```
172.16.100.25
```

Structure:

```
192 . 168 . 10 . 15

 ↑      ↑      ↑     ↑

Octet  Octet  Octet Octet
```

---

# IPv6

IPv6 stands for **Internet Protocol Version 6**.

It was introduced because IPv4 addresses are limited and the number of internet-connected devices has grown rapidly.

IPv6 consists of **128 bits**.

Example:

```
2001:db8:85a3::8a2e:370:7334
```

Advantages:

- Much larger address space
- Better scalability
- Improved routing efficiency
- Built-in support for modern networking

---

# IPv4 vs IPv6

| Feature | IPv4 | IPv6 |
|----------|------|------|
| Address Length | 32-bit | 128-bit |
| Format | Decimal | Hexadecimal |
| Example | 192.168.1.10 | 2001:db8::1 |
| Number of Addresses | ~4.3 Billion | Extremely Large |
| Commonly Used | Yes | Increasing Adoption |

---

# Public IP Address

A Public IP Address is globally unique and reachable over the Internet.

It is assigned by an Internet Service Provider (ISP) or a cloud provider such as AWS.

Examples:

- EC2 Web Server
- Public Load Balancer
- Public Website

Example:

```
Internet

↓

54.210.xx.xx

↓

EC2 Instance
```

Anyone on the Internet can reach the resource if networking and security rules allow it.

---

# Private IP Address

A Private IP Address is used for communication within a private network.

It cannot be accessed directly from the Internet.

Examples:

- EC2 instances in a private subnet
- Office computers
- Database servers
- Application servers

Private IPs improve security by isolating internal resources from direct internet access.

---

# Reserved Private IP Ranges

According to RFC 1918, the following ranges are reserved for private networks.

| CIDR Block | Address Range |
|------------|---------------|
| 10.0.0.0/8 | 10.0.0.0 – 10.255.255.255 |
| 172.16.0.0/12 | 172.16.0.0 – 172.31.255.255 |
| 192.168.0.0/16 | 192.168.0.0 – 192.168.255.255 |

These ranges are commonly used inside organizations and AWS VPCs.

---

# Public IP vs Private IP

| Public IP | Private IP |
|------------|------------|
| Accessible from the Internet | Accessible only within a private network |
| Globally Unique | Can be reused in different networks |
| Assigned by ISP or Cloud Provider | Assigned within the private network |
| Used for Internet-facing resources | Used for internal communication |

---

# Static IP Address

A Static IP Address does not change over time.

It remains assigned to the same device until manually changed.

Examples:

- AWS Elastic IP
- Database Server
- Production Web Server

Advantages:

- Stable connectivity
- Easier DNS management
- Suitable for production workloads

---

# Dynamic IP Address

A Dynamic IP Address is assigned automatically and may change over time.

Most home internet connections and default EC2 public IP addresses are dynamic.

Advantages:

- Automatic allocation
- Efficient IP management
- Lower administrative effort

---

# Static IP vs Dynamic IP

| Static IP | Dynamic IP |
|------------|------------|
| Fixed Address | Changes Automatically |
| Manual Assignment | Automatic Assignment |
| Best for Servers | Best for End Users |
| Predictable | Temporary |

---

# AWS Example

Suppose you launch an EC2 instance.

AWS assigns:

```
Private IP

↓

10.0.1.15
```

If Public IP assignment is enabled:

```
Public IP

↓

13.234.xx.xx
```

If you allocate an Elastic IP:

```
Elastic IP

↓

13.234.xx.xx

↓

Remains the same even after stopping and starting the instance.
```

---

# Summary

Every device on a network requires a unique IP Address for communication.

AWS networking services such as VPC, Subnets, Route Tables, Internet Gateway, NAT Gateway, and Security Groups all rely on IP addressing.

Understanding IP addressing is essential before learning CIDR notation and subnetting.

---

# Key Takeaways

- IP stands for Internet Protocol.
- Every device on a network requires a unique IP Address.
- IPv4 uses 32-bit addresses.
- IPv6 uses 128-bit addresses.
- Public IPs are accessible over the Internet.
- Private IPs are used for internal communication.
- AWS VPC commonly uses private IP ranges.
- Elastic IP is a Static Public IP.
- Default EC2 Public IP is Dynamic.

#  Ports & Protocols

Before two devices communicate over a network, they need more than just an IP Address.

An **IP Address** identifies the destination device, while a **Port Number** identifies the specific application or service running on that device.

For successful communication, both the IP Address and Port Number are required.

---

# What is a Port?

A Port is a logical communication endpoint that allows multiple applications and services to communicate over a network.

Think of it like this:

```
IP Address  → Apartment Building

Port Number → Apartment Number
```

The IP Address tells us which device to reach, while the Port Number tells us which application should receive the request.

---

# Why Do We Need Ports?

Imagine an EC2 instance running:

- SSH Server
- Apache Web Server
- MySQL Database
- Jenkins
- Docker

All these services share the same IP Address.

Ports allow the operating system to identify which application should receive the incoming request.

Without ports, the operating system would not know where to send the network traffic.

---

# Example

Suppose an EC2 instance has the following IP Address:

```
54.210.15.20
```

Services running on the server:

| Service | Port |
|----------|------|
| SSH | 22 |
| HTTP | 80 |
| HTTPS | 443 |
| MySQL | 3306 |

Examples:

```
54.210.15.20:22
```

SSH Connection

```
54.210.15.20:80
```

HTTP Website

```
54.210.15.20:443
```

HTTPS Website

```
54.210.15.20:3306
```

MySQL Database

---

# Port Number Ranges

Port numbers range from:

```
0 - 65535
```

These ports are divided into three categories.

| Range | Category | Purpose |
|--------|----------|---------|
| 0 - 1023 | Well-Known Ports | Standard Services |
| 1024 - 49151 | Registered Ports | Applications |
| 49152 - 65535 | Dynamic / Ephemeral Ports | Temporary Client Ports |

---

# Well-Known Ports (0-1023)

These ports are reserved for commonly used network services.

Examples:

| Port | Service |
|------|----------|
| 20/21 | FTP |
| 22 | SSH |
| 23 | Telnet |
| 25 | SMTP |
| 53 | DNS |
| 80 | HTTP |
| 123 | NTP |
| 143 | IMAP |
| 443 | HTTPS |

---

# Registered Ports (1024-49151)

These ports are used by applications and software.

Examples:

| Port | Application |
|------|-------------|
| 3306 | MySQL |
| 5432 | PostgreSQL |
| 6379 | Redis |
| 8080 | Jenkins / Tomcat |
| 8081 | Nexus Repository |
| 9000 | SonarQube |
| 9090 | Prometheus |
| 9092 | Kafka |
| 9200 | Elasticsearch |
| 27017 | MongoDB |

---

# Dynamic / Ephemeral Ports (49152-65535)

These ports are automatically assigned by the operating system for temporary client-side communication.

Example:

```
Laptop

192.168.1.10:52678

↓

AWS EC2

54.xxx.xxx.xxx:443
```

Port **52678** is automatically assigned by the client.

---

# What is a Protocol?

A Protocol is a set of rules that defines how devices communicate over a network.

Protocols ensure that data is transmitted correctly and understood by both the sender and receiver.

Examples:

- HTTP
- HTTPS
- SSH
- FTP
- DNS
- SMTP

---

# What is TCP?

TCP stands for **Transmission Control Protocol**.

It is a connection-oriented protocol that ensures reliable data delivery.

Before data is transmitted, TCP establishes a connection between the sender and receiver.

### Features

- Reliable Communication
- Error Detection
- Packet Ordering
- Acknowledgements
- Retransmission of Lost Packets

### Common Services Using TCP

- SSH
- HTTP
- HTTPS
- FTP
- MySQL
- PostgreSQL

---

# What is UDP?

UDP stands for **User Datagram Protocol**.

It is a connectionless protocol designed for speed.

UDP sends data without establishing a connection or verifying delivery.

### Features

- Faster Communication
- Low Overhead
- No Error Recovery
- No Packet Ordering

### Common Services Using UDP

- DNS
- DHCP
- NTP
- Voice Calls (VoIP)
- Video Streaming
- Online Gaming

---

# TCP vs UDP

| Feature | TCP | UDP |
|----------|-----|-----|
| Connection | Connection-Oriented | Connectionless |
| Reliability | High | Low |
| Speed | Slower | Faster |
| Error Recovery | Yes | No |
| Packet Ordering | Yes | No |
| Best For | Websites, Databases, SSH | Streaming, Gaming, DNS |

---

# Network Communication Flow

Whenever a client communicates with a server, the following information is exchanged:

```
Source IP

↓

Source Port

↓

Destination IP

↓

Destination Port
```

Example:

```
Client

192.168.1.10:52435

↓

Internet

↓

AWS EC2

54.xxx.xxx.xxx:443
```

- Source IP → Client IP
- Source Port → Temporary Port
- Destination IP → Server IP
- Destination Port → HTTPS (443)

---

# OSI Model (Interview Overview)

The OSI Model is a conceptual framework that explains how data travels across a network.

It consists of seven layers.

| Layer | Name |
|--------|------|
| 7 | Application |
| 6 | Presentation |
| 5 | Session |
| 4 | Transport |
| 3 | Network |
| 2 | Data Link |
| 1 | Physical |

For DevOps interviews, remember:

- Layer 4 → TCP / UDP
- Layer 3 → IP Address
- Layer 7 → HTTP / HTTPS

---

# Common DevOps Ports

| Port | Service | Used For |
|------|----------|----------|
| 22 | SSH | Linux Server Access |
| 53 | DNS | Domain Name Resolution |
| 80 | HTTP | Websites |
| 443 | HTTPS | Secure Websites |
| 3306 | MySQL | Database |
| 5432 | PostgreSQL | Database |
| 6379 | Redis | Cache |
| 6443 | Kubernetes API Server | Kubernetes Control Plane |
| 8080 | Jenkins | CI/CD |
| 8081 | Nexus | Artifact Repository |
| 9000 | SonarQube | Code Quality |
| 9090 | Prometheus | Monitoring |
| 9092 | Kafka | Event Streaming |
| 9200 | Elasticsearch | Search & Logging |
| 27017 | MongoDB | NoSQL Database |
| 50000 | Jenkins Agent | Agent Communication |

---

# AWS Perspective

Almost every AWS networking service depends on ports.

Examples:

- Security Groups control access based on ports.
- Network ACLs allow or deny traffic using ports.
- Load Balancers forward traffic to specific ports.
- EC2 instances listen on application ports.
- RDS databases use default database ports.

---

# Summary

- IP Address identifies a device.
- Port identifies an application running on the device.
- Protocol defines how communication happens.
- TCP provides reliable communication.
- UDP provides faster communication with lower overhead.
- Security Groups and NACLs use ports to control network traffic.

---

# Key Takeaways

- IP identifies the destination device.
- Port identifies the destination service.
- Protocol defines communication rules.
- TCP is reliable and connection-oriented.
- UDP is faster and connectionless.
- DevOps Engineers should remember commonly used service ports.
- Understanding ports is essential for AWS Security Groups, NACLs, Load Balancers, Kubernetes, Docker, and Linux troubleshooting.

- Routers connect different networks.
- Switches connect devices within the same network.
- Firewalls secure networks by controlling traffic.
