# Lab 01 – Installing MySQL Community Server 8.4 LTS on Amazon Linux 2023

## Objective

Install Oracle MySQL Community Server 8.4 LTS on an AWS EC2 instance running Amazon Linux 2023 and verify that the database server is operational.

---

## Prerequisites

- AWS Account
- EC2 Instance (Amazon Linux 2023)
- SSH Access
- Internet Connectivity
- Sudo Privileges

---

## Environment

| Component | Value |
|-----------|-------|
| Cloud | AWS |
| OS | Amazon Linux 2023 |
| Database | MySQL Community Server |
| Version | 8.4.10 LTS |
| Package Manager | DNF |

---

# Theory

## What is MySQL?

MySQL is an open-source Relational Database Management System (RDBMS) developed by Oracle. It stores data in tables and uses SQL (Structured Query Language) for data management.

---

## Why MySQL?

- Open Source
- High Performance
- ACID Compliance
- Enterprise Ready
- Replication Support
- Backup & Recovery
- High Availability
- Widely used in enterprise applications

---

## What is DNF?

DNF (Dandified Yum) is the package manager used by Amazon Linux 2023 and other Red Hat-based Linux distributions.

It is responsible for:

- Installing packages
- Updating packages
- Removing packages
- Resolving dependencies
- Managing repositories

---

## What is an RPM?

RPM stands for RPM Package Manager.

RPM files contain software or repository configuration used by DNF for installation.

---

## Repository Architecture

Internet
↓
Oracle MySQL Repository
↓
DNF
↓
Amazon Linux
↓
MySQL Community Server

---

# Installation Steps

## Step 1 – Verify repositories

```bash
sudo dnf repolist
```

---

## Step 2 – Download Oracle Repository

```bash
sudo wget https://dev.mysql.com/get/mysql84-community-release-el9-1.noarch.rpm
```

---

## Step 3 – Install Repository

```bash
sudo dnf install -y ./mysql84-community-release-el9-1.noarch.rpm
```

---

## Step 4 – Verify Repository

```bash
sudo dnf repolist
```

Expected repositories:

- mysql-8.4-lts-community
- mysql-connectors-community
- mysql-tools-8.4-lts-community

---

## Step 5 – Install MySQL

```bash
sudo dnf install -y mysql-community-server
```

---

## Step 6 – Verify Version

```bash
mysql --version
```

Output:

```
mysql Ver 8.4.10
```

---

## Step 7 – Start Service

```bash
sudo systemctl start mysqld
```

---

## Step 8 – Enable Auto Start

```bash
sudo systemctl enable mysqld
```

---

## Step 9 – Verify Service

```bash
sudo systemctl status mysqld
```

Expected:

```
Active: active (running)
```

---

## Step 10 – Verify Process

```bash
ps -ef | grep mysqld
```

---

## Step 11 – Verify Port

```bash
sudo ss -tulnp | grep 3306
```

Ports:

- 3306 (MySQL)
- 33060 (MySQL X Protocol)

---

## Step 12 – Retrieve Temporary Password

```bash
sudo grep 'temporary password' /var/log/mysqld.log
```

---

## Step 13 – Login

```bash
mysql -u root -p
```

---

## Step 14 – Change Root Password

```sql
ALTER USER 'root'@'localhost'
IDENTIFIED BY 'NewStrongPassword';
```

---

## Step 15 – Verify Login

```bash
mysql -u root -p
```

---

# Verification Checklist

- Repository Added ✅
- MySQL Installed ✅
- Service Running ✅
- Auto Start Enabled ✅
- Root Password Changed ✅
- Login Successful ✅

---

# Troubleshooting

## dnf: command not found

Cause:

Running Linux commands on macOS.

Solution:

SSH into the EC2 instance first.

---

## mysql-server package not found

Cause:

Oracle repository not configured.

Solution:

Install the MySQL Community Repository RPM.

---

## mysqld service won't start

Check:

```bash
sudo systemctl status mysqld
```

View logs:

```bash
sudo journalctl -u mysqld
```

---

# Interview Questions

### What is DNF?

DNF is the package manager used by Amazon Linux and other Red Hat-based distributions for installing, updating, and managing software packages.

---

### Why did we install the Oracle Repository?

Amazon Linux repositories do not include Oracle MySQL Community Server by default. Adding Oracle's repository allows installation of the official MySQL packages.

---

### What is Port 3306?

Default MySQL client communication port.

---

### What is Port 33060?

MySQL X Protocol port used by MySQL Shell and Document Store.

---

### Why change the temporary root password?

The temporary password is generated during installation for security. It must be replaced with a strong permanent password before normal administration.

---

# Key Takeaways

- Learned DNF package management
- Configured Oracle MySQL Repository
- Installed MySQL Community Server 8.4 LTS
- Managed services with systemctl
- Verified ports and processes
- Changed the MySQL root password
- Successfully connected to the database server

---

# Next Lab

Lab 02 – MySQL Architecture and System Databases