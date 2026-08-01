# Amazon Machine Image (AMI) Interview Questions

This document contains frequently asked Amazon Machine Image (AMI) interview questions for AWS and DevOps interviews.

---

# Q1. What is an AMI?

### Answer

Amazon Machine Image (AMI) is a pre-configured template used to launch EC2 instances.

It contains:

- Operating System
- Application Software
- Configuration Files
- Root Volume Snapshot
- Launch Permissions
- Block Device Mapping

---

# Q2. Why do we use AMI?

### Answer

AMI helps create identical EC2 instances quickly.

Benefits:

- Faster deployment
- Standardized environment
- Easy Backup
- Disaster Recovery
- Auto Scaling
- Infrastructure Automation

---

# Q3. What are the components of an AMI?

### Answer

An AMI consists of:

- Root Volume Snapshot
- Launch Permissions
- Block Device Mapping

---

# Q4. What are the different types of AMIs?

### Answer

- Public AMI
- Private AMI
- Shared AMI

---

# Q5. What is the difference between Public and Private AMI?

| Public AMI | Private AMI |
|------------|-------------|
| Available to everyone | Available only to owner |
| Created by AWS or Community | Created by Customer |
| Used for general purposes | Used in Production |

---

# Q6. What is a Shared AMI?

### Answer

A Shared AMI is a Private AMI that has been shared with specific AWS accounts.

It is commonly used to share standard server images across Development, Testing, and Production accounts.

---

# Q7. What is the difference between AMI and Snapshot?

| AMI | Snapshot |
|------|----------|
| Used to launch EC2 | Backup of EBS Volume |
| Contains metadata | Contains only volume data |
| Includes launch configuration | Does not include instance configuration |

---

# Q8. Can multiple EC2 instances be launched using the same AMI?

### Answer

Yes.

One AMI can be used to launch any number of EC2 instances.

---

# Q9. What happens when you create an AMI?

### Answer

AWS creates:

- Root Volume Snapshot
- AMI Metadata
- Launch Configuration

The original EC2 instance remains unchanged.

---

# Q10. Does creating an AMI stop the EC2 instance?

### Answer

By default, AWS briefly reboots the instance to ensure filesystem consistency.

However, you can choose **No Reboot** while creating an AMI.

No Reboot provides faster image creation but may result in inconsistent data if applications are actively writing to disk.

---

# Q11. Can an AMI be copied to another AWS Region?

### Answer

Yes.

AWS allows copying an AMI between Regions.

Common use cases:

- Disaster Recovery
- Multi-Region Deployments
- Backup
- Migration

---

# Q12. Can an AMI be shared with another AWS Account?

### Answer

Yes.

Private AMIs can be shared with specific AWS accounts by modifying launch permissions.

---

# Q13. What happens if you deregister an AMI?

### Answer

The AMI is removed from the account.

However, the associated EBS snapshots are **not deleted automatically**.

They continue to incur storage charges until deleted.

---

# Q14. What is Block Device Mapping?

### Answer

Block Device Mapping defines which storage devices are attached to an EC2 instance when it is launched from an AMI.

It includes:

- Root Volume
- Additional EBS Volumes (if configured)

---

# Q15. Can an AMI be modified after it is created?

### Answer

No.

An AMI is immutable.

If configuration changes are required:

- Launch a new EC2 instance.
- Make the required changes.
- Create a new AMI.

---

# Q16. Why are AMIs important in Auto Scaling?

### Answer

Auto Scaling launches new EC2 instances from an AMI.

This ensures every new instance has:

- Same Operating System
- Same Software
- Same Configuration
- Same Application Code

---

# Q17. What is a Golden AMI?

### Answer

A Golden AMI is a standardized and fully configured AMI used by an organization for launching production servers.

It usually includes:

- Security updates
- Monitoring agents
- Logging agents
- Required software
- Company standards

---

# Q18. What is the difference between AMI and Launch Template?

| AMI | Launch Template |
|------|-----------------|
| Contains Operating System Image | Contains complete launch configuration |
| Used to create EC2 | Uses an AMI to launch EC2 |
| Stores OS and software | Stores AMI ID, instance type, security groups, key pair, etc. |

---

# Scenario 1

Your production EC2 server is fully configured with Apache, Java, and your application.

Management wants to launch five identical servers.

What would you do?

### Answer

- Create an AMI from the configured EC2 instance.
- Launch five new EC2 instances using the AMI.

This ensures all servers have identical configurations.

---

# Scenario 2

A production server crashes completely.

How can you recover it quickly?

### Answer

If an AMI exists:

- Launch a new EC2 instance using the AMI.
- Attach any required data volumes.
- Associate the Elastic IP (if applicable).

This minimizes downtime.

---

# Scenario 3

A company wants to deploy the same application in another AWS Region.

What would you recommend?

### Answer

- Copy the AMI to the target Region.
- Launch new EC2 instances using the copied AMI.

---

# Scenario 4

A developer creates multiple AMIs every week but never deletes old ones.

What issue can this cause?

### Answer

- Increased EBS Snapshot storage costs.
- Management overhead.
- Confusion over which AMI is the latest.

Old AMIs and unused snapshots should be cleaned up regularly.

---

# Scenario 5

An Auto Scaling Group launches new EC2 instances, but they do not contain the latest application version.

What could be the reason?

### Answer

Possible causes:

- Auto Scaling Group is using an old AMI.
- A new AMI was created but the Launch Template was not updated.
- Launch Template version is outdated.

---

# Scenario 6

While creating an AMI, a developer selects **No Reboot**.

What is the risk?

### Answer

Applications writing data to disk may produce an inconsistent image.

For production workloads, allowing AWS to reboot the instance during AMI creation is generally safer.

---

# Production Interview Question

How are AMIs used in a Production Environment?

### Answer

Organizations create Golden AMIs containing:

- Operating System
- Security Patches
- Monitoring Agents
- Company Software
- Logging Configuration
- Application Dependencies

Whenever a new server is required, it is launched from the Golden AMI to ensure consistency across environments.

---

# Production Interview Question

Your company patches production servers every month.

How would you keep AMIs updated?

### Answer

1. Launch an EC2 instance from the latest AMI.
2. Apply operating system updates and security patches.
3. Update application dependencies if required.
4. Test the server.
5. Create a new AMI.
6. Update the Launch Template or Auto Scaling Group to use the new AMI.
7. Deregister outdated AMIs after validation.

---

# Troubleshooting Question

You launched a new EC2 instance from an AMI, but the application is not working.

How would you troubleshoot?

### Answer

Check:

- Was the application installed before creating the AMI?
- Were required services enabled?
- Are configuration files correct?
- Is the Security Group configured properly?
- Is the correct IAM Role attached?
- Review application logs.
- Verify startup scripts (User Data/Systemd).

---

# Frequently Asked Interview Points

- AMI is used to launch EC2 instances.
- Every AMI contains a Root Volume Snapshot.
- One AMI can launch multiple EC2 instances.
- AMIs are Region-specific but can be copied.
- Deregistering an AMI does not delete its snapshots.
- Auto Scaling Groups launch instances from AMIs.
- Golden AMIs are commonly used in production.
- Launch Templates reference an AMI.

---

# Quick Revision

✔ AMI = EC2 Template

✔ Snapshot = EBS Backup

✔ Public AMI = Available to Everyone

✔ Private AMI = Available to Owner

✔ Shared AMI = Shared with Specific Accounts

✔ Golden AMI = Standardized Production Image

✔ Copy AMI = Disaster Recovery & Multi-Region Deployment

✔ Deregister AMI = Removes Image (Snapshots remain)

✔ Auto Scaling = Launches EC2 from AMI
