# Amazon Elastic Block Store (EBS)

## What is Amazon EBS?

Amazon Elastic Block Store (EBS) is a **Block Storage** service provided by AWS that offers persistent storage for Amazon EC2 instances.

Unlike Amazon S3, which stores data as objects, Amazon EBS stores data in the form of **blocks**, just like the SSD or HDD inside a physical server.

An EBS volume can be attached to an EC2 instance and used as a hard disk to install an operating system, store applications, databases, logs, and user data.

---

# Why Do We Need Amazon EBS?

Imagine you have an EC2 instance hosting your company's application.

If you store all your data inside the EC2 instance itself and the instance fails or is terminated, you may lose your data.

Amazon EBS solves this problem by providing **persistent storage**.

Even if the EC2 instance is stopped, rebooted, or replaced, the data stored on the EBS volume remains safe (unless the volume is explicitly deleted).

---

# Real World Example

A company has deployed a Java application on an EC2 instance.

The server contains:

- Ubuntu Operating System
- Java
- Nginx
- Application Code
- Database Files
- Log Files

All of these are stored inside an EBS Volume.

If the EC2 instance needs to be upgraded, the company can:

- Stop the instance
- Detach the EBS volume
- Attach it to another EC2 instance

The application data remains available.

---

# What is Block Storage?

Block Storage stores data in small fixed-size blocks.

Each block has its own address.

The operating system combines these blocks to create files and directories.

Think of it like building a wall.

```
Wall

↓

Bricks

↓

Each Brick = Block
```

Linux reads and writes these blocks to store data efficiently.

---

# Types of Storage in AWS

AWS mainly provides three types of storage.

| Storage Type | Service | Example |
|--------------|----------|----------|
| Block Storage | Amazon EBS | EC2 Hard Disk |
| Object Storage | Amazon S3 | Images, Videos, Backups |
| File Storage | Amazon EFS | Shared File System |

---

# EBS vs S3 vs EFS

| Feature | Amazon EBS | Amazon S3 | Amazon EFS |
|----------|------------|-----------|------------|
| Storage Type | Block Storage | Object Storage | File Storage |
| Attached To | EC2 Instance | Internet/API | Multiple EC2 Instances |
| Maximum Size | Up to 64 TiB per volume | Virtually Unlimited | Elastic |
| File System Required | Yes | No | Yes |
| Mount Required | Yes | No | Yes |
| Use Case | OS, Database | Images, Videos, Backups | Shared Storage |

---

# EBS Architecture

```
                  AWS Cloud

               EC2 Instance
                     │
                     │
              Amazon EBS Volume
                     │
             File System (ext4/xfs)
                     │
             Files & Directories
```

---

# Key Features of Amazon EBS

- Persistent Storage
- Block Storage
- Highly Available
- Durable
- Supports Snapshots
- Supports Encryption
- Easy Volume Resize
- Multiple Volume Types
- Backup using Snapshots
- High Performance SSD & HDD Options

---

# Amazon EBS Volume Types

Amazon provides different volume types for different workloads.

## 1. General Purpose SSD (gp3)

Most commonly used EBS volume.

Suitable for:

- Web Servers
- Application Servers
- Development
- Testing

Advantages

- Low Cost
- High Performance
- Independent IOPS & Throughput

Recommended for most workloads.

---

## 2. General Purpose SSD (gp2)

Older generation SSD volume.

Still supported but AWS recommends gp3 because:

- Better Performance
- Lower Cost
- More Flexible

---

## 3. Provisioned IOPS SSD (io1)

Designed for applications requiring very high IOPS.

Examples

- Oracle Database
- SQL Server
- SAP

---

## 4. Provisioned IOPS SSD (io2)

Improved version of io1.

Advantages

- Higher Durability
- Better Reliability
- Supports Multi-Attach (supported configurations)

Used in production databases.

---

## 5. Throughput Optimized HDD (st1)

Designed for:

- Big Data
- Log Processing
- Data Warehousing

Not recommended for boot volumes.

---

## 6. Cold HDD (sc1)

Lowest-cost HDD volume.

Suitable for:

- Archived Data
- Rarely Accessed Data

---

# EBS Volume Comparison

| Volume Type | Storage | Best For |
|--------------|----------|----------|
| gp3 | SSD | General Purpose |
| gp2 | SSD | Older General Purpose |
| io1 | SSD | High IOPS Database |
| io2 | SSD | Critical Production Database |
| st1 | HDD | Big Data |
| sc1 | HDD | Archive Storage |

---

# Understanding IOPS

IOPS stands for **Input/Output Operations Per Second**.

It measures how many read and write operations a storage device can perform in one second.

Higher IOPS means better storage performance.

Example

Database Server

↓

Thousands of Read/Write Requests

↓

High IOPS Required

---

# Understanding Throughput

Throughput is the amount of data transferred per second.

Measured in:

- MB/s
- GB/s

Example

Video Streaming

↓

Large Files

↓

Higher Throughput Required

---

# Availability Zone Limitation

An EBS Volume belongs to **one Availability Zone (AZ)**.

Example

```
Mumbai Region

↓

ap-south-1a

↓

EBS Volume
```

An EBS volume **cannot be directly attached** to an EC2 instance in a different Availability Zone.

To move data across AZs:

- Create a Snapshot.
- Create a new EBS volume from that Snapshot in the target Availability Zone.

---

# Practical Overview

In our hands-on lab, we performed the following:

✔ Created an EBS Volume

✔ Attached the Volume to an EC2 Instance

✔ Verified the new disk in Linux

✔ Created a File System

✔ Mounted the Volume

✔ Stored Data

✔ Verified the Mount

✔ Unmounted the Volume

✔ Configured Persistent Mount using `/etc/fstab`

✔ Created a Snapshot

✔ Restored a Volume from Snapshot

✔ Resized the Volume

---

# Best Practices

- Use **gp3** for most workloads.
- Take regular snapshots for backup.
- Encrypt EBS volumes containing sensitive data.
- Tag volumes properly.
- Delete unused volumes to avoid unnecessary costs.
- Monitor storage usage and performance.
- Resize volumes proactively before they run out of space.

---

# Common Mistakes

- Confusing EBS with S3.
- Forgetting to mount a newly attached volume.
- Deleting a volume without taking a snapshot.
- Creating volumes in the wrong Availability Zone.
- Using expensive io2 volumes for simple workloads.
- Forgetting to update `/etc/fstab` after configuring persistent storage.

---

# Important Interview Points

- EBS is **Block Storage**.
- EBS is a **Regional Service**, but each volume is created in a **single Availability Zone**.
- EBS volumes are persistent.
- One EC2 instance can have multiple EBS volumes attached.
- Snapshots are stored in Amazon S3 (managed internally by AWS).
- gp3 is the recommended volume type for most workloads.
- EBS volumes can be resized without recreating them.
- A file system must be created before using a new EBS volume.

# Part2
# Linux Storage Fundamentals (EBS Practical)

Before using an Amazon EBS Volume, it is important to understand how Linux detects and manages storage devices.

Attaching an EBS volume in AWS is only the first step. Linux must detect the disk, create a file system, mount it, and make it available for storing data.

---

# EBS Volume Lifecycle

```
Create EBS Volume

        ↓

Attach to EC2

        ↓

Linux Detects Disk

        ↓

Create File System

        ↓

Create Mount Point

        ↓

Mount Volume

        ↓

Store Files

        ↓

Verify Mount

        ↓

(Optional)

Configure Persistent Mount

        ↓

Create Snapshot

        ↓

Resize Volume
```

---

# Step 1 - Verify Newly Attached Disk

## Command

```bash
lsblk
```

---

## What is lsblk?

`lsblk` stands for **List Block Devices**.

It displays all storage devices connected to the Linux system.

Examples include:

- Hard Disk
- SSD
- NVMe Disk
- Amazon EBS Volume
- USB Drive

---

## Why do we use lsblk?

Immediately after attaching an EBS volume from AWS, Linux does not automatically show it on the desktop.

We use `lsblk` to verify whether Linux has detected the new storage device.

---

## Example Output

```text
NAME    MAJ:MIN RM SIZE RO TYPE MOUNTPOINT

xvda      202:0 0   8G 0 disk
└─xvda1

xvdf      202:80 0 20G 0 disk
```

---

## Output Explanation

| Field | Meaning |
|--------|----------|
| NAME | Device Name |
| SIZE | Disk Size |
| TYPE | disk or partition |
| MOUNTPOINT | Mounted Directory |

---

## Interview Question

Why do we run **lsblk** after attaching an EBS Volume?

### Answer

To verify that Linux has detected the newly attached block storage device.

---

# Step 2 - Understanding Linux Device Names

When AWS attaches an EBS Volume, Linux assigns it a device name.

Examples

```
/dev/xvda

/dev/xvdf

/dev/nvme0n1
```

---

## What does /dev mean?

`/dev`

stands for

**Device Directory**

Linux represents every hardware device as a file.

Examples

```
Hard Disk

↓

/dev/xvda

Keyboard

↓

/dev/input

USB

↓

/dev/sdb
```

Everything in Linux is treated as a file.

---

## Common Device Names

| Device | Purpose |
|---------|----------|
| /dev/xvda | Root Disk |
| /dev/xvdf | Additional EBS Volume |
| /dev/nvme0n1 | NVMe SSD |
| /dev/sda | Physical Disk |

---

# Step 3 - What is a Block Device?

A Block Device stores data in fixed-size blocks.

Examples

- SSD
- HDD
- Amazon EBS
- NVMe

Block devices allow random read/write operations.

---

## Block Device vs Character Device

| Block Device | Character Device |
|---------------|-----------------|
| Stores Data in Blocks | Stores Data Character by Character |
| Random Access | Sequential Access |
| HDD | Keyboard |
| SSD | Mouse |
| Amazon EBS | Terminal |

---

## Interview Question

Is Amazon EBS a Block Storage or Object Storage?

### Answer

Amazon EBS is a **Block Storage** service.

---

# Step 4 - Check Disk Information

## Command

```bash
sudo fdisk -l
```

---

## What is fdisk?

`fdisk`

stands for

**Fixed Disk**

It is used to:

- View Partitions
- Create Partitions
- Delete Partitions

---

## Why do we use it?

To inspect disk partition information.

---

## Example Output

```text
Disk /dev/xvdf: 20 GiB
```

---

# Step 5 - What is a Partition?

A partition divides a physical disk into logical sections.

Example

20 GB Disk

↓

10 GB

↓

10 GB

Each partition behaves like an independent disk.

---

## Why Partition?

- Better Organization
- Multiple File Systems
- Multiple Operating Systems

---

# Step 6 - Create File System

## Command

```bash
sudo mkfs -t ext4 /dev/xvdf
```

---

## What is mkfs?

`mkfs`

means

**Make File System**

It prepares the disk so Linux can store files on it.

Without a file system, Linux cannot store files.

---

## Why is File System Required?

Imagine buying a new notebook.

Without page numbers or structure, it becomes difficult to organize information.

A File System organizes data on the disk.

---

# Common File Systems

| File System | Use Case |
|--------------|----------|
| ext4 | Most Common Linux File System |
| XFS | Large Enterprise Servers |
| ext3 | Older Linux Systems |
| ext2 | Legacy Systems |

---

## ext4

Advantages

- Stable
- Fast
- Journaling
- Recommended for most Linux systems

---

## XFS

Advantages

- High Performance
- Large File Support
- Enterprise Workloads

Commonly used in:

- Red Hat
- CentOS
- Enterprise Databases

---

## Interview Question

Can you store files immediately after attaching an EBS Volume?

### Answer

No.

First:

- Detect Disk
- Create File System
- Mount the Volume

---

# Step 7 - Create Mount Point

## Command

```bash
sudo mkdir /data
```

---

## What is a Mount Point?

A Mount Point is a directory where Linux attaches a storage device.

Examples

```
/data

/backup

/opt

/mnt
```

---

## Why Create a Mount Point?

Linux does not assign drive letters like Windows.

Instead, storage devices are attached to directories.

Example

Windows

```
D:
```

Linux

```
/data
```

---

# Step 8 - Mount the Volume

## Command

```bash
sudo mount /dev/xvdf /data
```

---

## What is Mounting?

Mounting is the process of attaching a storage device to the Linux file system.

After mounting

```
/data

↓

Amazon EBS Volume
```

Any files copied into `/data` are stored on the EBS Volume.

---

## Why Mount?

Without mounting

Linux knows the disk exists

BUT

Cannot store files.

Mounting connects the disk to the Linux directory structure.

---

# Step 9 - Verify Mounted Volume

## Command

```bash
df -h
```

---

## What is df?

`df`

stands for

**Disk Free**

Displays:

- Total Size
- Used Space
- Available Space

---

## What does -h mean?

`-h`

means

**Human Readable**

Instead of bytes

Displays

GB

MB

TB

---

## Sample Output

```text
Filesystem      Size Used Avail Mounted on

/dev/xvdf        20G 1G 19G /data
```

---

## Interview Question

How do you verify that your EBS Volume is successfully mounted?

### Answer

Use:

```bash
df -h
```

or

```bash
mount
```

---

# Step 10 - Check Mounted File Systems

## Command

```bash
mount
```

---

## Purpose

Displays all mounted file systems.

Useful for verifying:

- Mount Point
- File System Type
- Mounted Device


# Step 11 - Unmounting an EBS Volume

## Command

```bash
sudo umount /data
```

---

## What is Unmounting?

Unmounting means safely disconnecting a storage device from the Linux file system.

After unmounting, Linux stops using the volume and it can be detached safely from the EC2 instance.

```
Before

/data
   │
EBS Volume

After umount

/data

(No Storage Attached)
```

---

## Why do we Unmount?

Imagine removing a USB drive from your laptop while files are still being copied.

It may cause:

- Data Corruption
- File System Corruption
- Data Loss

The same applies to Amazon EBS.

Always unmount before detaching the volume.

---

## Verify Unmount

```bash
mount
```

or

```bash
df -h
```

If `/data` is not listed, the volume has been successfully unmounted.

---

## Interview Question

Why should we unmount an EBS volume before detaching it?

### Answer

Unmounting ensures all pending write operations are completed and prevents file system corruption or data loss.

---

# Step 12 - Check UUID

## Command

```bash
sudo blkid
```

---

## What is blkid?

`blkid`

stands for

**Block ID**

It displays information about storage devices.

Example Output

```text
/dev/xvdf: UUID="4c84d9f2-b7a3-4f91-a7ef-b32b5b4f1e9d" TYPE="ext4"
```

---

## What is UUID?

UUID stands for

**Universally Unique Identifier**

Every formatted disk receives a unique ID.

Example

```
UUID

↓

4c84d9f2-b7a3-4f91-a7ef-b32b5b4f1e9d
```

---

## Why do we use UUID?

Device names may change after reboot.

Example

Today

```
/dev/xvdf
```

Tomorrow

```
/dev/xvdg
```

UUID never changes.

Therefore, production servers use UUID instead of device names.

---

## Interview Question

Why is UUID preferred over `/dev/xvdf`?

### Answer

Device names can change after reboot or hardware changes, but UUID remains constant, making it reliable for persistent mounting.

---

# Step 13 - Persistent Mounting

## Problem

Suppose you mounted an EBS Volume.

```bash
mount /dev/xvdf /data
```

Everything works.

But after reboot...

```
df -h
```

The volume disappears.

Why?

Because Linux does not remember temporary mounts.

---

# Solution

Use

```
/etc/fstab
```

---

# What is /etc/fstab?

`fstab`

stands for

**File System Table**

It is a Linux configuration file that tells the operating system which file systems should be mounted automatically during boot.

---

## View fstab

```bash
cat /etc/fstab
```

---

## Edit fstab

```bash
sudo nano /etc/fstab
```

---

## Example

```text
UUID=4c84d9f2-b7a3-4f91-a7ef-b32b5b4f1e9d /data ext4 defaults,nofail 0 2
```

---

## Explanation

| Field | Meaning |
|---------|----------|
| UUID | Disk Identifier |
| /data | Mount Point |
| ext4 | File System |
| defaults | Default Mount Options |
| nofail | Continue Boot Even if Disk Missing |
| 0 | Dump Utility |
| 2 | File System Check Order |

---

## Why use nofail?

Imagine an EBS Volume is accidentally detached.

Without

```
nofail
```

Linux may fail to boot.

Using

```
nofail
```

allows the system to continue booting.

---

## Verify fstab

Never reboot immediately after editing.

Instead run

```bash
sudo mount -a
```

---

## What does mount -a do?

It checks the `/etc/fstab` file and attempts to mount all configured file systems.

If there is an error, it will be displayed immediately.

---

## Interview Question

What command should you run after editing `/etc/fstab`?

### Answer

```bash
sudo mount -a
```

This verifies that the configuration is correct before rebooting.

---

# Step 14 - EBS Snapshots

## What is Snapshot?

An EBS Snapshot is a point-in-time backup of an EBS Volume.

Snapshots are incremental.

Only changed blocks are stored after the first snapshot.

---

## Why Snapshots?

- Backup
- Disaster Recovery
- Restore Deleted Data
- Migration
- Clone Volumes

---

## Snapshot Workflow

```
EBS Volume

↓

Create Snapshot

↓

AWS Stores Snapshot

↓

Create New Volume

↓

Attach to EC2
```

---

## Important Interview Point

Snapshots are stored in Amazon S3 internally.

Users cannot directly access the S3 bucket.

AWS manages it automatically.

---

# Step 15 - Resize EBS Volume

Suppose your disk becomes full.

Current Size

```
20 GB
```

Need

```
50 GB
```

AWS allows online resizing.

---

## Steps

1. Modify Volume in AWS Console

↓

2. Verify Linux detects new size

↓

3. Extend Partition

↓

4. Extend File System

---

## Check Current Disk

```bash
lsblk
```

---

## Grow Partition

```bash
sudo growpart /dev/xvdf 1
```

---

## What is growpart?

It expands the existing partition to use the newly added disk space.

---

## Resize ext4 File System

```bash
sudo resize2fs /dev/xvdf1
```

---

## Resize XFS File System

```bash
sudo xfs_growfs /data
```

---

## Verify

```bash
df -h
```

---

## Interview Question

Does increasing the EBS volume size automatically increase the Linux file system?

### Answer

No.

You must also expand the partition and resize the file system.

---

# Step 16 - Disk Usage

## Check File System Usage

```bash
df -h
```

Shows:

- Total Size
- Used Space
- Available Space

---

## Check Folder Size

```bash
du -sh /data
```

---

## Difference between df and du

| df | du |
|----|----|
| Shows Disk Usage | Shows Directory/File Size |
| File System Level | Folder Level |

---

## Interview Question

When would you use `du -sh` instead of `df -h`?

### Answer

Use `du -sh` when you want to identify which directory is consuming disk space.

---

# Production Troubleshooting

## Scenario 1

EBS Volume attached.

But not visible.

Check

```bash
lsblk
```

```bash
sudo fdisk -l
```

---

## Scenario 2

Cannot store files.

Check

- File System created?
- Volume Mounted?

---

## Scenario 3

Server rebooted.

Volume disappeared.

Check

```
/etc/fstab
```

---

## Scenario 4

Disk Full.

Commands

```bash
df -h
```

```bash
du -sh /*
```

Increase EBS Size.

Resize File System.

---

# Best Practices

- Always use UUID in `/etc/fstab`.
- Verify with `mount -a`.
- Take Snapshot before resizing.
- Use ext4 or XFS.
- Monitor disk usage regularly.
- Keep backups before filesystem changes.

---

# Common Mistakes

❌ Detaching without unmounting.

❌ Forgetting to resize filesystem.

❌ Using device names instead of UUID.

❌ Editing `/etc/fstab` without verification.

❌ Forgetting Snapshot before major changes.

---

# Practical Commands Summary

lsblk                     # List Block Devices

fdisk -l                  # Show Disk & Partition Details

mkfs -t ext4 /dev/xvdf    # Create ext4 File System

mkdir /data               # Create Mount Point

mount /dev/xvdf /data     # Mount Volume

df -h                     # Check Disk Usage

mount                     # List Mounted File Systems

umount /data              # Unmount Volume

blkid                     # Display UUID

cat /etc/fstab            # View fstab

nano /etc/fstab           # Edit fstab

mount -a                  # Verify fstab

growpart /dev/xvdf 1      # Extend Partition

resize2fs /dev/xvdf1      # Resize ext4

xfs_growfs /data          # Resize XFS

du -sh /data              # Check Directory Size

# Important Interview Points

- Linux detects EBS as a block device.
- Every new EBS volume must be formatted before first use.
- A file system is required to store files.
- Linux uses mount points instead of drive letters.
- `lsblk` verifies storage devices.
- `df -h` verifies mounted storage and available space.
- `mount` connects the storage device to the Linux directory tree.
- Always unmount before detaching an EBS volume.
- UUID is preferred over device names.
- `/etc/fstab` enables persistent mounting.
- Test `/etc/fstab` with `mount -a`.
- Snapshots are incremental.
- Expanding an EBS volume requires filesystem resizing.
- `df -h` shows filesystem usage, while `du -sh` shows directory usage.


# Linux Storage Internals for DevOps

Understanding Linux storage is essential for every DevOps Engineer because Amazon EBS is simply a block storage device. Once it is attached to an EC2 instance, Linux becomes responsible for managing the storage.

This section explains how Linux internally stores files and manages storage devices.

---

# Everything in Linux is a File

One of the most important Linux concepts is:

> Everything in Linux is treated as a file.

Examples:

| Resource | Linux Representation |
|----------|----------------------|
| Hard Disk | /dev/xvda |
| EBS Volume | /dev/xvdf |
| Keyboard | /dev/input |
| Mouse | /dev/input |
| Terminal | /dev/tty |
| USB Device | /dev/sdb |

This design allows Linux to interact with hardware using standard file operations.

---

# What is an Inode?

An Inode (Index Node) is a data structure that stores metadata about a file.

Think of it as the **identity card** of a file.

The file name is **NOT** stored inside the inode.

---

# What information does an Inode store?

An inode stores:

- File Size
- File Owner
- Group Owner
- File Permissions
- Creation Time
- Modification Time
- Access Time
- Number of Hard Links
- Location of Data Blocks

---

# What is NOT stored in an Inode?

An inode does NOT store:

- File Name

Linux stores file names separately in directory entries.

---

# Why doesn't Linux store the filename inside the inode?

Because multiple filenames can point to the same inode.

This is how Hard Links work.

---

# Check Inode Number

## Command

```bash
ls -i
```

---

## Example

```text
152463 report.txt
```

Here

```
152463

↓

Inode Number
```

---

# View Detailed File Information

```bash
stat report.txt
```

---

## Why do we use stat?

It displays:

- Inode Number
- File Size
- Permissions
- Owner
- Timestamps

---

# Interview Question

What is an Inode?

### Answer

An Inode is a Linux data structure that stores metadata about a file except its filename.

---

# Hard Link

A Hard Link is another filename that points to the same inode.

Example

Original File

```
report.txt
```

Create Hard Link

```bash
ln report.txt report_backup.txt
```

---

# Verify

```bash
ls -li
```

Example

```text
152463 report.txt

152463 report_backup.txt
```

Notice

Both files have

Same Inode Number

---

# Hard Link Architecture

```
               Inode 152463
                    │
          ┌─────────┴─────────┐
          │                   │
     report.txt      report_backup.txt
```

---

# Characteristics of Hard Link

- Same Inode
- Same Data
- Multiple File Names
- Consumes almost no additional space
- Deleting one file does NOT delete the data.

---

# Hard Link Example

Delete

```bash
rm report.txt
```

Still exists

```
report_backup.txt
```

Why?

Because the inode still has one reference.

---

# Soft Link (Symbolic Link)

A Soft Link is a shortcut to another file.

Example

```bash
ln -s report.txt report_link.txt
```

---

# Verify

```bash
ls -l
```

Example

```text
report_link.txt -> report.txt
```

---

# Soft Link Architecture

```
report_link.txt

↓

report.txt

↓

Inode
```

---

# Characteristics of Soft Link

- Different Inode
- Acts like a shortcut
- Can link directories
- Can link across file systems
- Becomes broken if original file is deleted

---

# Difference Between Hard Link and Soft Link

| Hard Link | Soft Link |
|------------|-----------|
| Same Inode | Different Inode |
| Cannot cross File Systems | Can cross File Systems |
| Cannot link Directories | Can link Directories |
| Survives Original File Deletion | Breaks if Original File is Deleted |

---

# Interview Question

When would you use a Soft Link?

### Answer

Soft Links are commonly used for:

- Application shortcuts
- Configuration files
- Log directories
- Version management

Example

```
java

↓

java-21
```

---

# Device Files

Linux represents storage devices as files.

Examples

```
/dev/xvda

/dev/xvdf

/dev/sdb

/dev/nvme0n1
```

These are called Device Files.

---

# Block Device

A Block Device stores data in blocks.

Examples

- Amazon EBS
- SSD
- HDD
- NVMe

Supports

Random Read

Random Write

---

# Character Device

Character Devices transfer data character by character.

Examples

- Keyboard
- Mouse
- Serial Port

---

# Block Device vs Character Device

| Block Device | Character Device |
|---------------|-----------------|
| Data stored in Blocks | Data stored Character by Character |
| Random Access | Sequential Access |
| HDD | Keyboard |
| SSD | Mouse |
| Amazon EBS | Terminal |

---

# Journaling

Modern Linux File Systems like ext4 and XFS support Journaling.

Before writing data

↓

Linux records the operation in a Journal.

If power fails

↓

Linux can recover safely.

Advantages

- Prevents Corruption
- Faster Recovery
- Better Reliability

---

# Production Scenario

Developer says

"I attached the EBS volume but cannot see any files."

What will you check?

Answer

- lsblk
- File System
- Mount Status
- Mount Point
- df -h
- mount

---

# Production Scenario

Server rebooted.

Application data disappeared.

Possible Reason

Volume was mounted manually.

Persistent Mount using

```
/etc/fstab
```

was not configured.

---

# Production Scenario

Developer deleted the original file.

Application still works.

Possible Reason

Application is using a Hard Link.

---

# Production Scenario

Developer deleted original file.

Shortcut stopped working.

Reason

Soft Link became broken.

---

# Assignment Summary

During Hands-on, we performed:

✔ Created EBS Volume

✔ Attached Volume

✔ Verified using lsblk

✔ Checked Partition

✔ Created File System

✔ Created Mount Point

✔ Mounted Volume

✔ Verified using df -h

✔ Created Test Files

✔ Unmounted Volume

✔ Retrieved UUID

✔ Configured /etc/fstab

✔ Verified Persistent Mount

✔ Created Snapshot

✔ Restored Volume

✔ Resized Volume

✔ Expanded File System

---

# Best Practices

- Always use UUID inside /etc/fstab.
- Take Snapshot before resizing.
- Prefer ext4 or XFS.
- Use Hard Links only when required.
- Use Soft Links for application shortcuts.
- Verify mounts after reboot.
- Monitor disk usage regularly.

---

# Common Interview Questions

Q. What is an Inode?

Q. Does an Inode store filename?

Q. Difference between Hard Link and Soft Link?

Q. What is Journaling?

Q. Why do we use UUID?

Q. Why does Linux use Mount Points?

Q. Difference between Block Device and Character Device?

Q. Difference between ext4 and XFS?

Q. Why should EBS be unmounted before detaching?

Q. What happens if /etc/fstab contains an incorrect entry?

---

# Quick Revision

✔ EBS = Block Storage

✔ File System = Organizes Data

✔ Mount = Attach Storage to Directory

✔ UUID = Unique Disk Identifier

✔ Inode = Metadata of File

✔ Hard Link = Same Inode

✔ Soft Link = Shortcut

✔ ext4 = Common Linux File System

✔ XFS = Enterprise File System

✔ Block Device = HDD, SSD, EBS

✔ Character Device = Keyboard, Mouse

✔ /etc/fstab = Persistent Mount Configuration

✔ Journaling = Crash Recovery Mechanism
