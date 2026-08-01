# Amazon S3 Interview Questions

This document contains frequently asked Amazon S3 interview questions covering concepts, scenarios, troubleshooting, production use cases, and best practices.

---

# Q1. What is Amazon S3?

### Answer

Amazon Simple Storage Service (S3) is a fully managed Object Storage service provided by AWS. It is used to store and retrieve any amount of data from anywhere over the internet.

It stores data as **Objects** inside **Buckets**.

---

# Q2. Is Amazon S3 a Global or Regional Service?

### Answer

Amazon S3 is a **Regional Service**.

When you create a bucket, it is created in a specific AWS Region, although bucket names must be globally unique.

---

# Q3. What is Object Storage?

### Answer

Object Storage stores data as Objects.

Each Object contains:

- Object Data
- Metadata
- Object Key

Unlike Block Storage, Object Storage does not use partitions or file systems.

---

# Q4. What is a Bucket?

### Answer

A Bucket is a logical container used to store Objects in Amazon S3.

Bucket names must be globally unique.

---

# Q5. What is an Object?

### Answer

An Object is the actual file stored inside an S3 Bucket.

Examples:

- image.jpg
- backup.zip
- invoice.pdf

---

# Q6. What is an Object Key?

### Answer

The Object Key uniquely identifies an Object inside a Bucket.

Example:

```
images/profile.jpg
```

---

# Q7. What is Metadata?

### Answer

Metadata contains information about an Object.

Examples:

- File Size
- Last Modified
- Content Type
- Encryption Type

---

# Q8. What is the maximum Object size in S3?

### Answer

Maximum Object Size:

**5 TB**

For large files, AWS recommends using Multipart Upload.

---

# Q9. What are the different S3 Storage Classes?

### Answer

- Standard
- Standard-IA
- One Zone-IA
- Intelligent-Tiering
- Glacier Instant Retrieval
- Glacier Flexible Retrieval
- Glacier Deep Archive

---

# Q10. Which Storage Class is used for frequently accessed data?

### Answer

Amazon S3 Standard.

---

# Q11. What is Versioning?

### Answer

Versioning stores multiple versions of the same object.

Benefits:

- Recover deleted files
- Recover overwritten files
- Protection against accidental deletion

---

# Q12. What is a Lifecycle Rule?

### Answer

Lifecycle Rules automatically transition or delete objects based on defined rules.

Example:

30 Days → Standard-IA

90 Days → Glacier

365 Days → Delete

---

# Q13. What is Cross Region Replication (CRR)?

### Answer

CRR automatically copies objects from one S3 Bucket to another Bucket in a different AWS Region.

Requirements:

- Versioning enabled on both buckets.

---

# Q14. What is Bucket Policy?

### Answer

Bucket Policy is a Resource-Based Policy that controls access to an S3 Bucket.

---

# Q15. What is Block Public Access?

### Answer

Block Public Access prevents accidental public exposure of S3 Buckets.

It is recommended to keep it enabled unless public access is intentionally required.

---

# Q16. What encryption options are available in Amazon S3?

### Answer

- SSE-S3
- SSE-KMS
- SSE-C

---

# Q17. What is the difference between SSE-S3 and SSE-KMS?

### Answer

**SSE-S3**

- AWS manages encryption keys automatically.

**SSE-KMS**

- Uses AWS Key Management Service (KMS).
- Provides better control, auditing, and key rotation.

---

# Q18. What is Multipart Upload?

### Answer

Multipart Upload splits a large file into multiple smaller parts and uploads them in parallel.

Advantages:

- Faster upload
- Resume interrupted uploads
- Better performance

---

# Q19. What is the difference between S3 and EBS?

| Amazon S3 | Amazon EBS |
|------------|------------|
| Object Storage | Block Storage |
| Unlimited Storage | Fixed Volume Size |
| Access via Internet/API | Attached to EC2 |
| Stores Objects | Stores Blocks |

---

# Q20. Can multiple EC2 instances access the same S3 Bucket?

### Answer

Yes.

Multiple EC2 instances can access the same S3 Bucket if they have the required IAM permissions.

---

# Scenario 1

Your company stores application backups in Amazon S3.

Management wants to reduce storage costs because backups older than 90 days are rarely accessed.

What would you recommend?

### Answer

Configure an S3 Lifecycle Rule:

- Keep recent backups in Standard.
- Move older backups to Standard-IA or Glacier.
- Move long-term backups to Glacier Deep Archive.
- Delete data after the retention period if applicable.

---

# Scenario 2

An employee accidentally deletes an important file from S3.

How can you recover it?

### Answer

If Versioning is enabled:

- Retrieve the previous version of the object.

Without Versioning:

- Recovery is only possible if another backup exists.

---

# Scenario 3

A website hosted on Amazon S3 is returning "Access Denied".

How would you troubleshoot?

### Answer

Check:

- Bucket Policy
- Block Public Access settings
- Object permissions
- Static Website Hosting configuration
- Object exists in the bucket
- Correct object key (for example, `index.html`)

---

# Scenario 4

Your application running on EC2 cannot upload files to an S3 Bucket.

How would you troubleshoot?

### Answer

- Verify the EC2 IAM Role.
- Check IAM permissions.
- Verify the Bucket Policy.
- Confirm the correct bucket name.
- Verify object path.
- Review CloudTrail logs.
- Check for Explicit Deny.

---

# Scenario 5

A developer accidentally makes an S3 Bucket public.

How would you secure it?

### Answer

- Enable Block Public Access.
- Remove public Bucket Policy.
- Remove unnecessary ACLs.
- Review IAM permissions.
- Enable Access Analyzer.
- Monitor CloudTrail logs.

---

# Scenario 6

A company has customers worldwide and wants to reduce download latency.

Which AWS service would you recommend?

### Answer

Use **Amazon CloudFront** in front of the S3 Bucket.

CloudFront caches content at edge locations, reducing latency and improving performance.

---

# Scenario 7

Your company requires disaster recovery for critical documents stored in S3.

What solution would you implement?

### Answer

- Enable Versioning.
- Configure Cross Region Replication (CRR).
- Enable Server-Side Encryption.
- Enable Lifecycle Policies for backup management.

---

# Production Interview Question

Your company stores customer images in an EC2 server.

Storage is almost full and backups are becoming difficult.

What would you recommend?

### Answer

Move image storage to Amazon S3 because it provides:

- Unlimited storage
- High durability
- Better scalability
- Lower operational cost
- Easy integration with CloudFront
- Reduced load on EC2

---

# Production Interview Question

How would you securely allow an EC2 instance to upload logs to an S3 Bucket?

### Answer

- Create an IAM Role.
- Grant only required S3 permissions.
- Attach the Role to the EC2 instance.
- Avoid storing Access Keys.
- Enable Server-Side Encryption for sensitive logs.

---

# Troubleshooting Question

Users report slow uploads to S3.

What would you investigate?

### Answer

- Network bandwidth
- File size
- Multipart Upload usage
- AWS Region selection
- Internet latency
- Application performance

---

# Frequently Asked Interview Points

- S3 is Object Storage.
- S3 is a Regional Service.
- Bucket names are globally unique.
- Maximum Object Size is 5 TB.
- Versioning protects against accidental deletion.
- CRR requires Versioning.
- Lifecycle Rules reduce storage costs.
- Bucket Policy is Resource-Based.
- Block Public Access should remain enabled unless required.
- Multipart Upload improves large file uploads.

---

# Quick Revision

✔ S3 = Object Storage

✔ Bucket = Stores Objects

✔ Object = Actual File

✔ Object Key = Unique Identifier

✔ Metadata = Object Information

✔ Versioning = Multiple Versions

✔ Lifecycle = Automatic Storage Transition

✔ CRR = Disaster Recovery

✔ Bucket Policy = Resource-Based Access Control

✔ Block Public Access = Prevent Public Exposure

✔ Multipart Upload = Faster Large File Uploads

✔ Maximum Object Size = 5 TB

✔ S3 Durability = 99.999999999% (11 9's)
