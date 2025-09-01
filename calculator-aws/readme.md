<img width="300" height="185" alt="image" src="https://github.com/user-attachments/assets/9eadff17-094e-461f-b57b-1a35fcabe046" />


# Terraform Documentation: Static Module

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

The purpose of this static setup is to provide a simple and quick way to define and provision infrastructure using a single Terraform file (main.tf). It is mainly suited for small projects, demos, or learning scenarios, where the goal is to keep everything in one place for easier visibility. However, it lacks scalability and reusability, so it should not be used for production-grade infrastructure.

---
##  Structure

All Terraform configurations are written in a single file, typically named main.tf.


| Component             | Description                                                                                                       |
| --------------------- | ----------------------------------------------------------------------------------------------------------------- |
| **Provider Block**    | Defines the cloud provider configuration (e.g., AWS in this case).                                                |
| **Resources**         | Contains all infrastructure resources such as EC2, S3, etc.                                                       |
| **No Separate Files** | Variables, outputs, and providers are all included inside `main.tf` instead of being split across multiple files. |


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

| Best Practice                                         | Why to Avoid Single File                |
| ------------------------------------------------------- | ------------------------------------------ |
| Keep for **small/demo projects only**                   | Not scalable for production.               |
| Use **separate copies** for each environment (dev/prod) | Risk of overwriting configs.               |
| Comment resources clearly                               | Hard to track changes in large files.      |
| Transition to **modular structure** when project grows  | Avoids maintenance overhead.               |
| Store code in **version control (Git)**                 | Single file makes collaboration difficult. |


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
