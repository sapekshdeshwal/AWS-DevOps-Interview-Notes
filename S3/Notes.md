# Amazon Simple Storage Service (S3)

## What is Amazon S3?

Amazon Simple Storage Service (Amazon S3) is a fully managed Object Storage service provided by AWS that allows users to store and retrieve any amount of data from anywhere in the world.

Unlike EBS, S3 stores data as **Objects** inside **Buckets**.

---

# Why S3?

Before S3:

- Limited storage capacity
- Expensive storage infrastructure
- Manual backups
- Difficult scalability

With S3:

- Unlimited object storage
- Highly Durable (99.999999999%)
- Highly Available
- Secure
- Cost Effective
- Automatic Scaling

---

# Key Features

- Object Storage
- Unlimited Storage
- 11 9's Durability
- High Availability
- Encryption
- Versioning
- Lifecycle Management
- Cross Region Replication (CRR)
- Static Website Hosting
- Event Notifications
- Bucket Policies
- Access Logging

---

# S3 Architecture

```text
               User
                 │
            Internet
                 │
            S3 Bucket
                 │
        ------------------
        |       |        |
     image.jpg  file.pdf backup.zip
```

---

# S3 Terminology

## Bucket

A Bucket is a logical container used to store objects.

Example:

```
company-backup
```

Bucket Names:

- Must be globally unique.
- 3–63 characters.
- Lowercase letters only.
- Can include numbers and hyphens (-).

---

## Object

An Object is the actual file stored inside a bucket.

Examples:

- image.jpg
- invoice.pdf
- backup.zip
- video.mp4

Maximum Object Size:

**5 TB**

---

## Object Key

Every object has a unique key.

Example:

```
images/profile.jpg
```

---

## Metadata

Metadata stores information about an object.

Examples:

- File Size
- Content Type
- Last Modified
- Encryption Type
- Tags

---

# S3 Storage Classes

## Standard

- Frequently accessed data
- High Availability
- Low Latency

Example:

Website Images

---

## Standard-IA (Infrequent Access)

- Less frequently accessed
- Lower storage cost
- Retrieval charges apply

Example:

Monthly Reports

---

## One Zone-IA

- Stored in one Availability Zone
- Lower cost
- Suitable for non-critical data

---

## Intelligent-Tiering

Automatically moves objects between storage tiers based on access patterns.

Best for unknown or changing access patterns.

---

## Glacier Instant Retrieval

- Rarely accessed
- Millisecond retrieval
- Lower storage cost

---

## Glacier Flexible Retrieval

- Archive storage
- Retrieval takes minutes to hours

---

## Glacier Deep Archive

- Lowest storage cost
- Retrieval may take up to 12 hours
- Best for long-term archival

---

# S3 Versioning

Versioning keeps multiple versions of the same object.

Benefits:

- Recover deleted files
- Recover overwritten files
- Protect against accidental deletion

---

# Lifecycle Rules

Lifecycle Rules automatically move or delete objects.

Example:

After 30 Days

↓

Move to Standard-IA

↓

After 90 Days

↓

Move to Glacier

↓

After 365 Days

↓

Delete Object

---

# Cross Region Replication (CRR)

Copies objects automatically to another AWS Region.

Benefits:

- Disaster Recovery
- High Availability
- Compliance

Requirements:

- Versioning enabled on both buckets.
- Destination bucket in another region.

---

# Server Side Encryption (SSE)

S3 supports:

- SSE-S3
- SSE-KMS
- SSE-C

Used to protect stored data.

---

# Bucket Policy

A Bucket Policy is a Resource-Based Policy used to control access to an S3 bucket.

Example Use Cases:

- Public Website
- Cross Account Access
- Restrict IP Address

---

# S3 vs EBS

| Amazon S3 | Amazon EBS |
|------------|------------|
| Object Storage | Block Storage |
| Unlimited Storage | Limited Volume Size |
| Stores Objects | Stores Blocks |
| Access over Internet/API | Attached to EC2 |
| Highly Scalable | Attached to Instances |

---

# Practical Performed

- Create S3 Bucket
- Upload Objects
- Download Objects
- Delete Objects
- Enable Versioning
- Configure Bucket Policy
- Enable Encryption
- Configure Lifecycle Rule
- Enable Cross Region Replication
- Host Static Website

---

# Best Practices

- Enable Versioning.
- Enable Encryption.
- Block Public Access unless required.
- Follow Least Privilege.
- Use Lifecycle Rules.
- Enable Server Access Logging.
- Use Bucket Policies carefully.
- Enable MFA Delete for critical buckets.

---

# Common Mistakes

- Publicly exposing buckets.
- Disabling Versioning.
- Using "*" permissions.
- Forgetting Encryption.
- Deleting buckets without backups.
- Ignoring Lifecycle Policies.

---

# AWS CLI Commands

Create Bucket

```bash
aws s3 mb s3://my-demo-bucket
```

List Buckets

```bash
aws s3 ls
```

Upload File

```bash
aws s3 cp file.txt s3://my-demo-bucket/
```

Download File

```bash
aws s3 cp s3://my-demo-bucket/file.txt .
```

Sync Folder

```bash
aws s3 sync ./backup s3://my-demo-bucket
```

Delete Object

```bash
aws s3 rm s3://my-demo-bucket/file.txt
```

Delete Bucket

```bash
aws s3 rb s3://my-demo-bucket
```

---

# Quick Revision

| Component | Purpose |
|-----------|---------|
| Bucket | Stores Objects |
| Object | Actual File |
| Object Key | Unique Object Name |
| Metadata | Information about Object |
| Versioning | Maintain Multiple Versions |
| Lifecycle Rule | Automatic Data Transition |
| CRR | Cross Region Replication |
| Bucket Policy | Resource-Based Access Control |
| SSE | Encryption |
| S3 | Object Storage |

---

# Important Interview Points

- S3 is a Regional Service.
- Buckets are globally unique.
- Maximum Object Size is 5 TB.
- S3 provides 99.999999999% (11 9's) durability.
- Versioning protects against accidental deletion.
- Lifecycle Rules reduce storage costs.
- Bucket Policies are resource-based policies.
- S3 is Object Storage, whereas EBS is Block Storage.
- CRR requires Versioning to be enabled.
- Block Public Access should remain enabled unless public access is intentionally required.
