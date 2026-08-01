# Amazon EC2 Interview Questions

This document contains frequently asked Amazon EC2 interview questions, including concept-based, production, troubleshooting, and scenario-based questions.

---

# Q1. What is Amazon EC2?

### Answer

Amazon Elastic Compute Cloud (EC2) is a web service provided by AWS that allows users to launch and manage virtual servers (instances) in the cloud.

It provides scalable computing capacity without purchasing physical servers.

---

# Q2. Is EC2 a Global or Regional Service?

### Answer

EC2 is a **Regional Service**.

When launching an instance, you must select:

- AWS Region
- Availability Zone

---

# Q3. What is an EC2 Instance?

### Answer

An EC2 Instance is a virtual machine running inside AWS.

It consists of:

- Operating System
- CPU
- RAM
- Storage
- Network Interface

---

# Q4. What is an AMI?

### Answer

AMI (Amazon Machine Image) is a template used to launch EC2 instances.

It contains:

- Operating System
- Software
- Configuration
- Root Volume Snapshot

---

# Q5. What is an Instance Type?

### Answer

Instance Type defines the hardware configuration of an EC2 instance.

It determines:

- CPU
- RAM
- Storage
- Network Performance

Example:

- t2.micro
- t3.micro
- m5.large
- c5.large

---

# Q6. What are the different EC2 Instance Families?

### Answer

- General Purpose (T, M)
- Compute Optimized (C)
- Memory Optimized (R, X)
- Storage Optimized (I, D)
- Accelerated Computing (P, G)

---

# Q7. What is the difference between Stop and Terminate?

| Stop | Terminate |
|------|-----------|
| Instance can be restarted | Instance is permanently deleted |
| Instance ID remains | Instance ID is deleted |
| Root EBS usually remains | Root EBS may be deleted |
| Public IP changes | Instance is removed permanently |

---

# Q8. What happens when you Stop an EC2 Instance?

### Answer

- Operating System shuts down.
- Compute resources are released.
- Root EBS volume remains.
- Public IP changes (unless Elastic IP is attached).
- Private IP remains the same.

---

# Q9. What is the difference between Reboot and Stop?

### Answer

Reboot

- Restarts the Operating System.
- Public IP remains the same.
- Faster operation.

Stop

- Powers off the Virtual Machine.
- Public IP changes.
- Can take longer.

---

# Q10. Can you change the Instance Type?

### Answer

Yes.

Steps:

- Stop the Instance.
- Change Instance Type.
- Start the Instance.

---

# Q11. What is the difference between Public IP and Elastic IP?

| Public IP | Elastic IP |
|------------|------------|
| Dynamic | Static |
| Changes after Stop/Start | Remains the same |
| Assigned automatically | Allocated manually |

---

# Q12. What is a Security Group?

### Answer

A Security Group is a virtual firewall that controls inbound and outbound traffic for an EC2 instance.

It is **Stateful**.

---

# Q13. What is a Key Pair?

### Answer

A Key Pair is used to securely connect to Linux EC2 instances using SSH.

It consists of:

- Public Key
- Private Key (.pem)

---

# Q14. What is an IAM Role?

### Answer

IAM Role provides temporary AWS credentials to an EC2 instance.

It eliminates the need to store Access Keys on the server.

---

# Q15. Why should IAM Roles be used instead of Access Keys?

### Answer

IAM Roles:

- More Secure
- Temporary Credentials
- Automatically Rotated
- No Hardcoded Secrets

---

# Q16. Can multiple EBS Volumes be attached to one EC2 Instance?

### Answer

Yes.

Multiple EBS volumes can be attached to a single EC2 instance depending on the instance type and AWS limits.

---

# Q17. Can one EBS Volume be attached to multiple EC2 Instances?

### Answer

Normally **No**.

However, **Multi-Attach** is supported only for specific **io1/io2** volumes and compatible instance types.

---

# Q18. What happens if an EC2 Instance is terminated?

### Answer

- Instance is permanently deleted.
- Instance ID cannot be reused.
- Root EBS volume may be deleted.
- Additional EBS volumes remain if Delete on Termination is disabled.

---

# Q19. Which Operating Systems are supported by EC2?

### Answer

- Amazon Linux
- Ubuntu
- Red Hat Enterprise Linux
- CentOS
- SUSE Linux
- Windows Server

---

# Q20. What are EC2 Pricing Models?

### Answer

- On-Demand
- Reserved Instance
- Spot Instance
- Dedicated Host
- Savings Plan

---

# Scenario 1

Your website is hosted on an EC2 instance.

Users report that the website is not opening.

How would you troubleshoot?

### Answer

Check:

- Is the EC2 instance running?
- Is the Security Group allowing HTTP/HTTPS?
- Is the web server (Apache/Nginx) running?
- Is the application listening on the correct port?
- Is the Route Table configured correctly?
- Is the Internet Gateway attached?
- Is the Network ACL blocking traffic?
- Check application logs.

---

# Scenario 2

You are unable to SSH into an EC2 instance.

How would you troubleshoot?

### Answer

Verify:

- EC2 instance is Running.
- Correct Public IP or Elastic IP.
- Security Group allows Port 22.
- Correct Key Pair is used.
- Correct SSH username (ubuntu, ec2-user, etc.).
- Route Table and Internet Gateway.
- Network ACL rules.
- SSH service is running.

---

# Scenario 3

CPU utilization suddenly becomes 100%.

What will you check?

### Answer

Check:

```bash
top
```

```bash
htop
```

```bash
ps -ef
```

Also review:

- CloudWatch Metrics
- Running processes
- Application logs
- Memory usage
- Disk utilization

---

# Scenario 4

Disk space is full on an EC2 instance.

How would you troubleshoot?

### Answer

Run:

```bash
df -h
```

```bash
lsblk
```

```bash
du -sh /*
```

Then:

- Identify large files.
- Clean unnecessary logs.
- Extend the EBS volume if required.
- Resize the filesystem after extending the volume.

---

# Scenario 5

A developer accidentally terminated a production EC2 instance.

How would you recover it?

### Answer

- The terminated instance cannot be restarted.
- Launch a new instance using an existing AMI.
- If an AMI is unavailable, restore data using EBS snapshots.
- Attach restored EBS volumes if needed.
- Reassign the Elastic IP if applicable.

---

# Scenario 6

Your application running on EC2 needs access to an S3 bucket.

How would you provide secure access?

### Answer

- Create an IAM Role.
- Grant only the required S3 permissions.
- Attach the IAM Role to the EC2 instance.
- Avoid using Access Keys.

---

# Scenario 7

A company wants to reduce EC2 costs for batch-processing jobs that can tolerate interruptions.

Which pricing model would you recommend?

### Answer

Use **Spot Instances** because they are significantly cheaper and suitable for interruptible workloads.

---

# Production Interview Question

How would you secure an EC2 instance in Production?

### Answer

- Use IAM Roles.
- Restrict SSH access.
- Enable Security Groups.
- Keep OS updated.
- Enable CloudWatch Monitoring.
- Take regular AMI and EBS Snapshots.
- Use least privilege.
- Enable logging and auditing.

---

# Frequently Asked Interview Points

- EC2 is a Regional Service.
- One EC2 instance belongs to one Availability Zone.
- Security Groups are Stateful.
- Public IP changes after Stop/Start.
- Elastic IP remains static.
- Root EBS may be deleted on termination.
- IAM Roles are preferred over Access Keys.
- Spot Instances are interruptible.
- Reserved Instances reduce long-term costs.

---

# Quick Revision

✔ EC2 = Virtual Machine

✔ AMI = Template

✔ EBS = Block Storage

✔ Security Group = Stateful Firewall

✔ Elastic IP = Static Public IP

✔ Key Pair = SSH Authentication

✔ ENI = Virtual Network Interface

✔ IAM Role = Temporary Credentials

✔ Spot = Lowest Cost

✔ Reserved = Long-Term Savings

✔ On-Demand = Pay As You Go
