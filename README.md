# Freedom on the Move - AWS Infrastructure Documentation

## Table of Contents

1. [Overview](#overview)
2. [Database Infrastructure](#database-infrastructure)
   - [PostgreSQL Database (fotm-prod)](#postgresql-database-fotm-prod)
   - [MySQL Database (fotm-ghost-mysql)](#mysql-database-fotm-ghost-mysql)
3. [Container Services](#container-services)
   - [ECS Cluster Configuration](#ecs-cluster-configuration)
   - [Service Descriptions](#service-descriptions)
4. [Networking](#networking)
   - [VPC Configuration](#vpc-configuration)
   - [Security Groups](#security-groups)
5. [Load Balancing](#load-balancing)
   - [Legacy API Load Balancer](#legacy-api-load-balancer)
   - [Database Load Balancer](#database-load-balancer)
6. [Storage](#storage)
   - [S3 Bucket Overview](#s3-bucket-overview)
   - [Storage Architecture](#storage-architecture)
7. [Content Delivery](#content-delivery)
   - [CloudFront Distributions](#cloudfront-distributions)
   - [Domain Mapping](#domain-mapping)
8. [Security](#security)
   - [SSL/TLS Configuration](#ssltls-configuration)
   - [Database Encryption](#database-encryption)
   - [Access Control](#access-control)
9. [Monitoring and Logging](#monitoring-and-logging)
   - [CloudWatch Configuration](#cloudwatch-configuration)
   - [Database Insights](#database-insights)
10. [Backup and Recovery](#backup-and-recovery)
    - [RDS Backup Strategy](#rds-backup-strategy)
    - [Disaster Recovery Plan](#disaster-recovery-plan)
11. [Cost Optimization](#cost-optimization)
    - [Resource Sizing](#resource-sizing)
    - [Storage Management](#storage-management)
12. [Recommendations](#recommendations)
    - [High Availability Improvements](#high-availability-improvements)
    - [Security Enhancements](#security-enhancements)
    - [Performance Optimization](#performance-optimization)
    - [Cost Management](#cost-management)
13. [Appendix](#appendix)
    - [AWS Resource List](#aws-resource-list)
    - [Architecture Diagram](#architecture-diagram)
    - [Revision History](#revision-history)

## Overview

This documentation provides a comprehensive guide to the AWS infrastructure supporting the Freedom on the Move project. The infrastructure spans multiple AWS services including RDS, ECS/Fargate, S3, CloudFront, and Application Load Balancers to deliver a scalable, secure, and reliable platform.

The project consists of multiple components including a database search interface, a legacy API, a link redirector service, and a Ghost CMS instance, all working together to provide access to historical fugitive slave advertisements from North American newspapers.
