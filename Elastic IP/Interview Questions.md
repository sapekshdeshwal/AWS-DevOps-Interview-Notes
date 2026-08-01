# AWS Elastic IP - Interview Questions

This document contains frequently asked AWS Elastic IP interview questions, including basic concepts, production scenarios, troubleshooting, and rapid-fire questions.

---

# Basic Interview Questions

## Q1. What is an Elastic IP?

### Answer

An Elastic IP (EIP) is a **static public IPv4 address** provided by AWS that can be associated with an EC2 instance or an Elastic Network Interface (ENI).

Unlike a normal public IP, an Elastic IP remains the same until it is released.

---

## Q2. Why do we need an Elastic IP?

### Answer

Elastic IP provides a permanent public IP address for an EC2 instance.

It prevents IP changes when an EC2 instance is stopped and started, making it ideal for production applications.

---

## Q3. What problem does Elastic IP solve?

### Answer

By default, the public IP of an EC2 instance changes after stopping and starting the instance.

Elastic IP provides a static public IP, eliminating the need to update DNS records or application configurations.

---

## Q4. Is an Elastic IP static or dynamic?

### Answer

Elastic IP is a **static public IPv4 address**.

---

## Q5. What is the difference between a Public IP and an Elastic IP?

| Public IP | Elastic IP |
|------------|------------|
| Dynamic | Static |
| Changes after Stop/Start | Remains the same |
| Automatically Assigned | Manually Allocated |
| Temporary | Persistent |

---

## Q6. Can an Elastic IP be associated with any EC2 instance?

### Answer

Yes, provided the EC2 instance is in the same AWS Region.

---

## Q7. Can an Elastic IP be moved from one EC2 instance to another?

### Answer

Yes.

Elastic IPs can be disassociated from one EC2 instance and associated with another, making them useful during server migration or failover.

---

## Q8. Is an Elastic IP Region-specific?

### Answer

Yes.

An Elastic IP can only be used within the AWS Region where it was allocated.

---

## Q9. Can one EC2 instance have multiple Elastic IPs?

### Answer

Yes.

If the instance has multiple network interfaces or secondary private IPs, multiple Elastic IPs can be associated.

---

## Q10. Can an Elastic IP be associated with an ENI?

### Answer

Yes.

An Elastic IP can be associated directly with an Elastic Network Interface (ENI).

---

# AWS Practical Questions

## Q11. What are the steps to use an Elastic IP?

### Answer

1. Allocate an Elastic IP.
2. Associate it with an EC2 instance or ENI.
3. Access the resource using the Elastic IP.

---

## Q12. What happens when you stop and start an EC2 instance with an Elastic IP?

### Answer

The Elastic IP remains associated with the instance.

The public IP does not change.

---

## Q13. What happens when you stop and start an EC2 instance without an Elastic IP?

### Answer

The default public IP may change after the instance starts again.

---

## Q14. What happens if you disassociate an Elastic IP?

### Answer

The Elastic IP is detached from the EC2 instance but remains allocated to your AWS account.

It can later be associated with another resource.

---

## Q15. What happens if you release an Elastic IP?

### Answer

The Elastic IP is permanently returned to AWS and cannot be recovered.

---

# Cost & Billing Questions

## Q16. Is Elastic IP free?

### Answer

AWS allows limited free usage under certain conditions.

However, AWS charges for:

- Unused Elastic IPs
- Idle Elastic IPs
- Additional Elastic IPs beyond service limits

Always release unused Elastic IPs to avoid unnecessary charges.

---

## Q17. Why does AWS charge for unused Elastic IPs?

### Answer

Public IPv4 addresses are a limited resource.

Charging encourages customers to release unused Elastic IPs.

---

# Production Questions

## Q18. Why is Elastic IP recommended for production servers?

### Answer

Because it provides a static public IP address, ensuring consistent connectivity for users, DNS records, APIs, and external integrations.

---

## Q19. How can Elastic IP help during server migration?

### Answer

Instead of updating DNS records, the Elastic IP can simply be moved from the old EC2 instance to the new one, reducing downtime.

---

## Q20. Can Elastic IP improve High Availability?

### Answer

Yes.

During instance failure, the Elastic IP can be reassociated with a healthy EC2 instance, helping restore service quickly.

---

# Scenario-Based Questions

## Q21. Your website became inaccessible after restarting the EC2 instance. What could be the reason?

### Answer

The instance was using a dynamic public IP instead of an Elastic IP.

Stopping and starting the instance changed its public IP.

---

## Q22. Your DNS record points to an old IP address after replacing an EC2 instance. How would you fix it?

### Answer

Use an Elastic IP and associate it with the new EC2 instance.

This avoids changing the DNS record.

---

## Q23. An Elastic IP is allocated but the website is still inaccessible. What will you check?

### Answer

- Is the Elastic IP associated with the correct EC2 instance?
- Is the Security Group allowing HTTP/HTTPS?
- Is the web server running?
- Is the application listening on the correct port?
- Is the route table and Internet Gateway configured correctly?

---

## Q24. Your company wants to replace a production server with minimal downtime. What would you recommend?

### Answer

Deploy the new server, test it, and then move the Elastic IP from the old server to the new one.

---

## Q25. You notice charges for an Elastic IP that is not attached to any EC2 instance. What should you do?

### Answer

Release the unused Elastic IP if it is no longer required.

---

# Troubleshooting Questions

## Q26. How do you verify the public IP of an EC2 instance?

### Answer

Check the EC2 Console or run:

```bash
curl ifconfig.me
```

---

## Q27. Can you SSH using an Elastic IP?

### Answer

Yes.

Example:

```bash
ssh -i key.pem ubuntu@<Elastic-IP>
```

---

## Q28. Can an Elastic IP be associated with a stopped EC2 instance?

### Answer

Yes.

The association can exist, and the Elastic IP remains reserved for that instance.

---

## Q29. Does Elastic IP work with private subnets?

### Answer

No.

An Elastic IP is intended for internet-facing resources and is typically associated with instances that have internet connectivity.

---

## Q30. What AWS CLI command is used to allocate an Elastic IP?

### Answer

```bash
aws ec2 allocate-address --domain vpc
```

---

# Rapid Fire Questions & Answers

### Q31. Is Elastic IP static?

**Answer:** Yes.

---

### Q32. Is Elastic IP public or private?

**Answer:** Public IPv4 Address.

---

### Q33. Can Elastic IP change after reboot?

**Answer:** No.

---

### Q34. Can Elastic IP be moved between EC2 instances?

**Answer:** Yes.

---

### Q35. Is Elastic IP Region-specific?

**Answer:** Yes.

---

### Q36. Can Elastic IP be attached to an ENI?

**Answer:** Yes.

---

### Q37. Does Elastic IP work inside a private subnet without internet connectivity?

**Answer:** No.

---

### Q38. Can unused Elastic IPs incur charges?

**Answer:** Yes.

---

### Q39. What happens if you release an Elastic IP?

**Answer:** It is permanently returned to AWS.

---

### Q40. What is the main purpose of an Elastic IP?

**Answer:** To provide a static public IP address for AWS resources.

---

# Interview Tips

- Remember that an Elastic IP is a **static public IPv4 address**.
- Do not confuse Elastic IP with the default public IP assigned to an EC2 instance.
- Explain the complete workflow: **Allocate → Associate → Use → Disassociate → Release**.
- Mention that Elastic IPs are **Region-specific**.
- Highlight that Elastic IPs help reduce downtime during server migration and failover.
- Mention that AWS charges for unused Elastic IPs.
- Use production scenarios to explain why Elastic IPs are important.
