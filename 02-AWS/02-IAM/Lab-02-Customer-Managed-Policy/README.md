# Lab 02 – Customer Managed IAM Policy

> **Phase:** 1 – AWS Foundations  
> **Module:** 02 – Identity and Access Management (IAM)  
> **Lab:** 02 – Customer Managed IAM Policy  
> **Repository:** DBA-Mastery  
> **Author:** Srikanth Puchakayala  
> **Date:** July 2026  
> **Status:** ✅ Completed

---

# Table of Contents

1. Objective
2. Prerequisites
3. Business Scenario
4. Architecture
5. Lab Overview
6. Understanding Customer Managed Policies
7. Step 1 – Create Policy JSON
8. Step 2 – Validate JSON
9. Step 3 – Create IAM Policy
10. Step 4 – Attach Policy to Group
11. Step 5 – Verify Policy
12. AWS CLI Commands Used
13. Policy Explanation
14. What I Learned
15. Troubleshooting
16. Best Practices
17. Cleanup
18. Interview Questions
19. Lab Summary

---

# Objective

The objective of this lab is to learn how to create and manage **Customer Managed IAM Policies** in AWS.

Unlike AWS Managed Policies, Customer Managed Policies are created and maintained by the organization. They allow administrators to implement the **Principle of Least Privilege** by granting only the permissions required for a specific role.

---

# Prerequisites

Before starting this lab:

- AWS Account
- IAM Administrator User (`dba-admin`)
- AWS CLI Configured
- Lab 01 – IAM Users & Groups Completed
- IAM Group (`DBA-Team`) Created

---

# Business Scenario

A financial organization has multiple levels of Database Administrators.

Junior DBAs should be able to:

- View Amazon RDS resources
- View database information
- Create database snapshots

Junior DBAs should **not** be allowed to:

- Delete production databases
- Delete database snapshots
- Perform administrative IAM tasks

To meet this requirement, a **Customer Managed IAM Policy** is created.

---

# Architecture

```
                     AWS Account
                          │
                     IAM Administrator
                       (dba-admin)
                          │
              ┌───────────┴───────────┐
              │                       │
        IAM Group                 Customer Policy
         DBA-Team              JuniorDBAPolicy
              │                       │
              └───────────┬───────────┘
                          │
                     IAM User
                    junior-dba
```

---

# Lab Overview

Resources Used

| Resource | Name |
|----------|------|
| IAM Group | DBA-Team |
| IAM User | junior-dba |
| IAM Policy | JuniorDBAPolicy |

---

# Understanding Customer Managed Policies

Customer Managed Policies are IAM policies created by an organization to meet specific security and operational requirements.

Advantages:

- Custom permissions
- Reusable
- Version controlled
- Supports Least Privilege
- Easier auditing

Unlike AWS Managed Policies, these policies are fully controlled by the organization.

---

# Step 1 – Create the Policy JSON

File:

```
policy/junior-dba-policy.json
```

Policy Features:

- Allow viewing Amazon RDS resources
- Allow creating RDS snapshots
- Explicitly deny deleting databases
- Explicitly deny deleting snapshots

---

# Step 2 – Validate the JSON

Command:

```bash
python -m json.tool \
02-AWS/02-IAM/Lab-02-Customer-Managed-Policy/policy/junior-dba-policy.json
```

Purpose:

Validate that the IAM policy document is valid JSON before uploading it to AWS.

---

# Step 3 – Create the IAM Policy

Command:

```bash
aws iam create-policy \
--policy-name JuniorDBAPolicy \
--policy-document file://02-AWS/02-IAM/Lab-02-Customer-Managed-Policy/policy/junior-dba-policy.json
```

Purpose:

Upload the custom IAM policy into AWS.

Result:

A Customer Managed Policy named:

```
JuniorDBAPolicy
```

was successfully created.

---

# Step 4 – Attach Policy to IAM Group

Command:

```bash
aws iam attach-group-policy \
--group-name DBA-Team \
--policy-arn arn:aws:iam::<ACCOUNT_ID>:policy/JuniorDBAPolicy
```

Purpose:

Assign the custom permissions to every member of the DBA-Team group.

---

# Step 5 – Verify Attached Policies

Command:

```bash
aws iam list-attached-group-policies \
--group-name DBA-Team
```

Result:

```
AmazonRDSFullAccess

JuniorDBAPolicy
```

The custom policy is now attached successfully.

---

# AWS CLI Commands Used

```bash
python -m json.tool \
02-AWS/02-IAM/Lab-02-Customer-Managed-Policy/policy/junior-dba-policy.json

aws iam create-policy \
--policy-name JuniorDBAPolicy \
--policy-document file://02-AWS/02-IAM/Lab-02-Customer-Managed-Policy/policy/junior-dba-policy.json

aws iam attach-group-policy \
--group-name DBA-Team \
--policy-arn arn:aws:iam::<ACCOUNT_ID>:policy/JuniorDBAPolicy

aws iam list-attached-group-policies \
--group-name DBA-Team

aws iam get-policy \
--policy-arn arn:aws:iam::<ACCOUNT_ID>:policy/JuniorDBAPolicy
```

---

# Policy Explanation

The policy grants the following permissions:

### Allowed

- Describe Amazon RDS resources
- View RDS information
- Create database snapshots

### Explicitly Denied

- Delete DB Instances
- Delete DB Snapshots

This demonstrates the Principle of Least Privilege by allowing only the required actions while preventing destructive operations.

---

# What I Learned

This lab helped me understand:

- Customer Managed Policies
- IAM Policy JSON structure
- Policy Statements
- Allow vs Deny
- Policy Validation
- Policy Attachment
- Group-based Permission Management
- AWS CLI IAM Administration

---

# Troubleshooting

## Problem

```
MalformedPolicyDocument
```

Cause:

Invalid JSON syntax.

Resolution:

Validate the policy document before uploading.

```bash
python -m json.tool policy/junior-dba-policy.json
```

---

## Problem

```
EntityAlreadyExists
```

Cause:

A policy with the same name already exists.

Resolution:

Choose a different policy name or delete the existing policy if appropriate.

---

## Problem

```
AccessDenied
```

Cause:

Current IAM user lacks permission to create or attach IAM policies.

Resolution:

Verify your current identity:

```bash
aws sts get-caller-identity
```

Ensure the administrator account or role has the required IAM permissions.

---

# Best Practices

- Follow the Principle of Least Privilege.
- Prefer Customer Managed Policies for production environments.
- Avoid using `AdministratorAccess` unless necessary.
- Use IAM Groups for assigning permissions.
- Review and audit policies regularly.
- Test policies in a non-production environment before deployment.

---

# Cleanup

If the resources are no longer required:

Detach the policy:

```bash
aws iam detach-group-policy \
--group-name DBA-Team \
--policy-arn arn:aws:iam::<ACCOUNT_ID>:policy/JuniorDBAPolicy
```

Delete the policy:

```bash
aws iam delete-policy \
--policy-arn arn:aws:iam::<ACCOUNT_ID>:policy/JuniorDBAPolicy
```

> **Note:** A policy must be detached from all users, groups, and roles before it can be deleted.

---

# Interview Questions

1. What is a Customer Managed IAM Policy?
2. How is it different from an AWS Managed Policy?
3. What is the Principle of Least Privilege?
4. Why would an organization create custom IAM policies?
5. What is the purpose of the `Effect` field in a policy?
6. What happens when an explicit `Deny` is present?
7. Why should policy JSON be validated before uploading?
8. How do you attach a policy to an IAM Group?
9. What is the difference between Users, Groups, and Roles?
10. How would you secure IAM permissions for junior DBAs?

---

# Lab Summary

In this lab, I successfully:

- Created a Customer Managed IAM Policy (`JuniorDBAPolicy`)
- Wrote a custom IAM policy in JSON
- Validated the policy using Python
- Uploaded the policy to AWS
- Attached the policy to the `DBA-Team` IAM Group
- Verified the policy assignment using the AWS CLI
- Applied the Principle of Least Privilege for database administration

This lab strengthened my understanding of AWS IAM security by demonstrating how organizations create custom permission models instead of relying solely on AWS Managed Policies.