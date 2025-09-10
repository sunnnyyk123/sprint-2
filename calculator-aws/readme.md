


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
2. [How to Use the AWS Pricing Calculator](#How-to-Use-the-AWS-Pricing-Calculator)
3. [Step-by-Step Example: Estimating Costs for a Web Application](#Step-by-Step-Example:-Estimating-Costs-for-a-Web-Application)
4. [Best Practices](#Best-Practices)
5. [Contact Information](#contact-information)
6. [References](#references)

---

## Introduction

The AWS Pricing Calculator is a free tool to estimate your AWS infrastructure costs. It helps you model your cloud architecture, select services, and generate cost estimates based on your requirements. Below is a concise guide with a step-by-step example.

## How to Use the AWS Pricing Calculator

### Access the Calculator
- Visit AWS Pricing Calculator.
- No AWS account is required to start.

### Create a New Estimate
- Click "Create estimate" on the homepage.
- Name your estimate for easy reference (e.g., "WebApp_Infra").

### Add Services
- Click "Add service" to select AWS services (e.g., EC2, S3, RDS).
- Configure each service with details like region, instance type, storage, or usage patterns.

### Configure Service Details
- Specify parameters such as instance size, operating system, storage type, or data transfer.
- Use the tool’s suggestions for common configurations or input custom values.

### Review and Adjust
- View the cost breakdown in the estimate summary.
- Adjust configurations to optimize costs (e.g., reserved instances or Spot instances).

### Save or Export
- Save the estimate to share or revisit later (requires AWS account).
- Export as CSV or PDF for documentation.

### Analyze and Refine
- Compare costs across regions or configurations.
- Use the "Recommendations" feature for cost-saving suggestions.

## Step-by-Step Example: Estimating Costs for a Web Application

Scenario: Estimate costs for a simple web application using EC2 and S3 in the US East (N. Virginia) region.

### Start a New Estimate
- Go to calculator.aws.
- Click "Create estimate" and name it "WebApp_Cost_Estimate".

### Add EC2 Service
- Select "Amazon EC2" from the service list.
- Region: US East (N. Virginia).
- Instance Type: t3.micro (2 vCPUs, 1 GiB RAM).
- Operating System: Linux.
- Usage: 730 hours/month (always on).
- Pricing Strategy: On-Demand.

### Add S3 Service
- Select "Amazon S3".
- Region: US East (N. Virginia).
- Storage: 100 GB in Standard storage class.
- Data Transfer: 10 GB/month out to the internet.

### Review Estimate
- Check the summary for EC2 (~$8.50/month for t3.micro) and S3 (~$2.30/month for storage + transfer).
- Total estimated cost: ~$10.80/month.

### Export Estimate
- Click "Export" to download as CSV for stakeholder review.

## Best Practices
- Explore Pricing Options: Compare On-Demand, Reserved, or Spot instances for EC2 to reduce costs.
- Use Recommendations: Leverage AWS suggestions for cost optimization (e.g., Savings Plans).
- Check Regional Variations: Costs vary by region; test multiple regions.
- Update Regularly: Revisit estimates as your architecture or AWS pricing changes.

For more details, refer to the AWS Pricing Calculator User Guide.



##  Contact Information

| Name             | Email                                         |
|------------------|-----------------------------------------------|
| Sunny Kumar  | sunny.kumar.snaatak@mygurukulam.co        |

---


## References

| Resource                     | Link |
|-------------------------------|------|
| AWS Pricing Calculator  Documentation         | [Visit](https://developer.hashicorp.com/terraform/language?utm_source=chatgpt.com) |
| Basic module           | [Visit](https://registry.terraform.io/providers/hashicorp/aws/latest/docs?utm_source=chatgpt.com) |

---

---
