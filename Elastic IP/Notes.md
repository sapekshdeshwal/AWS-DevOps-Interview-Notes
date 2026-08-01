# AWS Elastic IP (EIP)

## What is an Elastic IP?

An **Elastic IP (EIP)** is a **static public IPv4 address** provided by AWS that can be associated with an EC2 instance or an Elastic Network Interface (ENI).

Unlike a normal public IP, an Elastic IP remains the same until you release it, making it suitable for production workloads.

---

# Why do we need Elastic IP?

By default, AWS assigns a **public IP** to an EC2 instance.

If the instance is stopped and started again, the public IP changes.

This can cause issues for:

- Websites
- Applications
- DNS Records
- Clients
- External Integrations

Elastic IP solves this problem by providing a **permanent public IP address**.

---

# Real World Example

A company hosts its production website on an EC2 instance.

Customers access the website using:

```
www.company.com
```

If the EC2 instance is stopped and started, the default public IP changes.

Without Elastic IP:

- Website becomes inaccessible until DNS is updated.

With Elastic IP:

- Public IP remains the same.
- No DNS changes are required.
- Users continue accessing the website without interruption.

---

# Public IP vs Private IP vs Elastic IP

| Feature | Private IP | Public IP | Elastic IP |
|----------|------------|-----------|------------|
| Accessible from Internet | ❌ No | ✅ Yes | ✅ Yes |
| Changes after Stop/Start | ❌ No | ✅ Yes | ❌ No |
| Static | Yes | No | Yes |
| Used Inside VPC | Yes | No | No |
| Production Ready | Internal Communication | Temporary Access | External Production Access |

---

# How Elastic IP Works

```
                Internet
                     │
             Elastic IP Address
                     │
             EC2 Instance (ENI)
                     │
               Private IP Address
```

The Elastic IP is mapped to the instance's private IP through the Elastic Network Interface (ENI).

---

# Key Features

- Static Public IPv4 Address
- Region-Specific
- Can be Remapped to another EC2 Instance
- Associated with an EC2 Instance or ENI
- Suitable for Production Applications
- Supports High Availability Scenarios

---

# Elastic IP Lifecycle

```
Allocate Elastic IP

        ↓

Associate with EC2

        ↓

Use the Application

        ↓

Disassociate

        ↓

Associate with another EC2

        ↓

Release Elastic IP
```

---

# Allocate an Elastic IP

Allocating an Elastic IP reserves a static public IPv4 address in your AWS account.

After allocation, the IP is owned by your AWS account until it is released.

---

# Associate an Elastic IP

After allocation, the Elastic IP must be associated with:

- EC2 Instance
- Elastic Network Interface (ENI)

Only then can it be used to access the resource from the internet.

---

# Disassociate an Elastic IP

Disassociating removes the Elastic IP from the EC2 instance.

The Elastic IP remains allocated to your AWS account and can later be associated with another resource.

---

# Release an Elastic IP

Releasing an Elastic IP permanently returns it to AWS.

After release, the IP cannot be recovered.

---

# Elastic IP Remapping

One of the biggest advantages of Elastic IP is that it can be moved quickly between EC2 instances.

Example:

```
Old Server

↓

Elastic IP

↓

New Server
```

This helps reduce downtime during maintenance or server failures.

---

# Practical Overview

During hands-on practice, we performed:

✔ Allocated an Elastic IP

✔ Associated it with an EC2 Instance

✔ Connected to the instance using the Elastic IP

✔ Stopped and Started the EC2 Instance

✔ Verified that the Elastic IP remained unchanged

✔ Disassociated the Elastic IP

✔ Reassociated it with another EC2 Instance

✔ Released the Elastic IP

---

# AWS CLI Commands

## Allocate Elastic IP

```bash
aws ec2 allocate-address --domain vpc
```

---

## Associate Elastic IP

```bash
aws ec2 associate-address \
--allocation-id eipalloc-xxxxxxxx \
--instance-id i-xxxxxxxx
```

---

## View Elastic IPs

```bash
aws ec2 describe-addresses
```

---

## Disassociate Elastic IP

```bash
aws ec2 disassociate-address \
--association-id eipassoc-xxxxxxxx
```

---

## Release Elastic IP

```bash
aws ec2 release-address \
--allocation-id eipalloc-xxxxxxxx
```

---

# Advantages of Elastic IP

- Static Public IP
- Suitable for Production Applications
- Easy Server Migration
- Reduces Downtime
- No DNS Changes Required
- Easy Disaster Recovery

---

# Limitations

- Only IPv4 addresses are supported.
- Region-specific resource.
- AWS charges for unused Elastic IPs.
- Limited number of Elastic IPs per Region (can be increased through a quota request).

---

# Best Practices

- Use Elastic IP only when a static public IP is required.
- Release unused Elastic IPs to avoid unnecessary charges.
- Use DNS (Amazon Route 53) with Elastic IP for production applications.
- Document Elastic IP allocations properly.
- Regularly review allocated Elastic IPs.

---

# Common Mistakes

- Assuming a normal public IP is permanent.
- Forgetting to release unused Elastic IPs.
- Associating an Elastic IP with the wrong EC2 instance.
- Confusing Elastic IP with a Private IP.
- Not updating Security Groups after moving an Elastic IP.

---

# Quick Revision

| Component | Purpose |
|-----------|---------|
| Elastic IP | Static Public IPv4 Address |
| Allocate | Reserve an Elastic IP |
| Associate | Attach Elastic IP to EC2 or ENI |
| Disassociate | Remove Elastic IP from Resource |
| Release | Return Elastic IP to AWS |
| Region | Elastic IPs are Region-specific |

---

# Important Interview Points

- Elastic IP is a **static public IPv4 address**.
- Elastic IP is **Region-specific**.
- Public IP changes after an EC2 stop/start, but an Elastic IP does not.
- An Elastic IP can be associated with an **EC2 instance** or an **Elastic Network Interface (ENI)**.
- Elastic IPs help reduce downtime during server migration.
- AWS charges for unused Elastic IPs.
- Release unused Elastic IPs to avoid unnecessary costs.
