# 🌐 Common Network Ports for DevOps Engineers

## Introduction

A **Port** is a logical communication endpoint that allows applications and services to communicate over a network.

Whenever a client communicates with a server, two things are required:

- **IP Address** → Identifies the device.
- **Port Number** → Identifies the application or service running on that device.

### Example

```
https://github.com

↓

IP Address : 140.82.xxx.xxx

↓

Port : 443 (HTTPS)
```

Without ports, the operating system would not know which application should receive incoming network traffic.

---

# Why are Ports Required?

Imagine a server running multiple services:

- Website
- Database
- SSH
- Jenkins
- Docker

All these services use the same IP address.

Ports help the operating system identify which service should receive the incoming request.

Think of it like:

```
IP Address  → Apartment Building

Port Number → Apartment Number
```

---

# Port Number Ranges

Ports are divided into three categories.

| Port Range | Category | Description |
|------------|----------|-------------|
| 0 – 1023 | Well-Known Ports | Reserved for standard services like SSH, HTTP, HTTPS, FTP, DNS, SMTP |
| 1024 – 49151 | Registered Ports | Used by applications such as MySQL, PostgreSQL, Docker, Jenkins, Redis |
| 49152 – 65535 | Dynamic / Private Ports | Temporary client-side ports automatically assigned by the operating system |

---

# Are Port Numbers Fixed?

The answer is **Yes and No**.

Some services use **well-known (default) ports** assigned by IANA, while many applications allow administrators to change their default ports.

Examples:

| Service | Default Port | Can be Changed? |
|----------|-------------:|:---------------:|
| SSH | 22 | ✅ Yes |
| HTTP | 80 | ✅ Yes |
| HTTPS | 443 | ✅ Yes |
| MySQL | 3306 | ✅ Yes |
| PostgreSQL | 5432 | ✅ Yes |
| Jenkins | 8080 | ✅ Yes |
| Redis | 6379 | ✅ Yes |
| MongoDB | 27017 | ✅ Yes |

> Although ports can be changed, most organizations use the default ports unless there is a security or business requirement.

---

# Common Network Ports

| Port | Protocol | Service | Purpose |
|------|----------|---------|---------|
| 20/21 | TCP | FTP | File Transfer |
| 22 | TCP | SSH | Secure Remote Login |
| 23 | TCP | Telnet | Remote Login (Insecure) |
| 25 | TCP | SMTP | Send Emails |
| 53 | TCP/UDP | DNS | Domain Name Resolution |
| 67/68 | UDP | DHCP | Automatic IP Assignment |
| 69 | UDP | TFTP | Lightweight File Transfer |
| 80 | TCP | HTTP | Web Traffic |
| 110 | TCP | POP3 | Receive Emails |
| 123 | UDP | NTP | Time Synchronization |
| 143 | TCP | IMAP | Receive Emails |
| 161/162 | UDP | SNMP | Network Monitoring |
| 389 | TCP/UDP | LDAP | Directory Services |
| 443 | TCP | HTTPS | Secure Web Traffic |
| 445 | TCP | SMB | Windows File Sharing |
| 465 | TCP | SMTPS | Secure Email Sending |
| 514 | UDP | Syslog | Log Collection |
| 587 | TCP | SMTP Submission | Secure Email Sending |
| 636 | TCP | LDAPS | Secure LDAP |
| 993 | TCP | IMAPS | Secure IMAP |
| 995 | TCP | POP3S | Secure POP3 |
| 1433 | TCP | Microsoft SQL Server | Database |
| 1521 | TCP | Oracle Database | Database |
| 2049 | TCP | NFS | Network File System |
| 2375 | TCP | Docker API | Docker (Non-TLS) |
| 2376 | TCP | Docker API | Docker (TLS) |
| 3306 | TCP | MySQL | Database |
| 3389 | TCP | RDP | Windows Remote Desktop |
| 5432 | TCP | PostgreSQL | Database |
| 5601 | TCP | Kibana | Log Visualization |
| 5672 | TCP | RabbitMQ | Message Broker |
| 6379 | TCP | Redis | In-Memory Database |
| 6443 | TCP | Kubernetes API Server | Kubernetes Control Plane |
| 8080 | TCP | Jenkins / Tomcat | CI/CD & Java Applications |
| 8081 | TCP | Nexus Repository | Artifact Repository |
| 8443 | TCP | Kubernetes Dashboard | Secure Web Interface |
| 9000 | TCP | SonarQube | Code Quality |
| 9090 | TCP | Prometheus | Monitoring |
| 9092 | TCP | Apache Kafka | Event Streaming |
| 9200 | TCP | Elasticsearch | Search & Logging |
| 9418 | TCP | Git | Git Protocol |
| 10250 | TCP | Kubelet | Kubernetes Node Communication |
| 27017 | TCP | MongoDB | NoSQL Database |
| 50000 | TCP | Jenkins Agent | Jenkins Agent Communication |

---

# Most Important Ports for DevOps Interviews

| Port | Service |
|------|---------|
| 22 | SSH |
| 53 | DNS |
| 80 | HTTP |
| 443 | HTTPS |
| 3306 | MySQL |
| 3389 | RDP |
| 5432 | PostgreSQL |
| 6379 | Redis |
| 6443 | Kubernetes API Server |
| 8080 | Jenkins / Tomcat |
| 8081 | Nexus Repository |
| 9000 | SonarQube |
| 9090 | Prometheus |
| 9092 | Apache Kafka |
| 9200 | Elasticsearch |
| 27017 | MongoDB |
| 50000 | Jenkins Agent |

---

# Quick Revision

- SSH → 22
- FTP → 20/21
- SMTP → 25
- DNS → 53
- HTTP → 80
- HTTPS → 443
- MySQL → 3306
- PostgreSQL → 5432
- Redis → 6379
- Kubernetes API Server → 6443
- Jenkins → 8080
- Nexus → 8081
- SonarQube → 9000
- Prometheus → 9090
- Kafka → 9092
- Elasticsearch → 9200
- MongoDB → 27017
- Jenkins Agent → 50000

---

# Interview Tips

- Learn the ports used by common DevOps tools.
- Understand the difference between **TCP** and **UDP**.
- Remember that many applications have **default ports**, but these can usually be changed.
- Know the three port ranges:
  - **0–1023** → Well-Known Ports
  - **1024–49151** → Registered Ports
  - **49152–65535** → Dynamic / Private Ports
- In AWS Security Groups and firewalls, ensure only the required ports are opened using the principle of least privilege.

---

## ⭐ Key Takeaways

- A **Port** identifies a specific application or service on a device.
- An **IP Address** identifies the device, while the **Port** identifies the service.
- Multiple services can run on the same server using different ports.
- Most applications have default ports, but they can usually be changed.
- Knowing common port numbers is essential for AWS, Linux, Kubernetes, Docker, and DevOps interviews.
