# Module 1 – AWS Global Infrastructure

> **Phase:** 1 – AWS Foundations  
> **Module:** 01 – AWS Global Infrastructure  
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
4. What is Computing?
5. Evolution of Computing
6. What is Cloud Computing?
7. Characteristics of Cloud Computing
8. Cloud Deployment Models
9. Cloud Service Models
10. What is AWS?
11. Why AWS?
12. AWS Global Infrastructure
13. Summary
14. Next Module

---

# Objective

The objective of this module is to build a solid understanding of AWS Global Infrastructure, the backbone of Amazon Web Services.

By the end of this module, you will understand:

- What cloud computing is
- Why organizations use AWS
- How AWS is structured globally
- Regions
- Availability Zones
- Edge Locations
- Local Zones
- Wavelength Zones
- AWS Global Backbone Network
- High Availability concepts
- Disaster Recovery basics

This knowledge is essential before learning IAM, EC2, VPC, Amazon RDS, Amazon Aurora, and other AWS services.

---

# Learning Outcomes

After completing this module, you will be able to:

✅ Explain Cloud Computing

✅ Explain AWS Architecture

✅ Explain AWS Global Infrastructure

✅ Differentiate Regions and Availability Zones

✅ Understand High Availability

✅ Explain Fault Tolerance

✅ Understand Disaster Recovery

✅ Identify the best AWS Region for deployment

---

# Prerequisites

Before starting this module, complete:

- Phase 0 – Environment Setup
- AWS Account Creation
- AWS CLI Configuration
- GitHub Repository Setup

---

# What is Computing?

Computing is the process of using computer hardware and software to perform operations such as:

- Processing data
- Running applications
- Storing information
- Communicating over networks
- Automating tasks

Examples:

- Banking systems
- Hospital management systems
- Social media platforms
- E-commerce websites
- Database servers

Traditionally, companies purchased their own servers, networking equipment, storage devices, and software licenses to build data centers.

This required significant capital investment, ongoing maintenance, power, cooling, and dedicated IT staff.

---

# Evolution of Computing

## Traditional Data Centers (On-Premises)

Organizations purchased:

- Physical Servers
- Storage Arrays
- Network Switches
- Firewalls
- Backup Devices
- Database Servers

Example Architecture

```
Users
   │
Internet
   │
Firewall
   │
Router
   │
Switch
   │
Servers
   │
Storage
```

Challenges:

- High upfront cost
- Hardware failures
- Capacity planning
- Long procurement cycles
- Disaster recovery complexity
- Maintenance overhead

---

## Virtualization

Virtualization introduced Hypervisors, allowing multiple virtual machines (VMs) to run on a single physical server.

Benefits:

- Better hardware utilization
- Reduced costs
- Faster provisioning
- Easier management

Popular Hypervisors:

- VMware ESXi
- Microsoft Hyper-V
- KVM

---

## Cloud Computing

Cloud computing allows organizations to rent computing resources over the internet instead of purchasing physical infrastructure.

Examples of cloud resources:

- Virtual Servers
- Storage
- Databases
- Networking
- AI Services
- Analytics
- Monitoring

You pay only for the resources you use.

---

# What is Cloud Computing?

Cloud computing is the on-demand delivery of computing resources over the internet with pay-as-you-go pricing.

Instead of buying servers, you can provision them in minutes.

Examples:

- Launch a Linux server
- Create a database
- Store files
- Run applications
- Analyze large datasets

All without owning physical hardware.

---

# Characteristics of Cloud Computing

The five essential characteristics are:

1. On-Demand Self-Service
2. Broad Network Access
3. Resource Pooling
4. Rapid Elasticity
5. Measured Service (Pay-as-you-go)

Example:

An e-commerce company receives heavy traffic during a festival sale.

Using cloud computing, it can automatically increase server capacity during peak hours and scale down afterward, paying only for the additional resources consumed.

---

# Cloud Deployment Models

## Public Cloud

Infrastructure is owned and managed by a cloud provider.

Examples:

- AWS
- Microsoft Azure
- Google Cloud Platform

Suitable for:

- Startups
- Small and Medium Businesses
- Most enterprise workloads

---

## Private Cloud

Infrastructure is dedicated to a single organization.

Examples:

- VMware Private Cloud
- OpenStack

Suitable for:

- Government
- Banking
- Healthcare
- Highly regulated industries

---

## Hybrid Cloud

Combines on-premises infrastructure with public cloud services.

Example:

- Sensitive databases remain on-premises.
- Web applications run in AWS.

---

## Multi-Cloud

Organizations use multiple cloud providers simultaneously.

Example:

- AWS for databases
- Azure for Active Directory
- Google Cloud for analytics

---

# Cloud Service Models

## Infrastructure as a Service (IaaS)

The provider manages the physical infrastructure.

You manage:

- Operating System
- Database
- Applications
- Security Configuration

AWS Examples:

- Amazon EC2
- Amazon EBS
- Amazon VPC

---

## Platform as a Service (PaaS)

The provider manages the operating system and runtime.

You focus on your application and data.

Examples:

- AWS Elastic Beanstalk
- AWS Lambda (serverless)
- AWS App Runner

---

## Software as a Service (SaaS)

Complete software delivered over the internet.

Examples:

- Gmail
- Microsoft 365
- Salesforce
- Dropbox

No infrastructure management is required by the customer.

---

# What is AWS?

Amazon Web Services (AWS) is the world's leading cloud computing platform.

It provides hundreds of cloud services for:

- Compute
- Storage
- Networking
- Databases
- Security
- Analytics
- Artificial Intelligence
- Machine Learning
- Monitoring
- DevOps

AWS launched in **2006** and today operates a global cloud infrastructure serving millions of customers.

---

# Why AWS?

Organizations choose AWS because it offers:

- High Availability
- Global Presence
- Scalability
- Security
- Reliability
- Pay-as-you-go Pricing
- Broad Service Portfolio
- Continuous Innovation

For DBAs, AWS provides managed database services such as:

- Amazon RDS
- Amazon Aurora
- Amazon DynamoDB
- Amazon Redshift

These services reduce operational overhead while improving scalability and availability.

---

# Summary

In this section, you learned:

- What computing is
- How computing evolved
- What cloud computing is
- Cloud deployment models
- Cloud service models
- What AWS is
- Why organizations use AWS

These concepts form the foundation for understanding AWS Global Infrastructure.

---

# Next Module Section

The next section of this document will cover:

- AWS Global Infrastructure
- AWS Regions
- Availability Zones
- Edge Locations
- Local Zones
- Wavelength Zones
- AWS Global Network

These topics are essential before learning IAM, EC2, and Amazon RDS.

---

# AWS Global Infrastructure

## Introduction

AWS Global Infrastructure is the worldwide network of physical data centers, networking equipment, edge locations, and cloud services that deliver AWS services to customers around the globe.

AWS has invested billions of dollars in building one of the largest and most reliable cloud infrastructures in the world.

Instead of operating from a single data center, AWS distributes its infrastructure across multiple geographic locations to provide:

- High Availability
- Low Latency
- Fault Tolerance
- Disaster Recovery
- Global Scalability

This infrastructure enables organizations to deploy applications closer to their users while maintaining high reliability and performance.

---

# Components of AWS Global Infrastructure

AWS Global Infrastructure consists of:

- Regions
- Availability Zones (AZs)
- Edge Locations
- Regional Edge Caches
- Local Zones
- Wavelength Zones
- Points of Presence (PoPs)
- AWS Global Backbone Network

Each component has a specific purpose and contributes to the reliability and performance of AWS services.

---

# AWS Global Infrastructure Architecture

```
                          AWS GLOBAL INFRASTRUCTURE

                                   Internet
                                       │
                ─────────────────────────────────────────
                          AWS Global Backbone Network
                ─────────────────────────────────────────

          ┌────────────────────┬────────────────────┐
          │                    │                    │
     Region (Mumbai)      Region (London)     Region (Virginia)
          │                    │                    │
     ┌────┴────┐          ┌────┴────┐         ┌────┴────┐
     │         │          │         │         │         │
    AZ-A      AZ-B       AZ-A      AZ-B      AZ-A     AZ-B
     │          │          │          │         │         │
 EC2 RDS     EC2 RDS    EC2 RDS    EC2 RDS  EC2 RDS  EC2 RDS

                  │
        Edge Locations Worldwide
```

---

# AWS Regions

## What is a Region?

An AWS Region is a **geographical location** where AWS operates one or more data centers.

Examples:

- Asia Pacific (Mumbai)
- Asia Pacific (Hyderabad)
- US East (N. Virginia)
- Europe (London)
- Europe (Frankfurt)
- Canada (Central)
- Australia (Sydney)

Each Region is isolated from every other Region.

---

## Why Regions?

Organizations select Regions based on:

- Customer proximity
- Legal compliance
- Data residency
- Disaster Recovery
- Service availability
- Cost

Example:

An Indian banking application may deploy in **Asia Pacific (Mumbai)** to reduce latency and satisfy regulatory requirements.

---

## Region Naming Convention

Example:

```
ap-south-1
```

Meaning:

```
ap       → Asia Pacific
south    → South Region
1        → Region Number
```

Examples:

```
us-east-1
us-east-2
eu-west-1
eu-central-1
ap-south-1
ap-southeast-1
```

---

# Availability Zones (AZ)

## What is an Availability Zone?

An Availability Zone (AZ) is one or more physically separate data centers within an AWS Region.

Each Availability Zone has:

- Independent power
- Independent cooling
- Independent networking
- Physical security

Yet all AZs in the same Region are connected using high-speed, low-latency private fiber networks.

---

## Example

```
Region: Mumbai (ap-south-1)

Availability Zone A

Availability Zone B

Availability Zone C
```

Applications can be distributed across multiple AZs to improve availability.

---

# Why Multiple Availability Zones?

If one data center fails because of:

- Power outage
- Flood
- Fire
- Hardware failure
- Network failure

the application continues running from another Availability Zone.

This design improves:

- Availability
- Reliability
- Fault tolerance

---

# Real DBA Example

Suppose you have an Amazon RDS MySQL database.

Primary Database:

```
Availability Zone A
```

Standby Database:

```
Availability Zone B
```

If AZ-A becomes unavailable, AWS automatically fails over to AZ-B.

The application continues running with minimal downtime.

This is known as **Multi-AZ Deployment**.

---

# Edge Locations

## What is an Edge Location?

Edge Locations are AWS sites used to cache content closer to users.

Primary service:

Amazon CloudFront

Instead of fetching data from a Region every time, frequently accessed content is cached at Edge Locations.

Benefits:

- Faster downloads
- Lower latency
- Reduced load on the origin server

---

## Example

User in Hyderabad requests an image.

Without CloudFront:

```
Hyderabad

↓

Mumbai Region

↓

Response
```

With CloudFront:

```
Hyderabad

↓

Nearby Edge Location

↓

Response
```

The response is significantly faster.

---

# Regional Edge Cache

Regional Edge Caches sit between CloudFront Edge Locations and AWS Regions.

Benefits:

- Larger cache capacity
- Improved performance
- Reduced origin requests

---

# Local Zones

## What are Local Zones?

Local Zones extend AWS infrastructure closer to large metropolitan areas.

Purpose:

Provide ultra-low latency for workloads such as:

- Gaming
- Video Editing
- Media Rendering
- Machine Learning
- Financial Trading

Example:

A Local Zone may exist closer to a city while the parent Region remains hundreds of kilometers away.

---

# Wavelength Zones

## What are Wavelength Zones?

AWS Wavelength integrates AWS infrastructure into 5G mobile networks.

Purpose:

Reduce latency for:

- Autonomous Vehicles
- IoT
- Smart Manufacturing
- AR/VR
- Mobile Gaming

Latency can be reduced to single-digit milliseconds.

---

# AWS Global Backbone Network

AWS owns one of the world's largest private fiber networks.

Benefits:

- Secure communication
- Low latency
- High bandwidth
- Reliable data transfer

Traffic between AWS Regions travels over the AWS private network instead of the public internet whenever possible.

This improves security and performance.

---

# Key Takeaways

| Component | Purpose |
|-----------|----------|
| Region | Geographic location |
| Availability Zone | Independent data centers within a Region |
| Edge Location | Content caching |
| Regional Edge Cache | Larger caching layer |
| Local Zone | Ultra-low latency workloads |
| Wavelength Zone | 5G integration |
| Backbone Network | Secure private AWS network |

---

# DBA Perspective

Understanding AWS Global Infrastructure helps Database Administrators:

- Select appropriate deployment Regions.
- Design highly available databases.
- Plan disaster recovery strategies.
- Reduce application latency.
- Optimize database performance.
- Meet regulatory compliance requirements.

When designing production database environments, always consider:

- Region selection
- Multi-AZ deployment
- Backup location
- Disaster Recovery Region
- Network latency
- Cost optimization

---

# Summary

In this section, you learned:

- AWS Global Infrastructure
- Regions
- Availability Zones
- Edge Locations
- Regional Edge Caches
- Local Zones
- Wavelength Zones
- AWS Backbone Network

These concepts are fundamental to understanding how AWS delivers reliable, scalable, and highly available cloud services.

---

# Next Section

In Part 3, we will cover:

- High Availability
- Fault Tolerance
- Disaster Recovery
- Multi-AZ Architecture
- Multi-Region Architecture
- AWS CLI Commands
- Hands-on Lab
- Enterprise DBA Scenarios
- Best Practices
- Interview Questions


---

# High Availability (HA)

## What is High Availability?

High Availability (HA) is the ability of a system to remain operational even if one or more components fail.

The primary goal of High Availability is to minimize downtime and ensure continuous access to applications and databases.

In AWS, High Availability is achieved by designing systems across multiple Availability Zones (AZs) within a Region.

---

## Why is High Availability Important?

Without High Availability:

- A single hardware failure can bring down an application.
- Database failures can interrupt business operations.
- Users may be unable to access critical services.

With High Availability:

- Applications continue running even during infrastructure failures.
- Downtime is minimized.
- Customer experience is improved.
- Business continuity is maintained.

---

## Example

Single Availability Zone Deployment:

```
            Region
              │
        ┌─────────────┐
        │ Availability│
        │ Zone A      │
        └─────────────┘
              │
         EC2 + Database
```

If Availability Zone A fails, the application becomes unavailable.

---

Multi-Availability Zone Deployment:

```
                    Region
                       │
        ┌──────────────┴──────────────┐
        │                             │
  Availability Zone A          Availability Zone B
        │                             │
     EC2 + RDS                 EC2 + Standby RDS
```

If one Availability Zone fails, the workload continues from the other Availability Zone.

---

# Fault Tolerance

## What is Fault Tolerance?

Fault Tolerance is the capability of a system to continue operating without interruption even when one or more components fail.

Unlike High Availability, which may involve a brief failover, Fault Tolerance is designed to eliminate service interruption.

---

## High Availability vs Fault Tolerance

| High Availability | Fault Tolerance |
|-------------------|-----------------|
| Small failover time may occur | No noticeable interruption |
| Lower cost | Higher cost |
| Uses redundant components | Uses fully redundant active systems |
| Suitable for most applications | Suitable for mission-critical applications |

---

## Real Example

An online banking system cannot afford downtime during transactions.

Such systems often use active-active architectures across multiple locations to provide fault tolerance.

---

# Disaster Recovery (DR)

## What is Disaster Recovery?

Disaster Recovery (DR) is the process of restoring applications and databases after a major outage or disaster.

Examples of disasters include:

- Earthquakes
- Floods
- Fire
- Large-scale power outages
- Regional network failures

Disaster Recovery focuses on restoring services as quickly as possible.

---

## Disaster Recovery Strategies

### Backup and Restore

- Lowest cost
- Longest recovery time

Data is backed up and restored only when needed.

---

### Pilot Light

A minimal environment runs continuously.

Additional resources are started during a disaster.

---

### Warm Standby

A scaled-down production environment runs continuously.

Resources are scaled up during failover.

---

### Multi-Site Active/Active

Multiple Regions actively serve users.

If one Region fails, traffic automatically shifts to another.

This provides the highest availability but also the highest cost.

---

# Recovery Objectives

## Recovery Time Objective (RTO)

RTO is the maximum acceptable time required to restore a system after an outage.

Example:

If a business defines an RTO of **30 minutes**, the service must be restored within that time.

---

## Recovery Point Objective (RPO)

RPO is the maximum acceptable amount of data loss.

Example:

If backups occur every 15 minutes, the maximum potential data loss is 15 minutes.

---

## Example Comparison

| Scenario | RTO | RPO |
|----------|-----|-----|
| Backup every 24 hours | Several hours | 24 hours |
| Multi-AZ RDS | Minutes | Near zero |
| Multi-Region Replication | Seconds | Near zero |

---

# Multi-AZ Architecture

```
Application
      │
      ▼
+---------------------+
| Availability Zone A |
| Primary Database    |
+---------------------+
          │
 Automatic Replication
          │
          ▼
+---------------------+
| Availability Zone B |
| Standby Database    |
+---------------------+
```

Advantages:

- Automatic failover
- High Availability
- Synchronous replication
- Managed by AWS

---

# Multi-Region Architecture

```
Region: Mumbai
      │
 Primary Database
      │
Cross-Region Replication
      │
      ▼
Region: Singapore
 Standby Database
```

Advantages:

- Disaster Recovery
- Geographic redundancy
- Reduced business risk

---

# AWS CLI Hands-on Lab

## View Current Region

```bash
aws configure get region
```

---

## List Available Regions

```bash
aws ec2 describe-regions \
    --query "Regions[].RegionName"
```

---

## List Availability Zones

```bash
aws ec2 describe-availability-zones
```

---

## Show Current Identity

```bash
aws sts get-caller-identity
```

---

## List S3 Buckets

```bash
aws s3 ls
```

---

# Hands-on Exercise

1. Sign in to the AWS Management Console.
2. Switch between Regions (Mumbai, Singapore, Virginia).
3. Explore the list of Availability Zones.
4. Open the EC2 Dashboard.
5. Observe how available resources change by Region.
6. Compare service availability across Regions.

---

# Best Practices

- Deploy production workloads across multiple Availability Zones.
- Enable automated backups.
- Regularly test disaster recovery procedures.
- Select Regions based on compliance and latency requirements.
- Use Infrastructure as Code (IaC) for repeatable deployments.
- Monitor system health with Amazon CloudWatch.

---

# Common Mistakes

- Deploying all resources in a single Availability Zone.
- Ignoring disaster recovery planning.
- Failing to test backups.
- Choosing a Region without considering compliance requirements.
- Assuming all AWS services are available in every Region.

---

# Troubleshooting

## Problem

Application unavailable after an Availability Zone failure.

### Possible Causes

- Single-AZ deployment.
- Missing load balancer.
- No standby database.

### Resolution

- Implement Multi-AZ deployment.
- Configure health checks.
- Enable automatic failover.

---

# DBA Production Scenario

A financial services company hosts its production PostgreSQL database on Amazon RDS.

Architecture:

- Primary database in **ap-south-1a**
- Standby database in **ap-south-1b**
- Automated backups enabled
- Cross-Region snapshot copies to **ap-southeast-1**
- CloudWatch alarms monitor CPU, storage, and connections

Benefits:

- High Availability
- Disaster Recovery
- Regulatory compliance
- Automated failover
- Minimal downtime

---

# Interview Questions

1. What is AWS Global Infrastructure?
2. What is an AWS Region?
3. What is an Availability Zone?
4. What is the difference between a Region and an Availability Zone?
5. Why are Availability Zones physically separated?
6. What is High Availability?
7. What is Fault Tolerance?
8. What is Disaster Recovery?
9. Explain RTO and RPO.
10. What is Multi-AZ deployment?
11. What is Multi-Region deployment?
12. What are Edge Locations?
13. What are Local Zones?
14. What are Wavelength Zones?
15. Why does AWS use a private backbone network?
16. How would you design a highly available database architecture?
17. How would you reduce latency for global users?
18. Which AWS services support Multi-AZ deployments?
19. What factors influence Region selection?
20. What is the difference between High Availability and Disaster Recovery?

---

# Module Summary

In this module, you learned:

- Cloud Computing fundamentals
- Cloud deployment models
- Cloud service models
- AWS overview
- AWS Global Infrastructure
- Regions
- Availability Zones
- Edge Locations
- Local Zones
- Wavelength Zones
- High Availability
- Fault Tolerance
- Disaster Recovery
- RTO and RPO
- Multi-AZ architecture
- Multi-Region architecture
- AWS CLI basics
- Enterprise DBA design principles

You now have the foundational knowledge required to understand how AWS provides secure, scalable, and highly available infrastructure for enterprise workloads.

---

# Next Module

➡ **Module 2 – IAM (Identity and Access Management)**

Location:

```
02-AWS/02-IAM/README.md
```

In the next module, you will learn:

- AWS Root User
- IAM Users
- IAM Groups
- IAM Roles
- IAM Policies
- MFA
- Least Privilege Principle
- Access Keys
- AWS CLI Authentication
- Enterprise IAM Best Practices