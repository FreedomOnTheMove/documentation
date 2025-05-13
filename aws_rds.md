# Freedom on the Move - AWS Infrastructure Documentation

## RDS (Relational Database Service)

The project utilizes two separate RDS database instances:

### 1. PostgreSQL Database (fotm-prod)

**General Configuration:**
- **DB Identifier:** fotm-prod
- **Engine:** PostgreSQL 15.7
- **Role:** Instance (primary)
- **Region & AZ:** us-east-1c
- **Current Activity:** 30 Connections
- **CPU Usage:** 3.66%
- **Created:** May 03, 2023, 12:56 (UTC-04:00)

**Instance Details:**
- **Instance Class:** db.t4g.medium (2 vCPU, 4 GB RAM)
- **Architecture:** ARM-based processor (t4g)
- **License Model:** PostgreSQL License
- **DB Name:** fotm
- **Master Username:** fotm
- **Parameter Group:** postgres15-most (in sync)
- **Option Group:** default-postgres-15 (in sync)

**Storage Configuration:**
- **Storage:** 250 GiB
- **Storage Type:** General Purpose SSD (gp2)
- **Encryption:** Enabled (AWS KMS)
- **Storage Autoscaling:** Disabled
- **Provisioned IOPS:** Not specified

**High Availability & Security:**
- **Multi-AZ:** No
- **Secondary Zone:** Not configured
- **Deletion Protection:** Enabled
- **Architecture:** Non-multitenant
- **IAM DB Authentication:** Not enabled

**Monitoring:**
- **Monitoring Type:** Database Insights - Standard
- **Performance Insights:** Disabled
- **Enhanced Monitoring:** Disabled
- **DevOps Guru:** Disabled

**Purpose:** Main application database storing advertisements, crowdsourcing information, and user content.

### 2. MySQL Database (fotm-ghost-mysql)

**General Configuration:**
- **DB Identifier:** fotm-ghost-mysql
- **Engine:** MySQL Community 8.0.40
- **Role:** Instance (primary)
- **Region & AZ:** us-east-1d
- **Current Activity:** 0.05 sessions
- **CPU Usage:** 1.96%
- **Created:** August 31, 2023, 10:47 (UTC-04:00)

**Instance Details:**
- **Instance Class:** db.m5d.large (2 vCPU, 8 GB RAM)
- **Instance Storage:** 75 GiB NVMe SSD
- **License Model:** General Public License
- **Master Username:** admin
- **Parameter Group:** default-mysql8.0 (in sync)
- **Option Group:** default-mysql-8-0 (in sync)

**Storage Configuration:**
- **Storage:** 200 GiB
- **Storage Type:** General Purpose SSD (gp3)
- **Encryption:** Enabled (AWS KMS)
- **Storage Autoscaling:** Enabled
- **Maximum Storage Threshold:** 1000 GiB
- **Provisioned IOPS:** 3000 IOPS
- **Storage Throughput:** 125 MiBps

**High Availability & Security:**
- **Multi-AZ:** No
- **Secondary Zone:** Not configured
- **Deletion Protection:** Enabled
- **Architecture:** Non-multitenant
- **IAM DB Authentication:** Not enabled

**Monitoring:**
- **Monitoring Type:** Database Insights - Standard
- **Performance Insights:** Enabled
- **Retention Period:** 7 days
- **Enhanced Monitoring:** Disabled
- **DevOps Guru:** Disabled

**Purpose:** Supports the Ghost CMS platform for content management.

---

These databases are publicly accessible by members of the security group.

Ideally Multi-AZ deployments would be used but the current selections are price conscientious. 