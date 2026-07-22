# Module 2 – Identity and Access Management (IAM)

> **Phase:** 1 – AWS Foundations  
> **Module:** 02 – Identity and Access Management (IAM)  
> **Repository:** DBA-Mastery  
> **Author:** Srikanth Puchakayala  
> **Version:** 1.0  
> **Last Updated:** July 2026  
> **Status:** 🚧 In Progress

---

# Table of Contents

1. Objective
2. Learning Outcomes
3. Prerequisites
4. What is IAM?
5. Why IAM?
6. Authentication vs Authorization
7. IAM Components
8. Root User
9. IAM Users
10. IAM Groups
11. IAM Roles
12. IAM Policies
13. Summary
14. Next Module

---

# Objective

The objective of this module is to understand how AWS controls access to resources using Identity and Access Management (IAM).

IAM is one of the first services that every AWS Administrator, Cloud Engineer, DevOps Engineer, Data Engineer, and Database Administrator must master because it controls **who can access AWS resources and what actions they are allowed to perform**.

---

# Learning Outcomes

After completing this module, you will be able to:

- Explain IAM
- Explain Authentication
- Explain Authorization
- Create IAM Users
- Create IAM Groups
- Create IAM Roles
- Understand IAM Policies
- Apply the Principle of Least Privilege
- Configure MFA
- Secure an AWS Account

---

# Prerequisites

Before starting this module, complete:

- Phase 0 – Environment Setup
- Module 1 – AWS Global Infrastructure
- AWS Account
- AWS CLI Configured

---

# What is IAM?

IAM (Identity and Access Management) is the AWS service used to securely control access to AWS resources.

IAM answers two important questions:

1. **Who is making the request?**
2. **What are they allowed to do?**

Without IAM, anyone with access to an AWS account could create, modify, or delete cloud resources.

IAM provides centralized access management for all AWS services.

---

# Why IAM?

Imagine a company with:

- 500 Employees
- 150 Developers
- 40 Database Administrators
- 80 DevOps Engineers
- 20 Security Engineers

Not everyone should have full administrative access.

Examples:

A DBA should manage databases but not billing.

A Developer should deploy applications but not delete production databases.

A Finance user should access billing but not EC2 instances.

IAM makes this possible.

---

# Authentication vs Authorization

## Authentication

Authentication verifies **who you are**.

Examples:

- Username and Password
- Access Keys
- Multi-Factor Authentication (MFA)
- Temporary Credentials

Example:

```
Username:
srikanth

Password:
********
```

AWS confirms your identity.

---

## Authorization

Authorization determines **what you are allowed to do** after authentication.

Example:

User:

```
Srikanth
```

Allowed:

✅ Launch EC2

✅ Read S3

✅ Create RDS Snapshots

Not Allowed:

❌ Delete IAM Users

❌ Modify Billing

❌ Delete Production Databases

Authorization is controlled using IAM Policies.

---

# IAM Components

IAM consists of several components:

- Root User
- IAM Users
- IAM Groups
- IAM Roles
- IAM Policies
- MFA
- Identity Providers
- Access Keys

Each component plays a different role in securing AWS resources.

---

# Root User

The Root User is created automatically when an AWS account is created.

Characteristics:

- Has unrestricted access to every AWS service.
- Cannot be restricted using IAM policies.
- Used only for account-level tasks.

Examples of Root-only tasks:

- Close AWS account
- Change support plan
- Modify account settings
- Configure payment methods

### Best Practices

- Do **not** use the Root User for daily work.
- Enable Multi-Factor Authentication (MFA).
- Store credentials securely.
- Create IAM users for administrators.

---

# IAM Users

An IAM User represents an individual person or application that requires access to AWS resources.

Examples:

| User | Role |
|------|------|
| Srikanth | Database Administrator |
| John | DevOps Engineer |
| Alice | Cloud Architect |

Each IAM User has unique credentials and permissions.

---

# IAM Groups

An IAM Group is a collection of IAM Users.

Instead of assigning permissions individually, permissions are assigned to the group.

Example:

```
DBA Team
```

Members:

- Srikanth
- Ravi
- Priya

Policy:

```
AmazonRDSFullAccess
```

All users in the group inherit the group's permissions.

Benefits:

- Easier administration
- Consistent permissions
- Reduced management effort

---

# IAM Roles

An IAM Role provides temporary permissions.

Unlike IAM Users, roles do not have permanent usernames or passwords.

Common use cases:

- EC2 accessing S3
- Lambda accessing DynamoDB
- RDS exporting backups to S3
- Cross-account access

Roles are assumed by trusted entities when needed.

---

# IAM Policies

Policies define permissions in AWS.

Policies answer questions such as:

- Can this user start an EC2 instance?
- Can this role read objects from S3?
- Can this group create RDS snapshots?

Policies are written in JSON.

Example:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:ListBucket",
      "Resource": "*"
    }
  ]
}
```

Policies specify:

- Effect (Allow or Deny)
- Actions
- Resources
- Conditions (optional)

---

# Summary

In this section, you learned:

- What IAM is
- Why IAM is important
- Authentication vs Authorization
- Root User
- IAM Users
- IAM Groups
- IAM Roles
- IAM Policies

These concepts form the foundation of AWS security and are essential before creating users, assigning permissions, and securing production environments.

---

# Next Section

In Part 2, we will cover:

- Managed Policies
- Customer Managed Policies
- Inline Policies
- Multi-Factor Authentication (MFA)
- Password Policies
- Access Keys
- AWS CLI Authentication
- IAM Best Practices
- Hands-on Labs
- AWS CLI Commands
- Enterprise DBA Scenarios
- Troubleshooting
- Interview Questions


---

# IAM Policies in Detail

IAM Policies are JSON documents that define **who can perform which actions on which AWS resources**.

A policy consists of one or more statements.

## Policy Structure

```json
{
  "Version": "2012-10-17",
  "Statement":[
      {
         "Effect":"Allow",
         "Action":"ec2:StartInstances",
         "Resource":"*"
      }
  ]
}
```

---

## Policy Elements

| Element | Description |
|----------|-------------|
| Version | Policy language version |
| Statement | One or more permission statements |
| Effect | Allow or Deny |
| Action | AWS API actions |
| Resource | AWS resource ARN |
| Condition | Optional restrictions |

---

# Types of IAM Policies

AWS supports three main policy types.

## 1. AWS Managed Policies

Created and maintained by AWS.

Examples:

- AdministratorAccess
- AmazonS3FullAccess
- AmazonEC2ReadOnlyAccess
- AmazonRDSFullAccess

Advantages

- Ready to use
- Updated automatically by AWS
- Suitable for common use cases

Disadvantages

- May provide more permissions than required.

---

## 2. Customer Managed Policies

Created by your organization.

Advantages

- Fully customizable
- Reusable
- Supports least privilege

Example

A DBA policy allowing:

- Start RDS
- Stop RDS
- Create Snapshots

but preventing:

- Delete Database

---

## 3. Inline Policies

Inline policies are attached directly to a single User, Group or Role.

Characteristics

- One-to-one relationship
- Cannot be reused
- Deleted automatically when the identity is deleted

Use Case

Temporary permissions for a specific user.

---

# IAM Users vs IAM Roles

| IAM User | IAM Role |
|----------|----------|
| Permanent identity | Temporary identity |
| Username & Password | No permanent credentials |
| Access Keys | Temporary credentials |
| Used by people | Used by AWS services & applications |

---

# Multi-Factor Authentication (MFA)

## What is MFA?

MFA adds an additional security layer.

Instead of only:

```
Username

Password
```

AWS also asks for

```
6-digit verification code
```

generated from:

- Google Authenticator
- Microsoft Authenticator
- Authy
- Hardware Security Key

---

## Why MFA?

Even if someone steals your password,

they cannot log in without the second authentication factor.

---

## Best Practice

Always enable MFA for:

- Root User
- Administrator Users
- Production DBAs
- Security Administrators

---

# Password Policy

Organizations should enforce strong passwords.

Example Policy

Minimum Length

```
12 Characters
```

Require

- Uppercase
- Lowercase
- Numbers
- Special Characters

Password Expiry

```
90 Days
```

Prevent Password Reuse

```
Last 24 Passwords
```

---

# Access Keys

Access Keys allow programmatic access.

Used by:

- AWS CLI
- SDKs
- Terraform
- Python
- Automation Scripts

Components

```
Access Key ID

Secret Access Key
```

Example

```
AKIA****************

****************************
```

Never expose Secret Access Keys.

---

# Temporary Credentials

AWS recommends using temporary credentials whenever possible.

Generated by:

- IAM Roles
- AWS STS

Benefits

- Automatically expire
- More secure
- No long-term credentials

---

# Principle of Least Privilege

One of the most important AWS security principles.

Definition

Grant only the permissions required to perform a task.

Example

Instead of

```
AdministratorAccess
```

Use

```
Read S3

Create RDS Snapshot

View CloudWatch
```

Only.

---

# IAM Permission Evaluation

When a request reaches AWS

AWS evaluates

```
Authentication

↓

Policies

↓

Explicit Deny?

↓

Allow?

↓

Grant or Reject
```

Important Rule

```
Explicit Deny

always wins.
```

---

# IAM Best Practices

✔ Never use Root User

✔ Enable MFA

✔ Rotate Access Keys

✔ Delete unused users

✔ Remove unused permissions

✔ Use Groups

✔ Use Roles

✔ Enable CloudTrail

✔ Monitor IAM activity

✔ Review permissions regularly

---

# AWS CLI Commands

Current User

```bash
aws iam get-user
```

List Users

```bash
aws iam list-users
```

List Groups

```bash
aws iam list-groups
```

List Roles

```bash
aws iam list-roles
```

List Policies

```bash
aws iam list-policies --scope AWS
```

Show Current Identity

```bash
aws sts get-caller-identity
```

---

# Hands-on Lab

## Lab 1

Create a new IAM User

```
dba-admin
```

Grant

```
AdministratorAccess
```

Enable

```
MFA
```

Login using IAM User.

---

## Lab 2

Create

```
DBA-Team
```

Group.

Add

```
dba-admin
```

Assign

```
AmazonRDSFullAccess
```

---

## Lab 3

Create Custom Policy

Allow

```
Start RDS

Stop RDS

Create Snapshot
```

Deny

```
Delete Database
```

---

# Common Mistakes

❌ Using Root User

❌ Sharing Access Keys

❌ Giving AdministratorAccess to everyone

❌ No MFA

❌ Hardcoding credentials

❌ Never rotating keys

---

# Troubleshooting

## Problem

Access Denied

Example

```
AccessDeniedException
```

Possible Causes

- Missing IAM Permission
- Wrong Role
- SCP Restriction
- Explicit Deny

Resolution

- Review IAM Policy
- Check Group Membership
- Verify Role
- Use IAM Policy Simulator

---

# DBA Production Scenario

A production Oracle DBA needs to

- Restart RDS
- Create Snapshots
- View CloudWatch
- Read S3 Backups

The DBA must NOT

- Delete IAM Users
- Change Billing
- Modify VPC
- Close AWS Account

Using IAM

A custom policy is created granting only the required permissions.

This follows the Principle of Least Privilege.

---

# Interview Questions

1. What is IAM?

2. Why is IAM important?

3. Difference between Authentication and Authorization?

4. Difference between IAM User and IAM Role?

5. What is an IAM Group?

6. What is an IAM Policy?

7. Types of IAM Policies?

8. Difference between Managed and Inline Policies?

9. What is MFA?

10. Why should Root User not be used?

11. What are Access Keys?

12. What is STS?

13. What is Least Privilege?

14. What is Explicit Deny?

15. How are IAM permissions evaluated?

16. How do you secure AWS accounts?

17. How would you design IAM for a production company?

18. How do you rotate Access Keys?

19. What AWS services use IAM?

20. Explain IAM from a DBA perspective.

---

# Module Summary

Congratulations!

You now understand

- IAM
- Authentication
- Authorization
- Users
- Groups
- Roles
- Policies
- MFA
- Password Policies
- Access Keys
- Temporary Credentials
- Least Privilege
- AWS CLI
- IAM Security Best Practices

IAM is the foundation of AWS security.

Every AWS service—including EC2, RDS, S3, Lambda, CloudWatch, and VPC—relies on IAM to control access securely.

---

# Next Module

➡ Module 3 – Amazon VPC (Virtual Private Cloud)

Location

```
02-AWS/03-VPC/README.md
```

Next Topics

- What is Networking?
- VPC
- CIDR
- Subnets
- Route Tables
- Internet Gateway
- NAT Gateway
- Security Groups
- Network ACLs
- VPC Peering
- Transit Gateway
- Enterprise Network Design



# Lab 01 – IAM Users and Groups

> **Phase:** 1 – AWS Foundations  
> **Module:** 02 – Identity and Access Management (IAM)  
> **Lab:** 01 – IAM Users and Groups  
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
6. Step 1 – Verify Current Identity
7. Step 2 – List Existing Users
8. Step 3 – Create IAM User
9. Step 4 – Verify IAM User
10. Step 5 – Create IAM Group
11. Step 6 – Add User to Group
12. Step 7 – Attach Managed Policy
13. Step 8 – Verify Policy
14. AWS CLI Commands Used
15. What I Learned
16. Troubleshooting
17. Best Practices
18. Cleanup
19. Interview Questions
20. Lab Summary

---

# Objective

The purpose of this lab is to understand how AWS Identity and Access Management (IAM) controls access to AWS resources.

By completing this lab, I learned how to:

- Create IAM Users
- Create IAM Groups
- Add Users to Groups
- Attach AWS Managed Policies
- Verify IAM configuration using AWS CLI
- Apply Role-Based Access Control (RBAC)

---

# Prerequisites

Before performing this lab:

- AWS Account
- IAM Administrator User (`dba-admin`)
- AWS CLI Installed
- AWS CLI Configured
- Internet Connection

---

# Business Scenario

A company has multiple database administrators.

Instead of assigning permissions individually, the organization creates a dedicated group called:

```
DBA-Team
```

Every DBA joins this group and automatically receives the required permissions.

This approach simplifies administration and follows enterprise security practices.

---

# Architecture

```
                    AWS Account
                         │
                  IAM Administrator
                    (dba-admin)
                         │
          ┌──────────────┴──────────────┐
          │                             │
     IAM Group                    Managed Policy
     DBA-Team             AmazonRDSFullAccess
          │
          │
      IAM User
    junior-dba
```

---

# Lab Overview

Resources created during this lab:

| Resource | Name |
|----------|------|
| IAM User | junior-dba |
| IAM Group | DBA-Team |
| Managed Policy | AmazonRDSFullAccess |

---

# Step 1 – Verify Current Identity

Command:

```bash
aws sts get-caller-identity
```

Purpose:

Verify the AWS account and IAM user currently authenticated.

Expected Result:

```
IAM User:
dba-admin
```

---

# Step 2 – List Existing Users

Command:

```bash
aws iam list-users
```

Purpose:

Display all IAM users in the AWS account.

---

# Step 3 – Create IAM User

Command:

```bash
aws iam create-user \
    --user-name junior-dba
```

Purpose:

Create a new IAM user that will represent a junior database administrator.

---

# Step 4 – Verify IAM User

Command:

```bash
aws iam get-user \
    --user-name junior-dba
```

Purpose:

Confirm that the user was created successfully.

---

# Step 5 – Create IAM Group

Command:

```bash
aws iam create-group \
    --group-name DBA-Team
```

Purpose:

Create a logical group for database administrators.

---

# Step 6 – Add User to Group

Command:

```bash
aws iam add-user-to-group \
    --group-name DBA-Team \
    --user-name junior-dba
```

Purpose:

Assign the IAM user to the DBA-Team group.

---

# Step 7 – Attach AWS Managed Policy

Command:

```bash
aws iam attach-group-policy \
    --group-name DBA-Team \
    --policy-arn arn:aws:iam::aws:policy/AmazonRDSFullAccess
```

Purpose:

Grant Amazon RDS administrative permissions to all members of the DBA-Team group.

---

# Step 8 – Verify Attached Policy

Command:

```bash
aws iam list-attached-group-policies \
    --group-name DBA-Team
```

Purpose:

Confirm that the policy has been successfully attached.

---

# AWS CLI Commands Used

```bash
aws sts get-caller-identity

aws iam list-users

aws iam create-user --user-name junior-dba

aws iam get-user --user-name junior-dba

aws iam create-group --group-name DBA-Team

aws iam add-user-to-group \
    --group-name DBA-Team \
    --user-name junior-dba

aws iam attach-group-policy \
    --group-name DBA-Team \
    --policy-arn arn:aws:iam::aws:policy/AmazonRDSFullAccess

aws iam list-attached-group-policies \
    --group-name DBA-Team

aws iam list-groups-for-user \
    --user-name junior-dba
```

---

# What I Learned

This lab helped me understand:

- IAM User Management
- IAM Group Management
- Group-based Permission Assignment
- AWS Managed Policies
- Role-Based Access Control (RBAC)
- Permission Inheritance
- AWS CLI for IAM Administration

---

# Troubleshooting

## Issue

```
AccessDenied
```

### Possible Causes

- Missing IAM permissions
- Incorrect policy attached
- Wrong IAM user
- Incorrect AWS CLI profile

### Resolution

Verify the authenticated user:

```bash
aws sts get-caller-identity
```

List attached policies:

```bash
aws iam list-attached-group-policies \
--group-name DBA-Team
```

---

# Best Practices

- Never use the Root User for daily administration.
- Use IAM Groups instead of assigning permissions directly to users.
- Follow the Principle of Least Privilege.
- Enable Multi-Factor Authentication (MFA).
- Regularly review IAM permissions.
- Rotate Access Keys periodically.

---

# Cleanup

If the lab resources are no longer required:

Remove the policy:

```bash
aws iam detach-group-policy \
--group-name DBA-Team \
--policy-arn arn:aws:iam::aws:policy/AmazonRDSFullAccess
```

Remove the user from the group:

```bash
aws iam remove-user-from-group \
--group-name DBA-Team \
--user-name junior-dba
```

Delete the user:

```bash
aws iam delete-user \
--user-name junior-dba
```

Delete the group:

```bash
aws iam delete-group \
--group-name DBA-Team
```

---

# Interview Questions

1. What is IAM?
2. What is an IAM User?
3. What is an IAM Group?
4. Why should Groups be used instead of assigning permissions directly?
5. What is a Managed Policy?
6. What is the Principle of Least Privilege?
7. What is Role-Based Access Control (RBAC)?
8. How do you verify the current AWS identity?
9. How do you attach a policy to a group?
10. Why is IAM important for AWS DBAs?

---

# Lab Summary

In this lab, I successfully:

- Created an IAM User (`junior-dba`)
- Created an IAM Group (`DBA-Team`)
- Added the user to the group
- Attached the `AmazonRDSFullAccess` managed policy
- Verified permissions using the AWS CLI
- Practiced enterprise IAM administration concepts

This lab provided hands-on experience with AWS IAM fundamentals and demonstrated how organizations manage access using users, groups, and policies.