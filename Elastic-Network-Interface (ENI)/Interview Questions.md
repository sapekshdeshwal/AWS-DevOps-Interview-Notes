# AWS Elastic Network Interface (ENI) - Interview Questions

This document contains frequently asked AWS Elastic Network Interface (ENI) interview questions, including basic concepts, production scenarios, troubleshooting, and rapid-fire questions.

---

# Basic Interview Questions

## Q1. What is an Elastic Network Interface (ENI)?

### Answer

An Elastic Network Interface (ENI) is a virtual network card used by an Amazon EC2 instance to communicate within a VPC and with other networks.

It contains networking information such as:

- Private IP Address
- Public IP / Elastic IP
- MAC Address
- Security Groups
- Subnet Information

---

## Q2. Why do we need an ENI?

### Answer

An ENI provides network connectivity to an EC2 instance.

Without an ENI, an EC2 instance cannot communicate with:

- Internet
- Other EC2 Instances
- AWS Services
- On-Premises Networks

---

## Q3. Is an ENI a physical or virtual network card?

### Answer

An ENI is a **virtual network interface card (vNIC)** provided by AWS.

---

## Q4. What information does an ENI contain?

### Answer

An ENI contains:

- Primary Private IP
- Secondary Private IPs
- Public IP (Optional)
- Elastic IP (Optional)
- MAC Address
- Security Groups
- Subnet
- VPC Information

---

## Q5. Does every EC2 instance require an ENI?

### Answer

Yes.

Every EC2 instance has at least one Primary ENI.

---

## Q6. What are the types of ENIs?

### Answer

- Primary ENI
- Secondary ENI

---

## Q7. What is a Primary ENI?

### Answer

A Primary ENI is automatically created when an EC2 instance is launched.

It cannot be detached from the instance.

---

## Q8. What is a Secondary ENI?

### Answer

A Secondary ENI is an additional network interface that can be manually created, attached, detached, and moved between EC2 instances within the same Availability Zone.

---

## Q9. Can the Primary ENI be detached?

### Answer

No.

The Primary ENI cannot be detached while the EC2 instance exists.

---

## Q10. Can a Secondary ENI be detached?

### Answer

Yes.

A Secondary ENI can be detached and attached to another compatible EC2 instance within the same Availability Zone.

---

# Networking Questions

## Q11. Can an ENI have multiple Private IP addresses?

### Answer

Yes.

An ENI supports one Primary Private IP and multiple Secondary Private IP addresses.

---

## Q12. Can an Elastic IP be associated with an ENI?

### Answer

Yes.

An Elastic IP is associated with an ENI.

---

## Q13. Can multiple Security Groups be attached to an ENI?

### Answer

Yes.

An ENI can have one or more Security Groups attached.

---

## Q14. Is an ENI Availability Zone specific?

### Answer

Yes.

An ENI can only be attached to EC2 instances within the same Availability Zone.

---

## Q15. Can an ENI be moved across Regions?

### Answer

No.

ENIs are Region and Availability Zone specific.

---

# Comparison Questions

## Q16. Difference between ENI and Elastic IP?

| ENI | Elastic IP |
|------|------------|
| Virtual Network Interface | Static Public IPv4 Address |
| Provides Network Connectivity | Provides Internet Reachability |
| Contains Private IP | Associated with ENI |

---

## Q17. Difference between ENI and Security Group?

| ENI | Security Group |
|------|----------------|
| Virtual Network Interface | Virtual Firewall |
| Handles Network Connectivity | Controls Allowed Traffic |
| Contains IP Addresses | Contains Security Rules |

---

## Q18. Difference between Primary ENI and Secondary ENI?

| Primary ENI | Secondary ENI |
|--------------|---------------|
| Automatically Created | Manually Created |
| Cannot be Detached | Can be Detached |
| Mandatory | Optional |

---

# AWS Practical Questions

## Q19. Which AWS CLI command lists all ENIs?

### Answer

```bash
aws ec2 describe-network-interfaces
```

---

## Q20. Which AWS CLI command creates an ENI?

### Answer

```bash
aws ec2 create-network-interface
```

---

## Q21. Which AWS CLI command attaches an ENI?

### Answer

```bash
aws ec2 attach-network-interface
```

---

## Q22. Which AWS CLI command detaches an ENI?

### Answer

```bash
aws ec2 detach-network-interface
```

---

## Q23. Which AWS CLI command deletes an ENI?

### Answer

```bash
aws ec2 delete-network-interface
```

---

## Q24. Can multiple ENIs be attached to an EC2 instance?

### Answer

Yes.

The maximum number depends on the EC2 instance type.

---

## Q25. How do you identify the ENIs attached to an EC2 instance?

### Answer

You can check the **Networking** section of the EC2 Console or use:

```bash
aws ec2 describe-network-interfaces
```

---

# Production Scenario Questions

## Q26. Why would you use a Secondary ENI in production?

### Answer

Secondary ENIs are commonly used for:

- High Availability
- Failover
- Multi-homed applications
- Network appliances
- Separate application traffic

---

## Q27. Your EC2 instance failed. How can ENI help reduce downtime?

### Answer

Detach the Secondary ENI from the failed instance and attach it to a healthy EC2 instance in the same Availability Zone.

This preserves network configuration and reduces downtime.

---

## Q28. Can moving an ENI help during server migration?

### Answer

Yes.

Moving a Secondary ENI transfers its private IPs, security groups, and associated Elastic IPs, making migration faster.

---

## Q29. A Secondary ENI cannot be attached to another EC2 instance. What will you check?

### Answer

- Same Availability Zone?
- Compatible instance type?
- ENI already attached?
- EC2 instance running?
- ENI attachment limits reached?

---

## Q30. Why is your EC2 instance not reachable even though the ENI is attached?

### Answer

Check:

- Security Groups
- Route Table
- Internet Gateway
- Network ACL
- Public/Elastic IP
- Application status
- Listening ports

---

# Troubleshooting Questions

## Q31. How do you verify the Private IP address of an ENI?

### Answer

Check the EC2 Console or use:

```bash
aws ec2 describe-network-interfaces
```

---

## Q32. Can an ENI exist without an EC2 instance?

### Answer

Yes.

A detached Secondary ENI can exist independently until it is attached or deleted.

---

## Q33. Can you delete an ENI that is attached to an EC2 instance?

### Answer

No.

It must first be detached (if it is a Secondary ENI).

---

## Q34. What happens if you delete an EC2 instance?

### Answer

The Primary ENI is deleted automatically.

Secondary ENIs remain if they are configured to persist.

---

# Rapid Fire Questions & Answers

### Q35. What does ENI stand for?

**Answer:** Elastic Network Interface.

---

### Q36. Is ENI a virtual network card?

**Answer:** Yes.

---

### Q37. Can the Primary ENI be detached?

**Answer:** No.

---

### Q38. Can the Secondary ENI be detached?

**Answer:** Yes.

---

### Q39. Can an ENI have multiple Private IPs?

**Answer:** Yes.

---

### Q40. Can an Elastic IP be associated with an ENI?

**Answer:** Yes.

---

### Q41. Are Security Groups attached to an ENI?

**Answer:** Yes.

---

### Q42. Is an ENI Availability Zone specific?

**Answer:** Yes.

---

### Q43. Can an ENI be moved between Regions?

**Answer:** No.

---

### Q44. Does every EC2 instance have a Primary ENI?

**Answer:** Yes.

---

### Q45. What determines how many ENIs an EC2 instance can have?

**Answer:** The EC2 instance type.

---

# Interview Tips

- Remember that **every EC2 instance has a Primary ENI**.
- The **Primary ENI cannot be detached**, while Secondary ENIs can.
- Security Groups are associated with the **ENI**, not directly with the EC2 instance.
- Elastic IPs are associated with the **ENI**.
- Secondary ENIs are commonly used for high availability, failover, and advanced networking scenarios.
- Always mention that ENIs are **Availability Zone specific**.
- In production troubleshooting, verify the ENI, Security Groups, Route Table, Network ACL, Internet Gateway, and application status together rather than checking only one component.
