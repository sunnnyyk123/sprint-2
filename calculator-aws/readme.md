
<img width="300" height="168" alt="image" src="https://github.com/user-attachments/assets/4ed609c0-0d03-4296-9a1d-b578ba90bdb6" />


# AWS Pricing Calculator Documentation

## Author Information

| Last Updated On | Version | Author           | Level           | Reviewer               |
|-----------------|---------|-----------------|----------------|------------------------|
| 11-09-2025      | V1.0    | Sunny Kumar     | Internal Review | Aman Raj               |
|                 |         | Sunny Kumar     | L0             | Shikha Tripathi        |
|                 |         | Sunny Kumar     | L1             | Kirti Nehra            |
|                 |         | Sunny Kumar     | L2             | Ashwini Singh/Deepak Nishad |

---
## Table of Contents

1. [Introduction](#Introduction)
2. [What is AWS Pricing Calculator](#What-is-AWS-Pricing-Calculator)
3. [Why AWS Pricing Calculator](#Why-AWS-Pricing-Calculator)
4. [Step-by-Step Example: Estimating Costs for a Web Application](#Step-by-Step-Example-Estimating-Costs-for-a-Web-Application)
5. [Best Practices](#Best-Practices)
6. [Contact Information](#contact-information)
7. [References](#references)

---
## Introduction
This documentation serves as a guide to walk you through the AWS Pricing Calculator. It explains how to estimate costs, explore different AWS services, and customize pricing scenarios to plan your cloud expenses effectively.

---
## What is AWS Pricing Calculator

The AWS Pricing Calculator is a free tool to estimate your AWS infrastructure costs. It helps you model your cloud architecture, select services, and generate cost estimates based on your requirements.
It also provides detailed cost breakdowns, making it easier to forecast and manage your cloud expenses.

---
## Why AWS Pricing Calculator
| Benefit                 | Description                                                                  |
| ----------------------- | ---------------------------------------------------------------------------- |
| **Cost Estimation**     | Provides accurate cost predictions for AWS services before deployment.       |
| **Comparison**          | Lets you evaluate different service options and configurations side by side. |
| **Budget Optimization** | Helps you plan and control expenses to avoid unexpected charges.             |


---
## Step-by-Step Example: Estimating Costs for a Web Application

Scenario: Estimate costs for a simple web application using EC2 in the US East (Ohio) region.

### Start a New Estimate

- Go to calculator.aws. 
- Click "Create estimate" and name it "ex: WebApp_Cost_Estimate".
<img width="1297" height="428" alt="image" src="https://github.com/user-attachments/assets/700ec873-b090-469c-bfd5-b63be7518804" />


### Add EC2 Service
- Select "Amazon EC2" from the service list.
- Region: US East (Ohio).
- Instance Type: t2.large (2 vCPUs, 8 GiB RAM).
- Operating System: Linux.
- Usage: 100 hours/month (always on).
- Pricing Strategy: On-Demand.
<img width="1312" height="465" alt="image" src="https://github.com/user-attachments/assets/d4ad2751-7dbe-4787-b7f6-1248a59418ca" />
<img width="1312" height="465" alt="image" src="https://github.com/user-attachments/assets/220221ff-7aa4-4580-b9af-6aea46adb0d9" />
<img width="1312" height="465" alt="image" src="https://github.com/user-attachments/assets/fbe4a80d-8dfc-4161-86e3-1268cdb41018" />

### Review Estimate
- Check the summary for EC2 (t2.large).

<img width="1314" height="504" alt="image" src="https://github.com/user-attachments/assets/509ccd04-5828-461a-91f4-bad1252b6f72" />


### Export Estimate
- Click "Export" to download as CSV for stakeholder review.
here is the csv file:
<img width="1314" height="504" alt="image" src="https://github.com/user-attachments/assets/4cb34a8c-eff8-4a1f-bbf0-3d86118fc425" />


## Best Practices
| Best Practice                 | Description                                                                  |
| ----------------------------- | ---------------------------------------------------------------------------- |
| **Explore Pricing Options**   | Compare On-Demand, Reserved, or Spot instances for EC2 to find cost savings. |
| **Use Recommendations**       | Leverage AWS suggestions like Savings Plans for optimized pricing.           |
| **Check Regional Variations** | Costs differ across regions; test multiple regions for cheaper options.      |
| **Update Regularly**          | Revisit and update estimates as your architecture or AWS pricing changes.    |




##  Contact Information

| Name             | Email                                         |
|------------------|-----------------------------------------------|
| Sunny Kumar  | sunny.kumar.snaatak@mygurukulam.co        |

---


## References

| Resource                     | Link |
|-------------------------------|------|
| AWS Pricing Calculator           | [Visit](https://calculator.aws/#/) |
| Documentation of AWS Pricing Calculator           | [Visit](https://docs.aws.amazon.com/pricing-calculator/) |

---

---
