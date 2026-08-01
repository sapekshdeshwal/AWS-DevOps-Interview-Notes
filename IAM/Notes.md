# AWS Identity and Access Management (IAM)

## What is IAM?

AWS Identity and Access Management (IAM) is a Global AWS service that helps you securely manage access to AWS resources by controlling **who can access AWS services** and **what actions they can perform**.

IAM provides Authentication (Who you are) and Authorization (What you can do).

---

# Why IAM?

Without IAM:

- Everyone would use the Root User.
- No access control.
- High security risk.
- Difficult to track user activities.
- No Principle of Least Privilege.

With IAM:

- Individual user accounts.
- Controlled permissions.
- Secure access to AWS resources.
- Activity tracking using CloudTrail.
- Better compliance and security.

---

# Key Features

- Global AWS Service
- Identity Management
- Access Management
- Fine-Grained Permissions
- Multi-Factor Authentication (MFA)
- Temporary Credentials using IAM Roles
- Policy-Based Access Control
- Free AWS Service

---

# IAM Components

## Root User

- Created when AWS Account is created.
- Has Full Administrative Access.
- Cannot be restricted using IAM Policies.
- Should only be used for account-level tasks.
- Enable MFA immediately.

---

## IAM User

An IAM User represents a person or an application that requires access to AWS resources.

Examples:

- Developer
- DevOps Engineer
- QA Engineer
- Administrator

Each IAM User has its own:

- Username
- Password (Console Access)
- Access Keys (CLI/API)
- Permissions

---

## IAM Group

An IAM Group is a collection of IAM Users.

Purpose:

- Simplifies permission management.
- Permissions are assigned to the Group instead of individual users.

Example:

Developer Group

- Rahul
- Amit
- Priya

All users inherit the permissions assigned to the group.

---

## IAM Policy

IAM Policy is a JSON document that defines permissions.

It specifies:

- What action is allowed or denied.
- Which AWS resource can be accessed.
- Under what conditions access is granted.

Policy Elements:

- Version
- Statement
- Effect
- Action
- Resource
- Condition

---

## IAM Role

IAM Role is an AWS identity that provides **temporary credentials** to trusted entities.

Unlike IAM Users, Roles do not have:

- Username
- Password
- Permanent Access Keys

Common Use Cases:

- EC2 accessing S3
- Lambda accessing DynamoDB
- Cross-Account Access
- Temporary access for applications

---

# Authentication vs Authorization

## Authentication

Verifies the identity of a user.

Example:

Username + Password + MFA

Question:

**Who are you?**

---

## Authorization

Determines what an authenticated user is allowed to do.

Example:

Developer can Start EC2 but cannot Terminate EC2.

Question:

**What are you allowed to do?**

---

# IAM Architecture

```text
                 AWS Account
                      │
                Root User
                      │
        ┌─────────────┼─────────────┐
        │             │             │
    IAM Users     IAM Groups    IAM Roles
        │             │             │
        └─────────────┼─────────────┘
                      │
                IAM Policies
                      │
                AWS Resources
```

---

# Types of IAM Policies

### AWS Managed Policy

- Created by AWS.
- Maintained by AWS.
- Ready to use.

Example:

- AmazonS3FullAccess
- AmazonEC2FullAccess
- AdministratorAccess

---

### Customer Managed Policy

- Created by Customer.
- Fully customizable.
- Recommended for production.

---

### Inline Policy

- Attached directly to one User, Group or Role.
- Cannot be reused.
- Used for unique permission requirements.

---

# Principle of Least Privilege (PoLP)

Users should receive only the minimum permissions required to perform their job.

Example:

Developer

✅ Start EC2

✅ Stop EC2

❌ Terminate EC2

---

# Multi-Factor Authentication (MFA)

Provides an additional layer of security.

Supported MFA Devices:

- Google Authenticator
- Microsoft Authenticator
- Authy
- Hardware Security Keys

Recommended:

Enable MFA for:

- Root User
- Administrator Users

---

# Access Keys

Used for:

- AWS CLI
- SDK
- API Access

Consists of:

- Access Key ID
- Secret Access Key

Best Practices:

- Rotate regularly.
- Never hardcode in applications.
- Never upload to GitHub.
- Prefer IAM Roles whenever possible.

---

# IAM Best Practices

- Never use Root User for daily tasks.
- Enable MFA.
- Follow Least Privilege.
- Use IAM Groups.
- Use IAM Roles instead of Access Keys.
- Rotate Access Keys regularly.
- Remove unused users.
- Enable CloudTrail.
- Review IAM permissions periodically.

---

# Common Mistakes

- Using Root User daily.
- Giving AdministratorAccess to everyone.
- Hardcoding Access Keys.
- Not enabling MFA.
- Using wildcard (*) permissions.
- Creating unnecessary IAM Users.
- Ignoring permission reviews.

---

# AWS CLI Commands

List Users

```bash
aws iam list-users
```

Create User

```bash
aws iam create-user --user-name developer1
```

Delete User

```bash
aws iam delete-user --user-name developer1
```

List Groups

```bash
aws iam list-groups
```

List Roles

```bash
aws iam list-roles
```

List Policies

```bash
aws iam list-policies
```

Generate Credential Report

```bash
aws iam generate-credential-report
```

---

# Hands-on Performed

- Created IAM Users
- Created IAM Groups
- Attached Managed Policies
- Created Custom Policies
- Added Users to Groups
- Enabled MFA
- Generated Access Keys
- Created IAM Roles
- Attached IAM Role to EC2
- Tested IAM Permissions

---

# Quick Revision

| Component | Purpose |
|-----------|---------|
| Root User | Full AWS Account Access |
| IAM User | Individual Identity |
| IAM Group | Collection of Users |
| IAM Policy | Permission Document |
| IAM Role | Temporary AWS Credentials |
| MFA | Additional Security Layer |
| Access Keys | CLI/API Authentication |
| STS | Temporary Credentials |
| IAM | Global AWS Service |

---

# Important Interview Points

- IAM is a Global Service.
- Root User cannot be restricted using IAM Policies.
- IAM Roles provide Temporary Credentials.
- IAM Users have Permanent Credentials.
- Explicit Deny always overrides Allow.
- IAM follows the Principle of Least Privilege.
- IAM Policies are written in JSON.
- Prefer IAM Roles over Access Keys.
- Enable MFA for privileged accounts.
- Use Customer Managed Policies for production.
