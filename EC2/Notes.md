# Amazon Elastic Compute Cloud (EC2)

## What is Amazon EC2?

Amazon Elastic Compute Cloud (EC2) is a web service provided by AWS that allows users to launch, manage, and scale virtual servers (called **Instances**) in the cloud.

Instead of purchasing and maintaining physical servers, organizations can provision virtual machines within minutes and pay only for the resources they use.

EC2 is one of the core AWS services and is widely used to host applications, websites, APIs, databases, CI/CD tools, and container workloads.

---

# Why EC2?

Before Cloud Computing:

- Purchase physical servers
- High infrastructure cost
- Hardware maintenance
- Long provisioning time
- Difficult scaling

Using EC2:

- Launch servers within minutes
- Pay only for what you use
- Easy vertical and horizontal scaling
- High Availability
- Global infrastructure
- No hardware maintenance

---

# Real World Use Cases

Amazon EC2 is commonly used for:

- Hosting Web Applications
- Hosting Backend APIs
- Running Docker Containers
- Kubernetes Worker Nodes
- Jenkins Server
- GitLab Runner
- Database Server
- Bastion Host
- Monitoring Servers
- Testing & Development Environments

---

# EC2 Architecture

```text
                 User
                  │
              Internet
                  │
           Security Group
                  │
             EC2 Instance
          ┌────────┴────────┐
          │                 │
      EBS Volume       Network Interface
          │
      Operating System
          │
      Application
```

---

# EC2 Components

## 1. Amazon Machine Image (AMI)

An AMI is a template used to launch EC2 Instances.

It contains:

- Operating System
- Software Packages
- Configuration
- Root Volume Snapshot

---

## 2. Instance Type

Defines:

- CPU
- Memory (RAM)
- Storage
- Network Performance

Example:

- t2.micro
- t3.micro
- m5.large
- c5.large
- r5.large

---

## 3. Key Pair

Used for secure authentication while connecting to Linux EC2 instances through SSH.

Types:

- Public Key
- Private Key (.pem)

Never share your private key.

---

## 4. Security Group

Acts as a Virtual Firewall.

Controls:

- Inbound Traffic
- Outbound Traffic

Security Groups are Stateful.

---

## 5. Elastic Block Store (EBS)

Persistent Block Storage attached to EC2.

Used to store:

- Operating System
- Applications
- User Data

---

## 6. Elastic Network Interface (ENI)

A virtual network card attached to an EC2 instance.

Contains:

- Private IP
- Public IP (Optional)
- MAC Address
- Security Groups

---

## 7. Elastic IP

A static public IPv4 address.

Used when:

- Public IP should not change.
- Hosting production applications.

---

## 8. IAM Role

Provides temporary AWS credentials to an EC2 instance.

Recommended instead of Access Keys.

---

# EC2 Instance Lifecycle

```text
Pending
   │
Running
   │
Stopping
   │
Stopped
   │
Running
   │
Shutting Down
   │
Terminated
```

---

# EC2 Instance Families

## General Purpose

Example:

- T2
- T3
- M5

Use Cases:

- Web Applications
- Small Databases
- Development Servers

---

## Compute Optimized

Example:

- C5
- C6

Use Cases:

- Gaming
- Video Encoding
- High CPU Applications

---

## Memory Optimized

Example:

- R5
- X1

Use Cases:

- SAP
- Redis
- Large Databases

---

## Storage Optimized

Example:

- I3
- D2

Use Cases:

- Big Data
- NoSQL Databases

---

## Accelerated Computing

Example:

- P Series
- G Series

Use Cases:

- AI
- Machine Learning
- Graphics Rendering

---

# EC2 Pricing Models

## On-Demand

- Pay per use
- No commitment
- Best for testing

---

## Reserved Instance

- 1 or 3 Year commitment
- Lower price
- Predictable workloads

---

## Spot Instance

- Lowest cost
- AWS can terminate anytime
- Suitable for fault-tolerant applications

---

## Dedicated Host

- Physical server dedicated to one customer
- Compliance requirements

---

## Savings Plan

- Flexible pricing
- Cost optimization

---

# Stop vs Terminate

| Stop | Terminate |
|------|-----------|
| Can start again | Permanently deleted |
| Instance ID remains | Instance ID removed |
| Root EBS retained (default) | Root volume may be deleted |
| Public IP changes | Instance removed permanently |

---

# Reboot vs Stop

| Reboot | Stop |
|---------|------|
| Restarts OS | Powers off VM |
| Public IP remains | Public IP changes (unless Elastic IP is attached) |
| Faster | Takes longer |

---

# Public IP vs Elastic IP

| Public IP | Elastic IP |
|------------|------------|
| Dynamic | Static |
| Changes after Stop/Start | Does not change |
| Assigned automatically | Allocated manually |

---

# Best Practices

- Use IAM Roles instead of Access Keys.
- Restrict SSH (Port 22) to trusted IPs.
- Use Security Groups instead of opening all ports.
- Create AMIs before major changes.
- Enable detailed monitoring if required.
- Attach only required EBS volumes.
- Tag EC2 resources properly.
- Keep the operating system updated.

---

# Common Mistakes

- Using Root User for daily work.
- Opening SSH to 0.0.0.0/0.
- Storing AWS Access Keys inside EC2.
- Forgetting to create backups.
- Launching oversized instances.
- Not monitoring CPU and disk usage.

---

# AWS CLI Commands

Launch Instance

```bash
aws ec2 run-instances
```

List Instances

```bash
aws ec2 describe-instances
```

Start Instance

```bash
aws ec2 start-instances --instance-ids <instance-id>
```

Stop Instance

```bash
aws ec2 stop-instances --instance-ids <instance-id>
```

Reboot Instance

```bash
aws ec2 reboot-instances --instance-ids <instance-id>
```

Terminate Instance

```bash
aws ec2 terminate-instances --instance-ids <instance-id>
```

Describe Instance Status

```bash
aws ec2 describe-instance-status
```

---

# Hands-on Practice

✔ Launch an EC2 Instance

✔ Connect using SSH

✔ Create a Key Pair

✔ Configure Security Group

✔ Allocate Elastic IP

✔ Attach IAM Role

✔ Create AMI

✔ Attach EBS Volume

✔ Mount EBS Volume

✔ Unmount EBS Volume

✔ Attach ENI

---

# Quick Revision

| Service | Purpose |
|----------|---------|
| EC2 | Virtual Machine |
| AMI | Instance Template |
| EBS | Persistent Block Storage |
| Security Group | Stateful Firewall |
| Elastic IP | Static Public IP |
| ENI | Virtual Network Card |
| Key Pair | SSH Authentication |
| IAM Role | Temporary AWS Credentials |

---

# Important Interview Points

- EC2 is a Regional Service.
- An EC2 instance is launched in a single Availability Zone.
- Security Groups are Stateful.
- EC2 can have multiple EBS volumes attached.
- Elastic IP remains the same until released.
- Use IAM Roles instead of storing Access Keys.
- Create an AMI before making major production changes.
- Stop preserves the instance; Terminate permanently deletes it.
