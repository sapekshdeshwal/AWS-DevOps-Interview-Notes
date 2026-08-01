# AWS Placement Groups - Interview Questions

This document contains frequently asked AWS Placement Group interview questions, including basic concepts, comparison questions, production scenarios, troubleshooting, and rapid-fire questions.

---

# Basic Interview Questions

## Q1. What is an AWS Placement Group?

### Answer

An AWS Placement Group is a logical grouping of EC2 instances that controls how the instances are placed on the underlying AWS infrastructure.

It is used to optimize:

- Network Performance
- Latency
- Throughput
- Fault Tolerance

---

## Q2. Why do we need Placement Groups?

### Answer

Placement Groups help improve application performance or availability by controlling how EC2 instances are physically placed within an Availability Zone.

---

## Q3. How many types of Placement Groups are available in AWS?

### Answer

AWS provides three types of Placement Groups:

- Cluster Placement Group
- Partition Placement Group
- Spread Placement Group

---

## Q4. What is a Cluster Placement Group?

### Answer

A Cluster Placement Group places EC2 instances close together on the underlying hardware within the same Availability Zone.

It provides:

- Lowest latency
- Highest network throughput

---

## Q5. What is a Partition Placement Group?

### Answer

A Partition Placement Group divides EC2 instances into multiple logical partitions.

Each partition uses separate hardware, improving fault isolation.

---

## Q6. What is a Spread Placement Group?

### Answer

A Spread Placement Group places each EC2 instance on separate physical hardware.

This minimizes the risk of multiple instances failing because of a single hardware failure.

---

## Q7. Which Placement Group provides the lowest latency?

### Answer

Cluster Placement Group.

---

## Q8. Which Placement Group provides the highest fault tolerance?

### Answer

Spread Placement Group.

---

## Q9. Which Placement Group is best for distributed applications?

### Answer

Partition Placement Group.

Examples:

- Hadoop
- Kafka
- Cassandra
- HDFS

---

## Q10. Are Placement Groups Availability Zone specific?

### Answer

Yes.

Placement Groups exist within a single Availability Zone.

---

# Comparison Questions

## Q11. Difference between Cluster, Partition and Spread Placement Groups?

| Feature | Cluster | Partition | Spread |
|----------|----------|-----------|---------|
| Purpose | Performance | Fault Isolation | High Availability |
| Latency | Lowest | Moderate | Moderate |
| Throughput | Highest | High | Normal |
| Fault Tolerance | Low | Medium | High |
| Hardware Separation | No | Partition Level | Yes |

---

## Q12. Which Placement Group is best for HPC workloads?

### Answer

Cluster Placement Group.

---

## Q13. Which Placement Group is best for Production Applications?

### Answer

Spread Placement Group for small critical workloads requiring maximum availability.

---

## Q14. Which Placement Group is best for Big Data applications?

### Answer

Partition Placement Group.

---

## Q15. Which Placement Group is best for Machine Learning clusters?

### Answer

Cluster Placement Group because of its low latency and high throughput.

---

# AWS Practical Questions

## Q16. Which AWS CLI command creates a Placement Group?

### Answer

```bash
aws ec2 create-placement-group
```

---

## Q17. Which AWS CLI command lists Placement Groups?

### Answer

```bash
aws ec2 describe-placement-groups
```

---

## Q18. Which AWS CLI command deletes a Placement Group?

### Answer

```bash
aws ec2 delete-placement-group
```

---

## Q19. Can existing EC2 instances always be moved into a Placement Group?

### Answer

No.

In many cases, the instances must be stopped or recreated depending on the placement strategy and instance type.

---

## Q20. Can multiple EC2 instances belong to the same Placement Group?

### Answer

Yes.

Multiple EC2 instances can be launched within the same Placement Group.

---

# Production Scenario Questions

## Q21. Your application requires extremely low network latency between EC2 instances. Which Placement Group would you choose?

### Answer

Cluster Placement Group.

---

## Q22. Your distributed database must continue working even if one hardware rack fails. Which Placement Group would you use?

### Answer

Partition Placement Group.

---

## Q23. You have three critical production servers and want to minimize the chance of simultaneous hardware failure. Which Placement Group is best?

### Answer

Spread Placement Group.

---

## Q24. Your HPC application is experiencing network delays. What AWS feature could improve performance?

### Answer

Deploy the EC2 instances in a Cluster Placement Group.

---

## Q25. Why shouldn't Cluster Placement Groups be used for highly available production workloads?

### Answer

Because the instances are placed close together.

If the underlying hardware fails, multiple instances may be affected simultaneously.

---

# Troubleshooting Questions

## Q26. You are unable to launch an EC2 instance inside a Placement Group. What will you check?

### Answer

- Instance type compatibility
- Availability Zone
- Capacity availability
- Placement Group configuration
- AWS service limits

---

## Q27. Why are your EC2 instances still showing high network latency even after creating a Placement Group?

### Answer

Possible reasons:

- Instances are not launched in the Placement Group.
- Wrong Placement Group type selected.
- Application bottleneck.
- Different Availability Zones.

---

## Q28. Can a Placement Group span multiple Availability Zones?

### Answer

No.

Placement Groups are Availability Zone specific.

---

## Q29. Why is a Spread Placement Group not suitable for a large HPC cluster?

### Answer

Spread Placement Groups prioritize fault isolation rather than network performance.

They also support a limited number of instances per Availability Zone.

---

## Q30. Can one EC2 instance belong to multiple Placement Groups?

### Answer

No.

An EC2 instance can belong to only one Placement Group.

---

# Rapid Fire Questions & Answers

### Q31. How many Placement Group types are available?

**Answer:** Three.

---

### Q32. Which Placement Group provides the highest throughput?

**Answer:** Cluster Placement Group.

---

### Q33. Which Placement Group provides the highest availability?

**Answer:** Spread Placement Group.

---

### Q34. Which Placement Group provides fault isolation?

**Answer:** Partition Placement Group.

---

### Q35. Are Placement Groups AZ specific?

**Answer:** Yes.

---

### Q36. Which Placement Group is best for Hadoop?

**Answer:** Partition Placement Group.

---

### Q37. Which Placement Group is best for HPC?

**Answer:** Cluster Placement Group.

---

### Q38. Which Placement Group is best for Kafka?

**Answer:** Partition Placement Group.

---

### Q39. Which Placement Group places instances on separate hardware?

**Answer:** Spread Placement Group.

---

### Q40. Can one EC2 instance belong to multiple Placement Groups?

**Answer:** No.

---

# Interview Tips

- Remember the three Placement Group types:
  - **Cluster** → High Performance (Low Latency & High Throughput)
  - **Partition** → Fault Isolation (Distributed Applications)
  - **Spread** → High Availability (Critical Workloads)

- Placement Groups are **Availability Zone specific**.

- Choose the Placement Group based on the application's requirement:
  - Performance → Cluster
  - Fault Isolation → Partition
  - Maximum Availability → Spread

- Don't recommend Cluster Placement Groups for applications where hardware fault isolation is the highest priority.

- Mention real-world examples during interviews:
  - **Cluster** → HPC, Machine Learning, Scientific Computing
  - **Partition** → Hadoop, Kafka, Cassandra
  - **Spread** → Domain Controllers, Critical Production Servers
