


# AWS Pricing Calculator Documentation

## Author Information

| Last Updated On | Version | Author           | Level           | Reviewer               |
|-----------------|---------|-----------------|----------------|------------------------|
| 29-08-2025      | V1.0    | Sunny Kumar     | Internal Review | Aman Raj               |
|                 |         | Sunny Kumar     | L0             | Shikha Tripathi        |
|                 |         | Sunny Kumar     | L1             | Kirti Nehra            |
|                 |         | Sunny Kumar     | L2             | Ashwini Singh/Deepak Nishad |

---
## Table of Contents

1. [Purpose](#Purpose)
2. [Module Structure](#Module-Structure)
3. [Environment-Specific-Values](#Environment-Specific-Values)
4. [Dependencies](#Dependencies)
5. [Best Practices](#Best-Practices)
6. [Contact Information](#contact-information)
7. [References](#references)

---

## Purpose

The AWS Pricing Calculator is a web-based tool that helps estimate the cost of using AWS services. It allows you to define resources like EC2 instances, S3 storage, RDS databases, and more, including their configurations, and then calculates the monthly estimated cost. This helps in planning budgets and comparing cost between different infrastructure options.

---
##  Structure

Estimate costs for multiple AWS services.

Customize resource configurations.

Compare different service configurations.

Export estimates in CSV or PDF for documentation and approval.

Understand pricing components like On-Demand, Reserved Instances, storage, and data transfer costs.


---
## Environment-Specific Values

Since everything is in one file, environment-specific values (like dev, staging, prod) are hardcoded.
If teams need to manage multiple environments, they must manually update values in main.tf, or use different copies of the same file for each environment (e.g., dev-main.tf, prod-main.tf).


| Value              | Example                   | Notes                                                                      |
| ------------------ | ------------------------- | -------------------------------------------------------------------------- |
| **Region**         | `ap-south-1`              | Defines the AWS region where resources will be created.                    |
| **Instance Type**  | `t2.micro`                | Can vary per environment (e.g., `t2.micro` for dev, `t3.medium` for prod). |
| **S3 Bucket Name** | `single-file-bucket-demo` | Must be unique across all AWS accounts; change per environment.            |




---
## Dependencies

- Terraform CLI (version ≥ 1.0.0).

- AWS credentials configured locally (via ~/.aws/credentials or environment variables).

- Internet access to reach AWS APIs.

>No additional dependencies are required since everything is contained in one file.

---
## Best Practices

Always select the correct region; pricing varies by region.

Include all resources: EC2, storage, database, network transfer.

Use Reserved Instances or Savings Plans for long-term workloads.

Regularly update estimates as your infrastructure grows.

---

##  Contact Information

| Name             | Email                                         |
|------------------|-----------------------------------------------|
| Sunny Kumar  | sunny.kumar.snaatak@mygurukulam.co        |

---


## References

| Resource                     | Link |
|-------------------------------|------|
| Module Documentation         | [Visit](https://developer.hashicorp.com/terraform/language?utm_source=chatgpt.com) |
| Basic module           | [Visit](https://registry.terraform.io/providers/hashicorp/aws/latest/docs?utm_source=chatgpt.com) |

---

---
