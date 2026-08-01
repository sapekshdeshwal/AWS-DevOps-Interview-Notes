# AWS Security Groups - Interview Questions

This document contains frequently asked AWS Security Group interview questions, including basic concepts, networking fundamentals, production scenarios, troubleshooting, and rapid-fire questions.

---

# Basic Interview Questions

## Q1. What is a Security Group?

### Answer

A Security Group is a **virtual firewall** that controls inbound and outbound traffic for AWS resources such as EC2 instances.

It allows traffic based on defined rules and helps secure AWS resources from unauthorized access.

---

## Q2. Why do we need Security Groups?

### Answer

Security Groups protect AWS resources by controlling which traffic is allowed to reach an EC2 instance.

For example:

- Allow SSH only from your office IP.
- Allow HTTP and HTTPS from the internet.
- Block unnecessary ports.

---

## Q3. At which level does a Security Group operate?

### Answer

Security Groups operate at the **Instance Level**.

They are attached to the **Elastic Network Interface (ENI)** of an EC2 instance.

---

## Q4. Is a Security Group Stateful or Stateless?

### Answer

Security Groups are **Stateful**.

If inbound traffic is allowed, the response traffic is automatically allowed.

No separate outbound rule is required for return traffic.

---

## Q5. What does Stateful mean?

### Answer

Stateful means AWS automatically allows return traffic for an established connection.

Example:

Laptop

↓

SSH Request (Port 22)

↓

EC2

↓

SSH Response

↓

Automatically Allowed

---

## Q6. Can a Security Group deny traffic?

### Answer

No.

Security Groups support **Allow Rules Only**.

To explicitly deny traffic, use a **Network ACL (NACL)**.

---

## Q7. Can one Security Group be attached to multiple EC2 instances?

### Answer

Yes.

A single Security Group can be associated with multiple EC2 instances.

---

## Q8. Can one EC2 instance have multiple Security Groups?

### Answer

Yes.

An EC2 instance can have multiple Security Groups attached.

The effective permissions are the combination of all allowed rules.

---

## Q9. What are Inbound Rules?

### Answer

Inbound Rules control incoming traffic to an EC2 instance.

Example:

- SSH (22)
- HTTP (80)
- HTTPS (443)

---

## Q10. What are Outbound Rules?

### Answer

Outbound Rules control traffic leaving the EC2 instance.

By default, all outbound traffic is allowed.

---

# Networking Questions

## Q11. What is a Port?

### Answer

A Port is a logical communication endpoint that allows applications and services to communicate over a network.

Example:

- SSH → 22
- HTTP → 80
- HTTPS → 443

---

## Q12. What is a Protocol?

### Answer

A Protocol defines how data is transmitted between devices over a network.

Common protocols include:

- TCP
- UDP
- ICMP

---

## Q13. What is the difference between TCP and UDP?

| TCP | UDP |
|------|-----|
| Connection Oriented | Connectionless |
| Reliable | Faster |
| Error Checking | No Error Recovery |

---

## Q14. What is CIDR?

### Answer

CIDR (Classless Inter-Domain Routing) represents a range of IP addresses.

Example:

```
0.0.0.0/0
```

Allows traffic from anywhere.

```
192.168.1.10/32
```

Allows only one specific IP address.

---

## Q15. What does 0.0.0.0/0 mean?

### Answer

It represents all IPv4 addresses.

Anyone on the internet can access the resource if the Security Group allows it.

---

## Q16. What does /32 mean?

### Answer

A `/32` CIDR represents a single IP address.

It is commonly used to allow SSH access only from your public IP.

---

# Security Group vs NACL

## Q17. Difference between Security Group and NACL?

| Security Group | NACL |
|----------------|------|
| Instance Level | Subnet Level |
| Stateful | Stateless |
| Allow Rules Only | Allow & Deny Rules |
| Evaluates All Rules | Rules Evaluated in Number Order |

---

## Q18. Which is more secure, Security Group or NACL?

### Answer

Both serve different purposes.

- Security Groups provide instance-level protection.
- NACLs provide subnet-level protection.

In production, both are commonly used together.

---

# AWS Practical Questions

## Q19. Which ports are commonly opened on a Web Server?

### Answer

- SSH → 22
- HTTP → 80
- HTTPS → 443

---

## Q20. Which port is used for SSH?

### Answer

Port **22**

---

## Q21. Which port is used for HTTP?

### Answer

Port **80**

---

## Q22. Which port is used for HTTPS?

### Answer

Port **443**

---

## Q23. Which port is used for MySQL?

### Answer

Port **3306**

---

## Q24. Which port is used for PostgreSQL?

### Answer

Port **5432**

---

## Q25. Why should SSH not be open to 0.0.0.0/0?

### Answer

Because anyone on the internet can attempt to connect to your server, increasing the risk of unauthorized access and brute-force attacks.

Restrict SSH access to trusted IP addresses whenever possible.

---

# Production Scenario Questions

## Q26. You cannot SSH into an EC2 instance. What will you check?

### Answer

- Is the EC2 instance running?
- Does it have a Public IP or Elastic IP?
- Does the Security Group allow TCP port 22 from your IP?
- Is the correct key pair being used?
- Is the Network ACL allowing the traffic?
- Is the SSH service running on the instance?

---

## Q27. Website is not opening on Port 80. What will you check?

### Answer

- Security Group allows HTTP (80)
- Web server (Apache/Nginx) is running
- Port 80 is listening
- NACL rules
- Route Table and Internet Gateway

---

## Q28. HTTPS is not working. What could be the reason?

### Answer

- Port 443 not allowed in Security Group
- SSL/TLS certificate issue
- Web server not configured for HTTPS
- Load Balancer listener missing

---

## Q29. Database connection is failing. What will you check?

### Answer

- Database service is running
- Security Group allows database port
- Application server IP is allowed
- NACL rules
- Database endpoint and credentials

---

## Q30. Why is your application accessible locally but not from the internet?

### Answer

Possible reasons:

- Security Group missing inbound rule
- NACL blocking traffic
- No Internet Gateway
- Route Table issue
- Application not listening on the expected port

---

# Troubleshooting Questions

## Q31. How do you verify whether a service is listening on a port?

### Answer

```bash
ss -tulnp
```

or

```bash
netstat -tulnp
```

---

## Q32. How do you verify HTTP connectivity from Linux?

### Answer

```bash
curl http://<server-ip>
```

---

## Q33. How do you verify network connectivity?

### Answer

```bash
ping <ip-address>
```

---

## Q34. How do you verify whether a specific port is reachable?

### Answer

```bash
nc -zv <server-ip> <port>
```

or

```bash
telnet <server-ip> <port>
```

---

# Rapid Fire Questions & Answers

### Q35. Are Security Groups Stateful?

**Answer:** Yes.

---

### Q36. Can Security Groups deny traffic?

**Answer:** No.

---

### Q37. Can multiple Security Groups be attached to one EC2?

**Answer:** Yes.

---

### Q38. Can one Security Group be attached to multiple EC2 instances?

**Answer:** Yes.

---

### Q39. What is the default outbound rule?

**Answer:** Allow all outbound traffic.

---

### Q40. What is the default SSH port?

**Answer:** 22

---

### Q41. What is the default HTTP port?

**Answer:** 80

---

### Q42. What is the default HTTPS port?

**Answer:** 443

---

### Q43. What is the default MySQL port?

**Answer:** 3306

---

### Q44. What is the default PostgreSQL port?

**Answer:** 5432

---

### Q45. Can Security Groups be attached to resources other than EC2?

**Answer:**

Yes. Security Groups can also be associated with resources such as:

- RDS
- Elastic Load Balancers (ALB/NLB where applicable)
- Amazon EFS Mount Targets
- Amazon ElastiCache
- Amazon Redshift
- Other VPC resources that support Security Groups

---

# Interview Tips

- Remember that **Security Groups are Stateful**.
- They support **Allow Rules Only**.
- They operate at the **Instance Level**.
- Always compare Security Groups with NACLs in interviews.
- Be comfortable troubleshooting connectivity issues by checking:
  - Security Group
  - NACL
  - Route Table
  - Internet Gateway
  - Service Status
  - Listening Port
- Never recommend opening SSH (22) to `0.0.0.0/0` in production unless absolutely necessary.
