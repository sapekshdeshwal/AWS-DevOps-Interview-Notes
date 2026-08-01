# Amazon EBS Interview Guide

This guide contains frequently asked Amazon EBS interview questions, including basic concepts, Linux commands, production scenarios, troubleshooting, and real-world use cases.

---

# Basic Interview Questions

## Q1. What is Amazon EBS?

### Answer

Amazon Elastic Block Store (EBS) is a persistent Block Storage service provided by AWS for EC2 instances.

It stores data in blocks and behaves like a virtual hard disk attached to an EC2 instance.

---

## Q2. Why do we need Amazon EBS?

### Answer

Amazon EBS provides persistent storage for:

- Operating Systems
- Applications
- Databases
- Log Files
- User Data

Unlike Instance Store, data remains available even after stopping the EC2 instance.

---

## Q3. Is Amazon EBS Block Storage or Object Storage?

### Answer

Amazon EBS is a **Block Storage** service.

---

## Q4. What is the difference between EBS, S3 and EFS?

| Feature | EBS | S3 | EFS |
|----------|-----|----|-----|
| Storage Type | Block | Object | File |
| Mount Required | Yes | No | Yes |
| Attached To | EC2 | API | Multiple EC2 |
| Best Use Case | OS, Database | Images, Backup | Shared Storage |

---

## Q5. Can one EBS Volume be attached to multiple EC2 instances?

### Answer

Normally **No**.

Only specific **io1/io2 Multi-Attach** volumes support attachment to multiple compatible EC2 instances.

---

## Q6. Can one EC2 have multiple EBS volumes?

### Answer

Yes.

An EC2 instance can have multiple EBS volumes attached depending on instance limits.

---

## Q7. Can an EBS Volume be attached across Availability Zones?

### Answer

No.

An EBS volume can only be attached to an EC2 instance in the **same Availability Zone**.

To move data across AZs:

- Create a Snapshot.
- Create a new EBS Volume in the target AZ.

---

# Linux + EBS Questions

## Q8. What should you do immediately after attaching an EBS Volume?

### Answer

Verify whether Linux detects the volume.

```bash
lsblk
```

---

## Q9. What does `lsblk` do?

### Answer

`lsblk` lists all block storage devices connected to the Linux system.

It is commonly used after attaching an EBS volume to verify that Linux has detected the disk.

---

## Q10. Why can't we store files immediately after attaching an EBS volume?

### Answer

Because a newly attached EBS volume usually has no file system.

The steps are:

1. Detect Disk
2. Create File System
3. Create Mount Point
4. Mount Volume

---

## Q11. What is a File System?

### Answer

A File System organizes how data is stored and retrieved from a storage device.

Without a file system, Linux cannot store files on the disk.

---

## Q12. Which File Systems are commonly used?

### Answer

- ext4
- XFS

---

## Q13. What command creates a File System?

```bash
sudo mkfs -t ext4 /dev/xvdf
```

### Answer

`mkfs` (Make File System) prepares the disk for storing files.

---

## Q14. What is a Mount Point?

### Answer

A Mount Point is a directory where Linux attaches a storage device.

Example:

```
/data
```

---

## Q15. What is Mounting?

### Answer

Mounting connects a storage device to the Linux directory structure so that files can be read and written.

---

## Q16. Which command mounts an EBS Volume?

```bash
sudo mount /dev/xvdf /data
```

---

## Q17. How do you verify that the volume is mounted?

```bash
df -h
```

or

```bash
mount
```

---

## Q18. What is the difference between `df` and `du`?

| df | du |
|----|----|
| File System Usage | Directory Usage |
| Disk Level | Folder Level |

---

## Q19. What does `du -sh` do?

### Answer

Displays the size of a directory in a human-readable format.

---

## Q20. Why should an EBS Volume be unmounted before detaching?

### Answer

To ensure pending write operations are completed and prevent data corruption or file system corruption.

---

## Q21. Which command unmounts a volume?

```bash
sudo umount /data
```

---

# UUID & fstab

## Q22. What is UUID?

### Answer

UUID (Universally Unique Identifier) is a unique identifier assigned to a file system after formatting.

---

## Q23. Why is UUID preferred over `/dev/xvdf`?

### Answer

Device names may change after reboot, but UUID remains constant.

---

## Q24. Which command displays UUID?

```bash
sudo blkid
```

---

## Q25. What is `/etc/fstab`?

### Answer

`/etc/fstab` is a Linux configuration file used to automatically mount file systems during system boot.

---

## Q26. Why do we use `mount -a`?

### Answer

It verifies the `/etc/fstab` configuration before rebooting.

---

# Snapshot Questions

## Q27. What is an EBS Snapshot?

### Answer

A point-in-time backup of an EBS volume.

---

## Q28. Are EBS Snapshots full backups?

### Answer

The first snapshot is full.

Subsequent snapshots are **incremental**, storing only changed blocks.

---

## Q29. Where are Snapshots stored?

### Answer

Internally in Amazon S3 (managed by AWS).

---

## Q30. Why are Snapshots important?

### Answer

- Backup
- Disaster Recovery
- Migration
- Restore Volumes

---

# Resize Questions

## Q31. What happens after increasing an EBS Volume size?

### Answer

Linux does not automatically use the additional space.

You must:

- Extend the partition (if required)
- Resize the file system

---

## Q32. Which command extends an ext4 file system?

```bash
resize2fs
```

---

## Q33. Which command extends an XFS file system?

```bash
xfs_growfs
```

---

## Q34. What does `growpart` do?

### Answer

It expands an existing partition to use the additional disk space after the EBS volume has been increased.

---

# Linux Concepts

## Q35. What is an Inode?

### Answer

An Inode is a Linux data structure that stores metadata about a file except its filename.

---

## Q36. Does an Inode store the filename?

### Answer

No.

The filename is stored in the directory entry, not in the inode.

---

## Q37. Which command displays the inode number?

```bash
ls -i
```

---

## Q38. What is a Hard Link?

### Answer

A Hard Link is another filename pointing to the same inode.

Both names refer to the same underlying data.

---

## Q39. What is a Soft Link?

### Answer

A Soft Link (Symbolic Link) is a shortcut that points to another file.

---

## Q40. Difference between Hard Link and Soft Link?

| Hard Link | Soft Link |
|------------|-----------|
| Same Inode | Different Inode |
| Cannot cross File Systems | Can cross File Systems |
| Survives Original File Deletion | Breaks if Original File is Deleted |

---

# Scenario-Based Questions

## Scenario 1

You attached an EBS volume, but it is not visible in Linux.

### Answer

Check:

```bash
lsblk
```

```bash
sudo fdisk -l
```

Verify the volume is attached to the correct EC2 instance and Availability Zone.

---

## Scenario 2

The volume is attached but you cannot store files.

### Answer

Check:

- File system created?
- Volume mounted?
- Correct mount point?

---

## Scenario 3

After reboot, the mounted volume disappeared.

### Answer

Check:

```bash
cat /etc/fstab
```

Verify using:

```bash
sudo mount -a
```

---

## Scenario 4

The disk is full.

### Answer

Check:

```bash
df -h
```

```bash
du -sh /*
```

Then:

- Increase EBS volume size
- Extend partition (if required)
- Resize the filesystem

---

## Scenario 5

A user accidentally detached an EBS volume without unmounting it.

### Answer

Possible consequences:

- Data corruption
- File system corruption
- Incomplete writes

Always unmount before detaching.

---

## Scenario 6

A developer resized an EBS volume from 20 GB to 50 GB, but Linux still shows 20 GB.

### Answer

AWS increased the volume size, but the Linux filesystem still needs to be expanded using:

- `growpart` (if needed)
- `resize2fs` (ext4)
- `xfs_growfs` (XFS)

---

# Production Interview Question

## Q41. How do you safely increase storage on a production EC2 instance?

### Answer

1. Take an EBS Snapshot.
2. Modify the EBS volume size.
3. Verify the new size with `lsblk`.
4. Extend the partition if required.
5. Resize the filesystem.
6. Verify with `df -h`.
7. Monitor the application after the change.

---

# Rapid Fire Questions

# Rapid Fire Interview Questions & Answers

### 1. What is Amazon EBS?

Amazon Elastic Block Store (EBS) is a persistent block storage service used with Amazon EC2 instances. It behaves like a virtual hard disk and is used to store operating systems, applications, databases, and user data.

---

### 2. Is Amazon EBS Block Storage or Object Storage?

Amazon EBS is a **Block Storage** service.

---

### 3. Why is a File System required?

A file system organizes how files and directories are stored on a disk. Without a file system, Linux cannot read or write data to the storage device.

---

### 4. What is the difference between ext4 and XFS?

**ext4**

- Most commonly used Linux file system
- Easy to resize
- Suitable for general workloads

**XFS**

- High-performance file system
- Better for large files and enterprise workloads
- Commonly used on RHEL/CentOS

---

### 5. Why do we use `lsblk`?

`lsblk` lists all block storage devices connected to the Linux system.

It is mainly used after attaching an EBS volume to verify that Linux has detected the new disk.

---

### 6. What is `mkfs`?

`mkfs` (Make File System) creates a file system on a storage device, making it ready to store files.

Example:

```bash
sudo mkfs -t ext4 /dev/xvdf
```

---

### 7. Why do we mount a volume?

Mounting connects a storage device to the Linux directory tree.

Without mounting, Linux detects the disk but cannot use it for storing files.

---

### 8. What is the difference between `df` and `du`?

**df**

- Shows file system usage
- Displays total, used, and available disk space

**du**

- Shows the size of files or directories
- Useful for identifying which folder consumes storage

---

### 9. Why do we use UUID?

UUID (Universally Unique Identifier) uniquely identifies a file system.

It is preferred over device names because device names like `/dev/xvdf` may change after a reboot, while the UUID remains constant.

---

### 10. What is `/etc/fstab`?

`/etc/fstab` is a Linux configuration file used to automatically mount file systems during system startup.

---

### 11. Why do we use `mount -a`?

`mount -a` verifies the `/etc/fstab` configuration and mounts all configured file systems without requiring a reboot.

---

### 12. What is an EBS Snapshot?

An EBS Snapshot is a point-in-time backup of an EBS volume.

It is used for backup, disaster recovery, migration, and restoring data.

---

### 13. Are EBS Snapshots incremental?

Yes.

The first snapshot is a full backup.

Subsequent snapshots store only the changed blocks, reducing storage usage and backup time.

---

### 14. What is an Inode?

An Inode is a Linux data structure that stores metadata about a file, such as permissions, ownership, timestamps, size, and disk block locations.

It does **not** store the filename.

---

### 15. What is the difference between Hard Link and Soft Link?

**Hard Link**

- Points to the same inode
- Survives deletion of the original filename
- Cannot cross file systems

**Soft Link**

- Has a different inode
- Acts like a shortcut
- Can cross file systems
- Breaks if the original file is deleted

---

### 16. What happens if you detach an EBS volume without unmounting it?

Possible issues include:

- Data corruption
- File system corruption
- Incomplete write operations
- Application errors

Always unmount the volume before detaching it.

---

### 17. Why doesn't Linux automatically use the extra space after resizing an EBS volume?

Increasing the EBS volume size only changes the underlying storage capacity.

You must also:

- Extend the partition (if required)
- Resize the file system using `resize2fs` or `xfs_growfs`

Only then will Linux recognize and use the additional space.

---

# Interview Tips

- Explain the complete EBS workflow rather than isolated commands.
- Mention Linux commands while answering AWS questions.
- Always include safety practices such as snapshots before resizing and unmounting before detaching.
- When discussing production systems, mention verification steps (`lsblk`, `df -h`, `mount -a`) and backups before making changes.
