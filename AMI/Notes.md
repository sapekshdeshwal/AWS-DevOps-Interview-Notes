# Amazon Machine Image (AMI)

## What is an AMI?

Amazon Machine Image (AMI) is a pre-configured template used to launch EC2 instances in AWS.

It contains everything required to create an EC2 instance, including:

- Operating System
- Application Software
- Configuration Files
- Root Volume Snapshot
- Launch Permissions
- Block Device Mapping

Think of an AMI as a **blueprint** or **golden image** for launching identical EC2 instances.

---

# Why do we need AMI?

Without AMI:

- Install Operating System every time
- Install required software manually
- Configure applications repeatedly
- Time-consuming deployment
- Inconsistent server configuration

With AMI:

- Launch servers within minutes
- Standardized environment
- Faster deployment
- Easy Disaster Recovery
- Auto Scaling support
- Backup of configured servers

---

# Real World Example

Suppose a company has:

- Ubuntu Server
- Java 21 Installed
- Nginx Installed
- Application Code Deployed
- Monitoring Agent Installed

Instead of configuring everything again for every new server, the company creates an AMI.

Whenever a new server is required, AWS launches it using the AMI.

Result:

- Same OS
- Same Software
- Same Configuration
- Same Application

---

# Components of AMI

An AMI consists of:

## 1. Root Volume Snapshot

Contains:

- Operating System
- Installed Packages
- Application Files
- Configurations

---

## 2. Launch Permissions

Defines who can use the AMI.

Types:

- Private
- Public
- Shared

---

## 3. Block Device Mapping

Defines which storage volumes are attached when the instance is launched.

Example:

- Root Volume
- Additional EBS Volumes

---

# Types of AMI

## Public AMI

Created by:

- AWS
- Community
- Third-party Vendors

Example:

Ubuntu

Amazon Linux

Windows Server

---

## Private AMI

Created by your AWS Account.

Accessible only within your account unless shared.

Used in production environments.

---

## Shared AMI

A Private AMI shared with another AWS Account.

Useful for:

- Development Team
- QA Team
- Production Team

---

# AMI Architecture

```text
             Existing EC2 Instance
                      │
          Create Image (AMI)
                      │
          Root Volume Snapshot
                      │
               Amazon Machine Image
                      │
          Launch New EC2 Instance
```

---

# AMI Creation Process

Step 1

Launch an EC2 Instance

↓

Step 2

Install:

- Apache/Nginx
- Java
- Python
- Docker
- Monitoring Agent

↓

Step 3

Configure the Application

↓

Step 4

Create AMI

↓

Step 5

Launch Multiple EC2 Instances using the AMI

---

# AMI Lifecycle

```text
Launch EC2

↓

Configure Instance

↓

Create AMI

↓

Launch New Instance

↓

Copy AMI (Optional)

↓

Deregister AMI
```

---

# AMI vs Snapshot

| AMI | Snapshot |
|------|----------|
| Used to Launch EC2 | Backup of EBS Volume |
| Contains Snapshot + Metadata | Stores Volume Data |
| Used for Server Deployment | Used for Backup & Recovery |
| Includes Launch Configuration | Does not include Instance Configuration |

---

# Copy AMI

AWS allows copying an AMI:

- Between Regions
- Between AWS Accounts

Use Cases:

- Disaster Recovery
- Multi-Region Deployment
- Backup
- Migration

---

# Deregister AMI

When an AMI is no longer required:

- Deregister the AMI
- Delete associated snapshots if no longer needed

Note:

Deregistering an AMI **does not automatically delete** the snapshots associated with it.

---

# Practical Performed

✔ Launch EC2 Instance

✔ Install Required Software

✔ Configure Server

✔ Create AMI

✔ Launch New Instance using AMI

✔ Verify Configuration

✔ Copy AMI (Optional)

✔ Deregister AMI

---

# Best Practices

- Create AMI before major production changes.
- Remove temporary files before creating an AMI.
- Keep AMIs updated.
- Delete unused AMIs.
- Delete unused snapshots to reduce costs.
- Use meaningful naming conventions.
- Tag AMIs properly.

---

# Common Mistakes

- Creating outdated AMIs.
- Forgetting to remove temporary files.
- Leaving sensitive data inside AMI.
- Not deleting old snapshots.
- Confusing AMI with Snapshot.
- Creating duplicate AMIs.

---

# AWS CLI Commands

Create AMI

```bash
aws ec2 create-image \
--instance-id i-1234567890abcdef0 \
--name "WebServer-AMI"
```

List AMIs

```bash
aws ec2 describe-images --owners self
```

Copy AMI

```bash
aws ec2 copy-image
```

Deregister AMI

```bash
aws ec2 deregister-image \
--image-id ami-xxxxxxxx
```

---

# Hands-on Practice

✔ Launch EC2 Instance

✔ Configure Web Server

✔ Create Custom AMI

✔ Launch New EC2 from AMI

✔ Verify Same Configuration

✔ Copy AMI

✔ Deregister AMI

---

# Quick Revision

| Component | Purpose |
|------------|---------|
| AMI | Template to Launch EC2 |
| Snapshot | Backup of EBS Volume |
| Public AMI | Available to Everyone |
| Private AMI | Available to Owner |
| Shared AMI | Shared with Specific AWS Accounts |
| Copy AMI | Duplicate AMI Across Regions/Accounts |
| Deregister | Remove AMI Registration |

---

# Important Interview Points

- AMI is used to launch EC2 Instances.
- Every AMI contains a Root Volume Snapshot.
- AMI includes Launch Permissions and Block Device Mapping.
- Multiple EC2 Instances can be launched from a single AMI.
- Deregistering an AMI does not delete its snapshots.
- AMIs can be copied across Regions.
- AMIs help in Disaster Recovery and Auto Scaling.
- AMI provides a standardized server configuration.
