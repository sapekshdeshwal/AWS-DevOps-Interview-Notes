# AWS Interview Questions

This document contains frequently asked networking interview questions covering networking fundamentals, IP addressing, ports, protocols, and basic networking concepts.

---

# Networking Fundamentals

## Q1. What is Networking?

### Answer

Networking is the process of connecting two or more devices so they can communicate and exchange data.

Examples of connected devices include:

- Computers
- Servers
- Mobile Phones
- Printers
- Cloud Servers

---

## Q2. Why do we need Networking?

### Answer

Networking allows devices to communicate and share resources.

Examples include:

- File Sharing
- Internet Access
- Email Communication
- Database Connectivity
- Cloud Computing

Without networking, communication between devices would not be possible.

---

## Q3. What is a Network?

### Answer

A Network is a collection of connected devices that communicate with each other to share data and resources.

---

## Q4. What are the different types of Networks?

### Answer

There are four common types:

- PAN (Personal Area Network)
- LAN (Local Area Network)
- MAN (Metropolitan Area Network)
- WAN (Wide Area Network)

---

## Q5. What is PAN?

### Answer

PAN (Personal Area Network) connects devices over a short distance.

Example:

- Bluetooth Headphones
- Smart Watch
- Wireless Keyboard

---

## Q6. What is LAN?

### Answer

LAN (Local Area Network) connects devices within a limited area such as:

- Home
- Office
- School

---

## Q7. What is MAN?

### Answer

MAN (Metropolitan Area Network) connects multiple LANs across a city.

---

## Q8. What is WAN?

### Answer

WAN (Wide Area Network) connects devices over large geographical areas.

Example:

The Internet.

---

## Q9. What is the difference between LAN and WAN?

| LAN | WAN |
|------|------|
| Small Area | Large Area |
| Faster | Relatively Slower |
| Private | Public or Private |
| Office/Home | Internet |

---

## Q10. What is Client-Server Architecture?

### Answer

In Client-Server Architecture:

- Client sends requests.
- Server processes the request.
- Server returns the response.

Example:

Browser → Web Server

---

# IP Addressing

## Q11. What is an IP Address?

### Answer

An IP Address is a unique numerical identifier assigned to every device connected to a network.

It allows devices to identify and communicate with each other.

---

## Q12. Why do we need an IP Address?

### Answer

Every device requires an IP Address so that data can reach the correct destination.

Without IP Addresses, devices cannot communicate.

---

## Q13. What does IP stand for?

### Answer

Internet Protocol.

---

## Q14. What are the two versions of IP?

### Answer

- IPv4
- IPv6

---

## Q15. What is IPv4?

### Answer

IPv4 is a 32-bit IP Address represented in decimal format.

Example:

```
192.168.1.10
```

---

## Q16. What is IPv6?

### Answer

IPv6 is a 128-bit IP Address introduced to overcome IPv4 address exhaustion.

---

## Q17. What is the difference between IPv4 and IPv6?

| IPv4 | IPv6 |
|------|------|
| 32-bit | 128-bit |
| Decimal | Hexadecimal |
| Limited Address Space | Very Large Address Space |

---

## Q18. What is a Public IP Address?

### Answer

A Public IP Address is accessible over the Internet.

Example:

AWS EC2 Public IP

---

## Q19. What is a Private IP Address?

### Answer

A Private IP Address is used for communication inside private networks.

It cannot be accessed directly from the Internet.

---

## Q20. What are the Private IP ranges?

### Answer

```
10.0.0.0/8

172.16.0.0/12

192.168.0.0/16
```

---

## Q21. What is the difference between Public IP and Private IP?

### Answer

Public IP

- Internet Accessible
- Globally Unique

Private IP

- Internal Communication
- Not Internet Accessible

---

## Q22. What is a Static IP?

### Answer

A Static IP remains the same until it is manually changed.

Example:

AWS Elastic IP.

---

## Q23. What is a Dynamic IP?

### Answer

A Dynamic IP changes automatically.

Example:

Default EC2 Public IP.

---

# Ports & Protocols

## Q24. What is a Port?

### Answer

A Port is a logical communication endpoint that identifies the application or service running on a device.

---

## Q25. Why do we need Ports?

### Answer

Multiple applications share the same IP Address.

Ports help identify which application should receive the incoming request.

---

## Q26. What is the Port Range?

### Answer

```
0 - 65535
```

---

## Q27. What are the three Port Categories?

### Answer

- Well-Known Ports (0-1023)
- Registered Ports (1024-49151)
- Dynamic/Ephemeral Ports (49152-65535)

---

## Q28. What is a Protocol?

### Answer

A Protocol is a set of rules that defines how devices communicate over a network.

---

## Q29. What is TCP?

### Answer

TCP (Transmission Control Protocol) is a connection-oriented protocol that provides reliable communication.

---

## Q30. What is UDP?

### Answer

UDP (User Datagram Protocol) is a connectionless protocol that provides faster communication with lower overhead.

---

## Q31. Difference between TCP and UDP?

| TCP | UDP |
|------|------|
| Reliable | Faster |
| Connection-Oriented | Connectionless |
| Error Recovery | No Error Recovery |
| Packet Ordering | No Packet Ordering |

---

## Q32. Which protocol is used by SSH?

### Answer

TCP

---

## Q33. Which protocol is used by HTTP?

### Answer

TCP

---

## Q34. Which protocol is commonly used by DNS?

### Answer

UDP

(TCP may also be used for specific operations like zone transfers.)

---

# Production Scenario Questions

## Q35. You cannot access a website hosted on an EC2 instance. What will you check?

### Answer

- Public IP
- Security Group
- Port 80/443
- Internet Gateway
- Route Table
- Web Server Status

---

## Q36. Why is a Private IP not accessible from the Internet?

### Answer

Private IP addresses are designed for internal communication and are not routable over the public Internet.

---

## Q37. Why does an EC2 instance need both an IP Address and a Port?

### Answer

The IP Address identifies the destination device, while the Port identifies the application or service running on that device.

---

## Q38. Why is TCP preferred for websites?

### Answer

TCP ensures reliable and ordered delivery of data, which is important for web applications.

---

## Rapid Fire Questions

### Q39. What is the full form of IP?

**Answer:** Internet Protocol

---

### Q40. What is the full form of TCP?

**Answer:** Transmission Control Protocol

---

### Q41. What is the full form of UDP?

**Answer:** User Datagram Protocol

---

### Q42. Which IP version is most commonly used today?

**Answer:** IPv4

---

### Q43. Which IP version provides a larger address space?

**Answer:** IPv6

---

### Q44. Which port is used by SSH?

**Answer:** 22

---

### Q45. Which port is used by HTTP?

**Answer:** 80

---

### Q46. Which port is used by HTTPS?

**Answer:** 443

---

### Q47. Which port is used by DNS?

**Answer:** 53

---

### Q48. Which port is used by MySQL?

**Answer:** 3306

---

### Q49. Which port is used by PostgreSQL?

**Answer:** 5432

---

### Q50. What is the range of Dynamic Ports?

**Answer:**

```
49152 - 65535
```

---

# Interview Tips

- Understand the difference between **IP Address**, **Port**, and **Protocol**.
- Remember the private IP address ranges defined by RFC 1918.
- Know the differences between IPv4 and IPv6.
- Be able to explain TCP vs UDP with practical examples.
- Memorize commonly used DevOps ports such as **22, 53, 80, 443, 3306, 5432, 6379, 6443, 8080, and 9090**.
- In AWS networking interviews, relate IP addresses, ports, and protocols to **VPC, Security Groups, Network ACLs, Load Balancers, and EC2**.
