# AWS Security Groups

## What is a Security Group?

A Security Group is a **virtual firewall** that controls inbound and outbound traffic for AWS resources such as EC2 instances.

It allows or denies network traffic based on defined rules, helping protect AWS resources from unauthorized access.

Security Groups are associated with the **Elastic Network Interface (ENI)** of an EC2 instance.

---

# Why do we need Security Groups?

Imagine you launch an EC2 instance with a web application.

Without any security, anyone on the internet could try to access:

- SSH (22)
- HTTP (80)
- HTTPS (443)
- Database Ports
- Application Ports

This creates a major security risk.

Security Groups allow you to control who can access your EC2 instance and on which ports.

---

# Real World Example

Suppose your company hosts a web application.

Requirements:

- Users should access the website on HTTPS (443).
- Developers should access the server using SSH (22).
- The database should only be accessible from the Application Server.

Security Groups make this possible by allowing only the required traffic.

---

# How Security Groups Work

```
                Internet
                     │
         -----------------------
         |                     |
   Allowed Traffic       Blocked Traffic
         │
   Security Group
         │
     EC2 Instance
```

Security Groups evaluate traffic before it reaches the EC2 instance.

---

# Key Features

- Virtual Firewall
- Instance Level Security
- Stateful Firewall
- Allow Rules Only
- Supports IPv4 & IPv6
- Controls Inbound and Outbound Traffic
- Can be attached to multiple EC2 Instances
- Multiple Security Groups can be attached to one EC2 Instance

---

# Components of a Security Group

Each Security Group rule consists of:

- Protocol
- Port Range
- Source (Inbound)
- Destination (Outbound)
- Description (Optional)

---

# Inbound Rules

Inbound Rules control incoming traffic to an EC2 instance.

Example:

| Protocol | Port | Source | Purpose |
|----------|------|---------|----------|
| TCP | 22 | My Public IP | SSH |
| TCP | 80 | 0.0.0.0/0 | HTTP |
| TCP | 443 | 0.0.0.0/0 | HTTPS |

---

# Outbound Rules

Outbound Rules control traffic leaving the EC2 instance.

By default, AWS allows all outbound traffic.

Example:

| Protocol | Port | Destination |
|----------|------|-------------|
| All Traffic | All | 0.0.0.0/0 |

---

# Common Protocols and Ports

| Protocol | Port | Purpose |
|----------|------|----------|
| SSH | 22 | Remote Login |
| HTTP | 80 | Website |
| HTTPS | 443 | Secure Website |
| FTP | 21 | File Transfer |
| RDP | 3389 | Windows Remote Desktop |
| MySQL | 3306 | MySQL Database |
| PostgreSQL | 5432 | PostgreSQL Database |
| MongoDB | 27017 | MongoDB |
| Redis | 6379 | Redis |

---

# Understanding Ports

A Port is a logical communication endpoint used by applications to send and receive network traffic.

Example:

- SSH uses Port 22.
- HTTP uses Port 80.
- HTTPS uses Port 443.

Think of a server as a building and ports as different doors.

Each application listens on a specific door (port).

---

# Understanding Protocols

A Protocol defines how data is transmitted over a network.

Common protocols:

- TCP
- UDP
- ICMP

---

# TCP vs UDP

| TCP | UDP |
|------|-----|
| Connection Oriented | Connectionless |
| Reliable | Faster |
| Error Checking | No Error Recovery |
| Used by HTTP, HTTPS, SSH | Used by DNS, Streaming, Gaming |

---

# What is CIDR?

CIDR (Classless Inter-Domain Routing) is used to define a range of IP addresses.

Examples:

```
0.0.0.0/0
```

Allows access from anywhere on the internet.

```
192.168.1.10/32
```

Allows only one specific IP address.

```
10.0.0.0/16
```

Allows access from the entire VPC subnet range.

---

# What is a Stateful Firewall?

Security Groups are **Stateful**.

This means:

If inbound traffic is allowed, the response traffic is automatically allowed.

You do not need to create separate outbound rules for return traffic.

Example:

Laptop

↓

SSH Request

↓

Security Group

↓

EC2

↓

SSH Response

↓

Automatically Allowed

---

# Security Group Architecture

```
                Internet
                     │
              Security Group
                     │
            ------------------
            |                |
         EC2 Instance     EC2 Instance
```

One Security Group can be attached to multiple EC2 instances.

Similarly, one EC2 instance can have multiple Security Groups attached.

---

# Security Group vs Network ACL

| Security Group | Network ACL |
|----------------|-------------|
| Instance Level | Subnet Level |
| Stateful | Stateless |
| Supports Allow Rules Only | Supports Allow and Deny Rules |
| Evaluates All Rules | Rules Evaluated by Number |
| Default Outbound Allowed | Configurable |

---

# Practical Overview

During our hands-on practice, we performed:

✔ Created a Security Group

✔ Allowed SSH (Port 22)

✔ Allowed HTTP (Port 80)

✔ Allowed HTTPS (Port 443)

✔ Attached the Security Group to an EC2 Instance

✔ Verified Website Access

✔ Modified Security Group Rules

✔ Removed Unnecessary Rules

✔ Tested Connectivity

---

# AWS CLI Commands

## Create Security Group

```bash
aws ec2 create-security-group \
--group-name WebServer-SG \
--description "Security Group for Web Server"
```

---

## View Security Groups

```bash
aws ec2 describe-security-groups
```

---

## Allow SSH

```bash
aws ec2 authorize-security-group-ingress \
--group-id sg-xxxxxxxx \
--protocol tcp \
--port 22 \
--cidr YOUR_IP/32
```

---

## Allow HTTP

```bash
aws ec2 authorize-security-group-ingress \
--group-id sg-xxxxxxxx \
--protocol tcp \
--port 80 \
--cidr 0.0.0.0/0
```

---

## Allow HTTPS

```bash
aws ec2 authorize-security-group-ingress \
--group-id sg-xxxxxxxx \
--protocol tcp \
--port 443 \
--cidr 0.0.0.0/0
```

---

# Best Practices

- Allow only required ports.
- Restrict SSH access to trusted IP addresses.
- Use the Principle of Least Privilege.
- Remove unused rules regularly.
- Separate Security Groups for Web, Application, and Database servers.
- Use descriptive names and tags.
- Review Security Group rules periodically.

---

# Common Mistakes

- Allowing SSH from `0.0.0.0/0`.
- Opening unnecessary ports.
- Using one Security Group for all servers.
- Forgetting to remove temporary access rules.
- Assuming Security Groups can deny traffic (they cannot).

---

# Quick Revision

| Component | Purpose |
|-----------|---------|
| Security Group | Virtual Firewall |
| Inbound Rule | Controls Incoming Traffic |
| Outbound Rule | Controls Outgoing Traffic |
| Port | Communication Endpoint |
| Protocol | Communication Method |
| CIDR | IP Range |
| Stateful | Return Traffic Automatically Allowed |

---

# Important Interview Points

- Security Groups are **Stateful**.
- Security Groups operate at the **Instance Level**.
- They support **Allow Rules Only**.
- One Security Group can be attached to multiple EC2 instances.
- One EC2 instance can have multiple Security Groups.
- SSH uses Port **22**.
- HTTP uses Port **80**.
- HTTPS uses Port **443**.
- Security Groups are associated with the EC2 instance's **Elastic Network Interface (ENI)**.
- Restrict SSH access using your public IP instead of allowing `0.0.0.0/0`.
