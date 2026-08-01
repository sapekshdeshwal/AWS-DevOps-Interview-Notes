# AWS Key Pair

## What is a Key Pair?

An AWS Key Pair is a set of cryptographic keys used to securely authenticate and connect to an Amazon EC2 instance.

A Key Pair consists of:

- Public Key
- Private Key

AWS stores the **Public Key**, while you download and securely store the **Private Key**.

Instead of using passwords, AWS uses Key Pair authentication for secure access to Linux EC2 instances.

---

# Why Do We Need a Key Pair?

When launching an EC2 instance, AWS needs a secure way to verify the identity of the user trying to connect.

A Key Pair provides password-less and secure authentication.

Without a valid private key, users cannot access the EC2 instance using SSH.

---

# Real World Example

Suppose you launch a Linux EC2 instance for hosting a web application.

As a DevOps Engineer, you need to:

- Deploy the application
- Install packages
- Monitor logs
- Configure services

To perform these tasks, you first connect to the EC2 instance using SSH and the downloaded private key.

Example:

```bash
ssh -i my-key.pem ubuntu@<Public-IP>
```

Without the correct private key, SSH access will be denied.

---

# Components of a Key Pair

A Key Pair consists of two keys:

### Public Key

- Stored by AWS.
- Automatically placed inside the EC2 instance.
- Used to verify the connecting user.

### Private Key

- Downloaded only once during key pair creation.
- Stored securely by the user.
- Used to authenticate with the EC2 instance.

> **Important:** AWS never stores or allows you to download the private key again. If you lose it, you must create a new key pair and update the instance.

---

# Public Key vs Private Key

| Public Key | Private Key |
|------------|-------------|
| Stored by AWS | Stored by User |
| Can be shared | Must remain confidential |
| Used for verification | Used for authentication |
| Automatically installed on EC2 | Downloaded as `.pem` or converted to `.ppk` |

---

# How Key Pair Authentication Works

```
             DevOps Engineer

                    │

         Private Key (.pem)

                    │

                SSH Request

                    │

              EC2 Instance

                    │

      Public Key (Stored in EC2)

                    │

          Authentication Success
```

If the public key matches the private key, access is granted.

Otherwise, the connection is rejected.

---

# PEM vs PPK

| PEM | PPK |
|------|-----|
| Privacy Enhanced Mail | PuTTY Private Key |
| Used by Linux, macOS | Used by PuTTY on Windows |
| Supported by OpenSSH | Supported by PuTTY |

---

# Supported Authentication

### Linux EC2

Uses:

- SSH
- Key Pair

Example:

```bash
ssh -i my-key.pem ubuntu@<Public-IP>
```

---

### Windows EC2

Typically uses:

- RDP
- Administrator Password (generated using the private key)

---

# How to Create a Key Pair

1. Open AWS Management Console.
2. Navigate to **EC2 → Key Pairs**.
3. Click **Create Key Pair**.
4. Enter a key pair name.
5. Select:
   - RSA or ED25519
   - PEM or PPK
6. Click **Create Key Pair**.
7. Download the private key file and store it securely.

---

# Connect to an EC2 Instance

Linux Example:

```bash
ssh -i my-key.pem ubuntu@54.xxx.xxx.xxx
```

Amazon Linux:

```bash
ssh -i my-key.pem ec2-user@54.xxx.xxx.xxx
```

RHEL:

```bash
ssh -i my-key.pem ec2-user@54.xxx.xxx.xxx
```

CentOS:

```bash
ssh -i my-key.pem centos@54.xxx.xxx.xxx
```

Debian:

```bash
ssh -i my-key.pem admin@54.xxx.xxx.xxx
```

---

# Linux File Permission

Before connecting, the private key should have secure permissions.

Command:

```bash
chmod 400 my-key.pem
```

### Why?

SSH refuses to use a private key that is accessible by other users.

Permission **400** means:

- Owner → Read
- Group → No Permission
- Others → No Permission

---

# AWS CLI Commands

## Create Key Pair

```bash
aws ec2 create-key-pair \
--key-name DevOps-Key
```

---

## Describe Key Pairs

```bash
aws ec2 describe-key-pairs
```

---

## Delete Key Pair

```bash
aws ec2 delete-key-pair \
--key-name DevOps-Key
```

---

# Best Practices

- Store the private key securely.
- Never share the private key.
- Use separate key pairs for different environments.
- Rotate key pairs periodically.
- Remove unused key pairs.
- Restrict file permissions using `chmod 400`.
- Use IAM and AWS Systems Manager Session Manager where appropriate instead of relying solely on SSH.

---

# Common Mistakes

- Losing the private key.
- Uploading the private key to GitHub.
- Sharing the private key with others.
- Using incorrect SSH username.
- Forgetting to run `chmod 400`.
- Assuming AWS can provide the private key again.

---

# Quick Revision

| Component | Purpose |
|-----------|---------|
| Key Pair | Secure EC2 Authentication |
| Public Key | Stored by AWS |
| Private Key | Stored by User |
| PEM | Linux/macOS SSH Key |
| PPK | PuTTY SSH Key |
| SSH | Secure Remote Login |
| chmod 400 | Secure Private Key Permission |

---

# Important Interview Points

- A Key Pair consists of a Public Key and a Private Key.
- AWS stores the Public Key, while the user downloads and stores the Private Key.
- The Private Key can only be downloaded once during key pair creation.
- Linux EC2 instances use SSH with a Key Pair for authentication.
- The private key should have `400` file permissions before use.
- If the private key is lost, AWS cannot recover it; a new key pair must be created.
- Never upload or share your private key.
- Use different key pairs for development, testing, and production environments.
