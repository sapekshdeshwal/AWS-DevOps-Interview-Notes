# AWS IAM Interview Questions

This document contains frequently asked AWS IAM interview questions, including concept-based, scenario-based, troubleshooting, and real-world DevOps interview questions.

---

# Q1. What is AWS IAM?

### Answer

AWS Identity and Access Management (IAM) is a Global AWS service used to securely manage authentication and authorization for AWS resources.

It controls:

- Who can access AWS resources.
- What actions they can perform.
- Which AWS resources they can access.

---

# Q2. Is IAM a Global or Regional Service?

### Answer

IAM is a **Global Service**.

IAM Users, Groups, Roles, and Policies are available across all AWS Regions within an AWS account.

---

# Q3. What is the difference between Authentication and Authorization?

| Authentication | Authorization |
|---------------|--------------|
| Verifies identity | Determines permissions |
| Username & Password | IAM Policies |
| "Who are you?" | "What can you do?" |

---

# Q4. What is the Principle of Least Privilege?

### Answer

The Principle of Least Privilege (PoLP) means granting users only the minimum permissions required to perform their job.

Example:

A Developer should be able to Start and Stop EC2 instances but should not be allowed to Terminate them.

---

# Q5. What is the difference between Root User and IAM User?

| Root User | IAM User |
|-----------|----------|
| Created during AWS Account creation | Created manually |
| Full Account Access | Limited by IAM Policies |
| Cannot be restricted | Permissions can be managed |
| Used for Account Management | Used for Daily Operations |

---

# Q6. What is an IAM Group?

### Answer

An IAM Group is a collection of IAM Users.

Instead of assigning permissions individually, permissions are attached to the group.

---

# Q7. Can one IAM User belong to multiple Groups?

### Answer

Yes.

An IAM User can belong to multiple IAM Groups and inherits permissions from all associated groups.

---

# Q8. What is an IAM Policy?

### Answer

An IAM Policy is a JSON document that defines permissions for AWS resources.

A policy specifies:

- Effect
- Action
- Resource
- Condition

---

# Q9. What are the different types of IAM Policies?

### Answer

1. AWS Managed Policy
2. Customer Managed Policy
3. Inline Policy

---

# Q10. Which Policy type is recommended in Production?

### Answer

Customer Managed Policies.

Reasons:

- Reusable
- Easy to manage
- Fully customizable
- Centralized permission management

---

# Q11. What is an IAM Role?

### Answer

An IAM Role is an AWS identity that provides temporary security credentials to trusted entities.

Unlike IAM Users, Roles do not have:

- Username
- Password
- Permanent Access Keys

---

# Q12. Why are IAM Roles preferred over Access Keys?

### Answer

IAM Roles provide temporary credentials that automatically expire.

Advantages:

- Better Security
- Automatic Credential Rotation
- No Hardcoded Keys
- Lower Risk

---

# Q13. What is AWS STS?

### Answer

AWS Security Token Service (STS) generates temporary security credentials for IAM Roles.

---

# Q14. What is MFA?

### Answer

Multi-Factor Authentication (MFA) provides an additional layer of security by requiring a second authentication factor.

---

# Q15. Why should MFA be enabled?

### Answer

To protect AWS accounts from unauthorized access, especially privileged accounts such as the Root User and Administrators.

---

# Q16. What are Access Keys?

### Answer

Access Keys are credentials used for:

- AWS CLI
- SDK
- API Access

Each Access Key consists of:

- Access Key ID
- Secret Access Key

---

# Q17. Why should Access Keys never be hardcoded?

### Answer

Hardcoded credentials can be exposed through source code, Git repositories, or logs, leading to unauthorized access.

Use IAM Roles whenever possible.

---

# Q18. What is Explicit Deny?

### Answer

An Explicit Deny always overrides an Allow statement in IAM Policy evaluation.

---

# Q19. What is Implicit Deny?

### Answer

By default, all AWS requests are denied unless explicitly allowed through an IAM Policy.

---

# Q20. What is an ARN?

### Answer

ARN (Amazon Resource Name) uniquely identifies an AWS resource.

Example:

```
arn:aws:s3:::company-backup
```

---

# Scenario 1

## A developer needs to upload files to an S3 bucket from an EC2 instance.

The developer suggests storing AWS Access Keys inside the application.

What would you recommend?

### Answer

- Do not store Access Keys.
- Create an IAM Role.
- Attach the Role to the EC2 Instance.
- Grant only the required S3 permissions.
- Use temporary credentials provided by STS.

---

# Scenario 2

An employee accidentally receives AdministratorAccess.

What will you do?

### Answer

- Remove AdministratorAccess.
- Apply the Principle of Least Privilege.
- Create a Customer Managed Policy with only required permissions.
- Review access using IAM Access Analyzer.

---

# Scenario 3

A user reports "AccessDenied" while accessing an S3 bucket.

How will you troubleshoot?

### Answer

Check:

- IAM Policy
- Bucket Policy
- Explicit Deny
- Resource ARN
- Permission Boundary
- SCP (if AWS Organizations is used)

---

# Scenario 4

An EC2 instance cannot access an S3 bucket.

How will you troubleshoot?

### Answer

- Verify IAM Role is attached.
- Check IAM Role permissions.
- Verify Bucket Policy.
- Check Region.
- Verify Object ARN.
- Review CloudTrail logs.

---

# Scenario 5

A company has 500 employees.

Would you create 500 IAM Policies?

### Answer

No.

Create:

- IAM Groups
- Customer Managed Policies
- Assign Users to Groups

This simplifies permission management.

---

# Scenario 6

Your security audit finds IAM Users that haven't logged in for 180 days.

What will you do?

### Answer

- Review IAM Credential Report.
- Validate with the respective teams.
- Disable or remove inactive users.
- Delete unused Access Keys.

---

# Production Interview Question

Your company has:

- 200 Developers
- 50 QA Engineers
- 30 DevOps Engineers
- 10 Database Administrators

How would you design IAM?

### Answer

- Create separate IAM Groups.
- Assign Customer Managed Policies.
- Enable MFA.
- Use IAM Roles for AWS Services.
- Apply Least Privilege.
- Enable CloudTrail.
- Perform regular permission reviews.

---

# Frequently Asked Interview Points

- IAM is a Global Service.
- Root User should never be used for daily tasks.
- IAM Roles provide Temporary Credentials.
- IAM Policies are written in JSON.
- Explicit Deny overrides Allow.
- Enable MFA for privileged users.
- Prefer IAM Roles over Access Keys.
- Use Customer Managed Policies in production.
- Follow the Principle of Least Privilege.
- Enable CloudTrail for auditing.

---

# Quick Revision

✔ IAM = Identity & Access Management

✔ Authentication = Verify Identity

✔ Authorization = Verify Permissions

✔ IAM User = Permanent Identity

✔ IAM Role = Temporary Identity

✔ IAM Policy = Permission Document

✔ IAM Group = Collection of Users

✔ MFA = Additional Security

✔ STS = Temporary Credentials

✔ IAM = Global AWS Service
