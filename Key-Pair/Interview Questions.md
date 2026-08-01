# AWS Key Pair - Interview Questions

This document contains frequently asked AWS Key Pair interview questions, including basic concepts, SSH authentication, production scenarios, troubleshooting, and rapid-fire questions.

---

# Basic Interview Questions

## Q1. What is an AWS Key Pair?

### Answer

An AWS Key Pair is a combination of a **Public Key** and a **Private Key** used to securely authenticate users when connecting to an EC2 instance.

AWS stores the Public Key, while the user downloads and securely stores the Private Key.

---

## Q2. Why do we need a Key Pair?

### Answer

A Key Pair provides secure authentication for EC2 instances.

Instead of using passwords, AWS uses SSH Key Pair authentication to allow secure remote access.

---

## Q3. What are the components of a Key Pair?

### Answer

A Key Pair consists of:

- Public Key
- Private Key

The Public Key is stored on the EC2 instance, while the Private Key is kept by the user.

---

## Q4. Where is the Public Key stored?

### Answer

The Public Key is stored on the EC2 instance (inside the user's `~/.ssh/authorized_keys` file) and is managed during instance launch.

---

## Q5. Where is the Private Key stored?

### Answer

The Private Key is downloaded by the user during key pair creation and must be stored securely.

AWS does not store the private key for later download.

---

## Q6. Can AWS recover a lost Private Key?

### Answer

No.

AWS cannot recover or regenerate a lost Private Key.

A new Key Pair must be created and configured.

---

## Q7. What is the difference between Public Key and Private Key?

| Public Key | Private Key |
|------------|-------------|
| Stored on EC2 | Stored by User |
| Used for Verification | Used for Authentication |
| Can be Shared | Must be Kept Secret |

---

## Q8. What is SSH?

### Answer

SSH (Secure Shell) is a secure network protocol used to remotely connect to Linux servers.

Default SSH Port:

```
22
```

---

## Q9. Which protocol is used to connect to a Linux EC2 instance?

### Answer

SSH (Secure Shell)

---

## Q10. Which port is used by SSH?

### Answer

Port **22**

---

# Authentication Questions

## Q11. How does Key Pair authentication work?

### Answer

1. User initiates an SSH connection using the Private Key.
2. EC2 verifies the Private Key against the stored Public Key.
3. If they match, access is granted.
4. Otherwise, the connection is rejected.

---

## Q12. Why is password authentication not recommended?

### Answer

Password authentication is more vulnerable to brute-force attacks.

SSH Key Pair authentication is more secure because it uses cryptographic keys instead of passwords.

---

## Q13. Why is the Private Key important?

### Answer

The Private Key proves the identity of the user attempting to connect.

Without it, SSH authentication fails.

---

## Q14. Can the same Key Pair be used for multiple EC2 instances?

### Answer

Yes.

A single Key Pair can be used for multiple EC2 instances.

However, using separate Key Pairs for different environments is considered a best practice.

---

## Q15. What happens if the wrong Private Key is used?

### Answer

SSH authentication fails.

The user receives a "Permission denied (publickey)" error.

---

# Linux Questions

## Q16. Why do we run `chmod 400 my-key.pem`?

### Answer

It restricts access to the Private Key file.

SSH refuses to use a key file that is accessible by other users.

---

## Q17. What does `chmod 400` mean?

### Answer

- Owner → Read
- Group → No Permission
- Others → No Permission

---

## Q18. What command is used to connect to an EC2 instance?

### Answer

```bash
ssh -i my-key.pem ubuntu@<Public-IP>
```

---

## Q19. What is a PEM file?

### Answer

A PEM file is a Private Key format commonly used with OpenSSH on Linux and macOS.

---

## Q20. What is a PPK file?

### Answer

A PPK (PuTTY Private Key) file is used by PuTTY on Windows for SSH authentication.

---

# AWS Practical Questions

## Q21. How do you create a Key Pair?

### Answer

1. Open the EC2 Console.
2. Navigate to **Key Pairs**.
3. Click **Create Key Pair**.
4. Select RSA or ED25519.
5. Choose PEM or PPK.
6. Download the Private Key.

---

## Q22. What AWS CLI command creates a Key Pair?

### Answer

```bash
aws ec2 create-key-pair --key-name DevOps-Key
```

---

## Q23. How do you list existing Key Pairs?

### Answer

```bash
aws ec2 describe-key-pairs
```

---

## Q24. How do you delete a Key Pair?

### Answer

```bash
aws ec2 delete-key-pair --key-name DevOps-Key
```

---

## Q25. Does deleting a Key Pair from AWS delete the Private Key from your computer?

### Answer

No.

Deleting the Key Pair from AWS only removes the Public Key association.

Your local Private Key file remains unchanged.

---

# Production Scenario Questions

## Q26. A developer lost the Private Key. What will you do?

### Answer

AWS cannot recover the Private Key.

Create a new Key Pair and update the EC2 instance by adding the new Public Key (or use an alternative recovery method such as AWS Systems Manager if available).

---

## Q27. You are getting "Permission denied (publickey)". What will you check?

### Answer

- Correct Private Key?
- Correct SSH username?
- File permission (`chmod 400`)?
- Correct Public IP or Elastic IP?
- Security Group allows SSH (Port 22)?
- EC2 instance is running?

---

## Q28. SSH connection is timing out. What could be the reason?

### Answer

- Security Group blocks Port 22.
- Network ACL blocks traffic.
- Instance has no Public/Elastic IP.
- Internet Gateway or Route Table issue.
- SSH service is not running.

---

## Q29. Why should different environments use different Key Pairs?

### Answer

Using separate Key Pairs for Development, Testing, and Production improves security and simplifies access management.

---

## Q30. Why should Private Keys never be stored in GitHub?

### Answer

Anyone with access to the Private Key can potentially access your EC2 instances.

Private Keys should never be committed to version control.

---

# Rapid Fire Questions & Answers

### Q31. What is a Key Pair?

**Answer:** A Public Key and Private Key used for EC2 authentication.

---

### Q32. Which key is stored by AWS?

**Answer:** Public Key.

---

### Q33. Which key is downloaded by the user?

**Answer:** Private Key.

---

### Q34. Can AWS recover a lost Private Key?

**Answer:** No.

---

### Q35. Which port does SSH use?

**Answer:** 22.

---

### Q36. Which command secures a PEM file?

**Answer:**

```bash
chmod 400 my-key.pem
```

---

### Q37. Which file format is used on Linux?

**Answer:** PEM.

---

### Q38. Which file format is used with PuTTY?

**Answer:** PPK.

---

### Q39. Can one Key Pair be used for multiple EC2 instances?

**Answer:** Yes.

---

### Q40. Is a Key Pair required for Linux EC2 instances?

**Answer:** Yes, unless you use an alternative access method such as AWS Systems Manager Session Manager.

---

# Interview Tips

- Explain the difference between the Public Key and the Private Key.
- Mention that AWS never stores or reissues the Private Key.
- Remember that SSH uses Port **22**.
- Explain why `chmod 400` is required before connecting.
- Never recommend sharing or storing Private Keys in Git repositories.
- Mention best practices such as using separate Key Pairs for different environments and rotating them periodically.
