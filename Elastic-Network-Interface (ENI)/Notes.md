# AWS Elastic Network Interface (ENI)

## What is an Elastic Network Interface (ENI)?

An **Elastic Network Interface (ENI)** is a virtual network card (Virtual Network Adapter) that enables communication between an EC2 instance and the network.

Every EC2 instance must have at least one ENI to communicate within a VPC or with the internet.

An ENI contains networking information such as:

- Private IP Address
- Public IP / Elastic IP (if associated)
- MAC Address
- Security Groups
- Subnet Information

---

# Why Do We Need an ENI?

An EC2 instance requires a network interface to:

- Communicate with other EC2 instances
- Access the Internet
- Connect to AWS Services
- Receive incoming traffic
- Send outgoing traffic

Without an ENI, an EC2 instance cannot communicate over the network.

---

# Real World Example

Suppose a company has two web servers.

```
Internet

     │

Load Balancer

     │

EC2 Instance

     │

Elastic Network Interface

     │

VPC Network
```

The ENI acts as the network adapter that allows the EC2 instance to send and receive network traffic.

---

# Components of an ENI

An Elastic Network Interface contains:

- Primary Private IPv4 Address
- Secondary Private IPv4 Addresses (Optional)
- Public IP (Optional)
- Elastic IP (Optional)
- MAC Address
- Security Groups
- Subnet
- VPC Information

---

# Types of ENI

## Primary ENI

- Automatically created when an EC2 instance is launched.
- Cannot be detached from the instance.
- Known as **eth0** inside Linux.

---

## Secondary ENI

- Created manually.
- Can be attached or detached.
- Can be moved between EC2 instances in the same Availability Zone.

---

# How ENI Works

```
                Internet

                     │

              Elastic IP

                     │

             Elastic Network Interface

                     │

               EC2 Instance
```

The ENI acts as the communication bridge between the EC2 instance and the network.

---

# ENI Features

- Virtual Network Card
- Supports Multiple Private IP Addresses
- Supports Elastic IP Association
- Supports Multiple Security Groups
- Can be Attached or Detached (Secondary ENI)
- Can be Reused
- Available within a Single Availability Zone

---

# Primary vs Secondary ENI

| Primary ENI | Secondary ENI |
|--------------|---------------|
| Created Automatically | Created Manually |
| Cannot be Detached | Can be Detached |
| Mandatory | Optional |
| One per EC2 Instance | Multiple Supported (Depends on Instance Type) |

---

# ENI vs Security Group

| ENI | Security Group |
|------|----------------|
| Virtual Network Card | Virtual Firewall |
| Provides Network Connectivity | Controls Network Traffic |
| Attached to EC2 | Attached to ENI |

---

# ENI vs Elastic IP

| ENI | Elastic IP |
|------|------------|
| Virtual Network Interface | Static Public IPv4 Address |
| Handles Network Communication | Provides Public Internet Access |
| Contains Private IP | Associated with ENI |

---

# Practical Overview

During hands-on practice, we performed:

✔ Created an EC2 Instance

✔ Viewed the Primary ENI

✔ Checked Private IP Address

✔ Checked MAC Address

✔ Verified Attached Security Groups

✔ Allocated an Elastic IP

✔ Associated the Elastic IP with the ENI

✔ Created a Secondary ENI

✔ Attached the Secondary ENI to an EC2 Instance

✔ Detached the Secondary ENI

✔ Reattached the Secondary ENI to another EC2 Instance

---

# AWS CLI Commands

## Describe ENIs

```bash
aws ec2 describe-network-interfaces
```

---

## Create an ENI

```bash
aws ec2 create-network-interface \
--subnet-id subnet-xxxxxxxx \
--groups sg-xxxxxxxx
```

---

## Attach an ENI

```bash
aws ec2 attach-network-interface \
--network-interface-id eni-xxxxxxxx \
--instance-id i-xxxxxxxx \
--device-index 1
```

---

## Detach an ENI

```bash
aws ec2 detach-network-interface \
--attachment-id eni-attach-xxxxxxxx
```

---

## Delete an ENI

```bash
aws ec2 delete-network-interface \
--network-interface-id eni-xxxxxxxx
```

---

# Advantages of ENI

- Supports Multiple IP Addresses
- Supports High Availability
- Easy Server Migration
- Multiple Security Groups
- Supports Elastic IP
- Better Network Flexibility

---

# Limitations

- A Secondary ENI can only be attached within the same Availability Zone.
- The number of ENIs depends on the EC2 instance type.
- Primary ENI cannot be detached.
- ENIs cannot be moved across Regions.

---

# Best Practices

- Use Secondary ENIs for high availability and failover.
- Attach only the required Security Groups.
- Remove unused ENIs.
- Use meaningful names and tags.
- Monitor ENI usage regularly.

---

# Common Mistakes

- Assuming the Primary ENI can be detached.
- Confusing ENI with Elastic IP.
- Creating unused ENIs.
- Attaching an ENI in a different Availability Zone.
- Forgetting to update Security Groups after attaching a new ENI.

---

# Quick Revision

| Component | Purpose |
|-----------|---------|
| ENI | Virtual Network Card |
| Primary ENI | Default Network Interface |
| Secondary ENI | Additional Network Interface |
| Private IP | Internal Communication |
| Elastic IP | Static Public IP |
| Security Group | Controls Traffic |
| MAC Address | Unique Hardware Address |

---

# Important Interview Points

- ENI stands for **Elastic Network Interface**.
- Every EC2 instance has at least one Primary ENI.
- The Primary ENI cannot be detached.
- Secondary ENIs can be attached and detached.
- An ENI can have multiple Private IP addresses.
- An Elastic IP is associated with an ENI, not directly with the EC2 instance.
- Security Groups are attached to the ENI.
- ENIs are Availability Zone specific.
- The maximum number of ENIs depends on the EC2 instance type.
