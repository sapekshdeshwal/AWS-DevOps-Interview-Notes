# Interview Questions (CIDR & Subnetting)

This document contains frequently asked interview questions on Binary, CIDR, Subnetting, IP Address Calculations, AWS Reserved IPs, and Production Scenarios.

---

# Binary Basics

## Q1. Why do computers use Binary instead of Decimal?

### Answer

Computers use Binary because electronic circuits have only two states:

- ON (1)
- OFF (0)

All processing inside a computer is performed using Binary.

---

## Q2. What is a Bit?

### Answer

A Bit (Binary Digit) is the smallest unit of data.

It can contain only:

```
0

or

1
```

---

## Q3. What is a Byte?

### Answer

A Byte consists of:

```
8 Bits
```

---

## Q4. How many bits are present in an IPv4 Address?

### Answer

```
32 Bits
```

---

## Q5. Why is Binary important in Networking?

### Answer

Binary is used to calculate:

- Network Bits
- Host Bits
- CIDR
- Subnet Mask
- Network Address
- Broadcast Address

---

# CIDR

## Q6. What is CIDR?

### Answer

CIDR stands for:

**Classless Inter-Domain Routing**

It is a method used to define IP address ranges.

Example:

```
10.0.0.0/16
```

---

## Q7. Why do we need CIDR?

### Answer

CIDR helps:

- Allocate IP ranges
- Reduce IP wastage
- Improve routing
- Create subnets

---

## Q8. What does /24 mean?

### Answer

It means:

```
24 Network Bits

8 Host Bits
```

It does NOT mean 24 IP addresses.

---

## Q9. What does /16 mean?

### Answer

```
16 Network Bits

16 Host Bits
```

---

## Q10. What does /32 represent?

### Answer

A single IP Address.

---

## Q11. Which CIDR creates a larger network?

### Answer

```
/16
```

Smaller CIDR prefix → Larger Network.

---

## Q12. Which CIDR creates a smaller network?

### Answer

```
/28
```

Larger CIDR prefix → Smaller Network.

---

# Network & Host Bits

## Q13. What are Network Bits?

### Answer

Network Bits identify the network.

All devices in the same network share the same Network Bits.

---

## Q14. What are Host Bits?

### Answer

Host Bits identify individual devices inside the network.

---

## Q15. How do you calculate Host Bits?

### Answer

Formula:

```
Host Bits

=

32

-

CIDR
```

Example:

```
/24

↓

32-24

↓

8 Host Bits
```

---

# Subnetting

## Q16. What is Subnetting?

### Answer

Subnetting is the process of dividing a large network into multiple smaller logical networks.

---

## Q17. Why do we need Subnetting?

### Answer

Subnetting improves:

- Security
- Performance
- Scalability
- Network Management
- IP Address Utilization

---

## Q18. What is a Network Address?

### Answer

The first IP Address of a subnet.

It identifies the subnet.

It cannot be assigned to a host.

---

## Q19. What is a Broadcast Address?

### Answer

The last IP Address in a subnet.

It is used to send data to all devices in the subnet.

It cannot be assigned to a host.

---

## Q20. What is the First Usable IP?

### Answer

The IP Address immediately after the Network Address.

Example:

```
10.0.1.1
```

---

## Q21. What is the Last Usable IP?

### Answer

The IP Address immediately before the Broadcast Address.

Example:

```
10.0.1.254
```

---

## Q22. What is the formula to calculate Total IP Addresses?

### Answer

```
2^(Host Bits)
```

---

## Q23. What is the formula to calculate Usable IP Addresses?

### Answer

General Networking

```
2^(Host Bits) - 2
```

AWS

```
Total IPs - 5
```

---

## Q24. How many Total IP Addresses are available in /24?

### Answer

```
256
```

---

## Q25. How many Usable IP Addresses are available in /24?

### Answer

General Networking

```
254
```

AWS

```
251
```

---

## Q26. Why are there only 251 usable IPs in AWS for a /24 subnet?

### Answer

AWS reserves five IP addresses in every subnet for networking purposes.

---

# AWS Specific Questions

## Q27. Which IP Addresses does AWS reserve?

### Answer

AWS reserves:

- First IP (Network Address)
- Next three IP addresses for AWS networking functions
- Last IP (Reserved by AWS)

Total Reserved:

```
5 IP Addresses
```

---

## Q28. Can you use all IP Addresses in an AWS subnet?

### Answer

No.

AWS reserves five IP addresses.

---

## Q29. Can overlapping CIDR Blocks exist in VPC Peering?

### Answer

No.

VPC Peering requires non-overlapping CIDR ranges.

---

## Q30. What CIDR Block would you choose for a new VPC?

### Answer

A common choice is:

```
10.0.0.0/16
```

because it provides flexibility for future subnet creation.

---

# Scenario Based Questions

## Q31. Your company expects around 200 EC2 instances in one subnet. Which CIDR would you choose?

### Answer

```
/24
```

AWS provides:

```
251 Usable IPs
```

---

## Q32. Your application requires only 20 EC2 instances. Which subnet would you choose?

### Answer

```
/27
```

Provides:

```
27 Usable IPs in AWS
```

---

## Q33. Your production VPC is running out of IP addresses. What should you do?

### Answer

Possible solutions:

- Create additional subnets.
- Associate an additional IPv4 CIDR block with the VPC.
- Plan larger CIDR ranges during the design phase.

---

## Q34. Why should overlapping CIDR blocks be avoided?

### Answer

Overlapping CIDRs cause routing conflicts and prevent services like VPC Peering from working correctly.

---

## Q35. A developer created a /28 subnet but wants to launch 20 EC2 instances. Will it work?

### Answer

No.

A /28 subnet provides:

- 16 Total IPs
- 11 Usable IPs in AWS

This is insufficient for 20 instances.

---

# Rapid Fire Questions

## Q36. What is CIDR?

**Answer:** Classless Inter-Domain Routing.

---

## Q37. How many bits are in IPv4?

**Answer:** 32 Bits.

---

## Q38. What is the formula for Total IPs?

**Answer:**

```
2^(Host Bits)
```

---

## Q39. What is the formula for Host Bits?

**Answer:**

```
32 - CIDR
```

---

## Q40. Which CIDR has more hosts: /24 or /28?

**Answer:** /24.

---

## Q41. Which CIDR is larger: /16 or /24?

**Answer:** /16.

---

## Q42. Which CIDR represents a single IP?

**Answer:** /32.

---

## Q43. How many IPs are reserved by AWS?

**Answer:** 5.

---

## Q44. Can overlapping CIDR ranges be peered?

**Answer:** No.

---

## Q45. Which subnet is commonly used in AWS?

**Answer:** /24.

---

## Q46. What is the first IP of a subnet called?

**Answer:** Network Address.

---

## Q47. What is the last IP of a subnet called?

**Answer:** Broadcast Address.

---

## Q48. Which address identifies the network?

**Answer:** Network Address.

---

## Q49. Which address sends packets to all hosts in a subnet?

**Answer:** Broadcast Address.

---

## Q50. Why is subnetting important in AWS?

**Answer:**

- Better Security
- Better Network Organization
- Better Scalability
- Efficient IP Utilization
- Easier Network Management

---

# Interview Tips

- Never say **/24 means 24 IP addresses**. It means **24 network bits**.
- Remember the formula:
  - **Host Bits = 32 − CIDR**
  - **Total IPs = 2^(Host Bits)**
- Clarify whether the interviewer is asking about **general networking** or **AWS VPC**, because AWS reserves **5 IP addresses** in every subnet.
- Be prepared to explain **why** you would choose a `/24`, `/26`, or `/27` subnet based on the expected number of resources and future growth.
- Avoid overlapping CIDR ranges when designing VPCs, especially if VPC Peering or Transit Gateway connectivity may be required later.
