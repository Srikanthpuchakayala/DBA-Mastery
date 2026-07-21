# Table of Contents

- Environment
- Step 1 – Verify Operating System
- Step 2 – Verify CPU Architecture
- Step 3 – Verify Homebrew
- Step 4 – Verify Git
- Step 5 – Verify VS Code CLI
- Step 6 – Verify AWS CLI
- Step 7 – Verify MySQL
- Step 8 – Verify Docker
- Step 9 – Verify Python
- Step 10 – Verify Java
- Step 11 – Create Project Workspace
- Step 12 – Create Project Structure
- Step 13 – Documentation Files
- Step 14 – README Files
- Step 15 – Git Configuration
- Step 16 – GitHub Repository
- Step 17 – Connect Local Repository
- Step 18 – First Commit
- Step 19 – Push to GitHub
- AWS CLI Review
- Lessons Learned
- Next Steps





# Phase 0 – 
Environment Setup

## Objective

Prepare a professional Database Administration (DBA) development environment on macOS that will be used throughout the DBA Mastery roadmap.

---

# Environment

| Component | Value |
|-----------|-------|
| Operating System | macOS 15.6 |
| Architecture | Apple Silicon (ARM64) |
| Workspace | ~/Projects/DBA-Mastery |

---

# Step 1 - Verify Operating System

## Command

```bash
sw_vers
```

### Purpose

Displays the installed macOS version.

### Output

```text
ProductName: macOS
ProductVersion: 15.6
BuildVersion: 24G84
```

### Notes

Verified that the system is running the latest macOS version.

---

# Step 2 - Verify CPU Architecture

## Command

```bash
uname -m
```

### Purpose

Checks the processor architecture.

### Output

```text
arm64
```

### Notes

Confirmed that the machine uses Apple Silicon (M2).

---

# Step 3 - Verify Homebrew

## Command

```bash
brew --version
```

### Purpose

Checks whether Homebrew is installed.

### Output

```text
Homebrew 6.0.9
```

### Status

✅ Installed

---

# Step 4 - Verify Git

## Command

```bash
git --version
```

### Output

```text
git version 2.39.5 (Apple Git-154)
```

### Status

✅ Installed

---

# Step 5 - Verify VS Code CLI

## Command

```bash
code --version
```

### Initial Output

```text
zsh: command not found: code
```

## Problem

VS Code was installed, but the `code` command was not available in Terminal.

## Resolution

Opened Visual Studio Code.

Command Palette:

```
Shell Command:
Install 'code' command in PATH
```

Restarted Terminal.

Verified again.

```bash
code --version
```

### Status

✅ Fixed

---

# Step 6 - Verify AWS CLI

## Command

```bash
aws --version
```

### Output

```text
aws-cli/2.24.15 Python/3.12.9 Darwin/24.6.0 exe/x86_64
```

### Status

✅ Installed

---

# Step 7 - Verify MySQL

## Command

```bash
mysql --version
```

### Output

```text
mysql Ver 9.6.0 for macos15.7 on arm64 (Homebrew)
```

### Status

✅ Installed

---

# Step 8 - Verify Docker

## Command

```bash
docker --version
```

### Output

```text
Docker version 20.10.17
```

### Status

⚠️ Installed

### Future Improvement

Upgrade Docker to the latest version.

---

# Step 9 - Verify Python

## Command

```bash
python3 --version
```

### Output

```text
Python 3.9.18
```

### Status

✅ Installed

---

# Step 10 - Verify Java

## Command

```bash
java -version
```

### Output

```text
Java 1.8.0_491
```

### Status

⚠️ Upgrade Required

### Future Plan

Upgrade to Java 21 LTS.

---

# Step 11 - Create Project Workspace

## Command

```bash
mkdir -p ~/Projects
```

## Purpose

Create a dedicated folder for all development projects.

---

## Command

```bash
mv ~/DBA-Mastery ~/Projects/
```

Moved the project into the new workspace.

---

## Verify

```bash
pwd
```

Expected Output

```text
/Users/sxxxxxxxxxxxx/Projects/DBA-Mastery
```

---

# Step 12 - Create Project Structure

## Command

```bash
mkdir -p \
00-Setup \
01-Linux \ 
02-AWS \
03-SQL \
04-MySQL \
05-PostgreSQL \ 
06-SQL-Server \ 
07-Oracle \
08-Amazon-RDS \
09-Amazon-Aurora \ 
10-Performance-Tuning \
11-Backup-Recovery \ 
12-High-Availability-Replication \
13-Monitoring \
14-Security \
15-Automation \
16-Migrations \
17-Production-Scenarios \
18-Projects \
19-Interview-Preparation \
20-Certifications \
Assets \
Backups \
Downloads \
GitHub \
Labs \
Logs \
Notes \
Projects \
Resources \
Screenshots \
Scripts \
Templates \
README.md \
ROADMAP.md \
CHANGELOG.md \
LEARNING-JOURNAL.md\
LICENSE
```

### Purpose

Create the complete repository structure.

---

# Step 13 - Create Documentation Files

## Command

```bash
touch README.md ROADMAP.md CHANGELOG.md LEARNING-JOURNAL.md LICENSE .gitignore
```

### Purpose

Create the main project documentation files.

---

# Step 14 - Create README Files

## Command

```bash
find . -maxdepth 1 -type d ! -name ".git" ! -name "." -exec touch {}/README.md \;
```

### Purpose

Create a README.md inside every folder.

---

# Step 15 - Configure Git

## Verify Git Username

```bash
git config --global user.name
```

Output

```text
xxxxxxxxxxxxxx
```

---

## Verify Git Email

```bash
git config --global user.email
```

Output

```text
xxxxxxxxxxxxx
```

---

# Step 16 - Create GitHub Repository

Repository Name

```
DBA-Mastery
```

Repository URL

```
git@github.com:Srikanthpuchakayala/DBA-Mastery.git
```

---

# Step 17 - Connect Local Repository

## Initialize Git

```bash
git init
```

---

## Rename Branch

```bash
git branch -M main
```

---

## Add Remote

```bash
git remote add origin git@github.com:Srikanthpuchakayala/DBA-Mastery.git
```

---

## Verify Remote

```bash
git remote -v
```

---

# Step 18 - First Commit

## Stage Files

```bash
git add .
```

---

## Commit

```bash
git commit -m "Initial repository structure"
```

---

# Step 19 - Push to GitHub

## Command

```bash
git push -u origin main
```

---

# Issue Encountered

Git returned:

```text
Updates were rejected because the remote contains work that you do not have locally.
```

### Root Cause

The GitHub repository already contained an initial commit (README, LICENSE, or .gitignore), while the local repository had a different history.

### Attempted Resolution

```bash
git pull origin main --allow-unrelated-histories
```

Git requested a pull strategy because the local and remote branches had divergent histories.

### Current Status

Pending merge and synchronization.

---

# AWS CLI Review

## Command

```bash
aws configure list
```

### Observation

AWS CLI is still configured with credentials from the old AWS account.

### Next Action

- Create an IAM user in the new AWS account.
- Generate new Access Keys.
- Reconfigure the AWS CLI.
- Enable AWS Budget and Billing Alerts.

---

# Lessons Learned

- Always verify the development environment before beginning a project.
- Keep all technical projects under `~/Projects`.
- GitHub repositories should preferably be created empty when starting locally.
- Git does not track empty directories.
- Use `README.md` files to document folders instead of relying on empty directories.
- Never commit AWS credentials, SSH private keys, passwords, or other sensitive information to GitHub.

---

# Next Steps

- Resolve Git synchronization.
- Configure GitHub SSH authentication.
- Configure AWS CLI with the new AWS account.
- Upgrade Java to Java 21 LTS.
- Configure AWS Budget Alerts.
- Begin Phase 1 – Linux Administration.


---

# Phase 0 Completion Summary

## Objectives Achieved

- ✅ macOS development environment verified
- ✅ Homebrew installed
- ✅ Git configured
- ✅ VS Code configured
- ✅ AWS CLI installed and configured
- ✅ Docker verified
- ✅ MySQL installed
- ✅ Python verified
- ✅ Java verified
- ✅ GitHub repository created
- ✅ Repository structure created
- ✅ AWS IAM User configured
- ✅ AWS CLI authenticated
- ✅ LocalStack configuration issue resolved
- ✅ Environment ready for hands-on DBA learning

---

## Deliverables

- Professional GitHub Repository
- Local Development Environment
- AWS Account Ready
- AWS CLI Ready
- Documentation Repository

---

## Status

**Phase 0 Completed Successfully**

Ready to begin:

➡️ Phase 1 – AWS Foundations    

# Next Phase

Phase 1 – AWS Foundations

Upcoming Topics

- AWS Global Infrastructure
- AWS Regions
- Availability Zones
- Edge Locations
- IAM Deep Dive
- VPC
- Security Groups
- EC2
- EBS
- CloudWatch