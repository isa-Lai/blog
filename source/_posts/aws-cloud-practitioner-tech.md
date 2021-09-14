---
layout: post
title: AWS Cloud Practitioner - Technology
date: 2021-09-13 19:59:50
categories: [Certification,AWS]
tags: [AWS]
toc: true
---
Tachnology take 33% of the exam, which has the most percentage.

<!-- more -->

## Organizations and Accounts
- **Organizations** allow to centrally manage billing, control access, compliance, security, share resources
- **Root Account User** is a single sign-in identity that has complete access to all service.
  - Each account has a root account user
- **Organization Units** are a group of AWS accounts within an organization - create a hierarchy
- **Sercvice Control Policies** give central control over the allowed permisions for all accounts

## Networking
- **Region** the geograohical location of your network
- **AZ** the data center
- **VPC** a logically isolated sention of the AWS cloud where you can launch AWS resources
- **Internet Gateway** enable access to the internet
- **ROute Tables** determine where network traffic from your subnets are directed
- **NACLs** acts as a firewall at the instance level
- **Subnets** a logical pertition of an IP network into multiple, smaller network segments
  
![AWS Networking](https://4sysops.com/wp-content/uploads/2016/09/AWS-network-diagram-600x544.png)

## Database Service
- **DynamoDB** - NoSQL `key/value` database
- **DocumentDB** - NoSQL `Document` database that is MongoDB compatible
- **RDS** - `relational` database service that supports multiple engines: mySQK, Postgresm NatuaDB, oravle, MSSS, auroroa
  - **Aurora** MySql (5x faster) and PSQL (3x faster) database `fully managed`
  - Aurora Serverless - only runs when you need it, like AWS Lamda
- **Neptune** - managed `graph` database
- **Redshift** - `culumnar` database, `petabyte` warehouse
- **ElastiCache** - `Redis`, or `memcached` database

## Procisioning Service
Provisioning : The allocation or creation of resources and services to a customer
- **Elastic Beanstalk** - service for delploying and scaling web applications and services developed with Java.
- **OpsWorks** - comfiguration management service that provides managed instance of `Chef` and `Puppet`
- **CloudFormation** - premake packages that can luanch and configure your AWS compute, network, storage, and other services required to deploy a workload on AWS
- **AWS Marketplace**

## Computing Service
- **EC2** elestic compute cloud, highly configurable server eg, CPU, Momory, network, OS
  - `Docker as a Service` highly scalable, high-performance container orchestration service that supports Docker containers, pay for EC2 instances
- **Fargate** microservices where dont care about the infrastruture. Play per task
- **ESK** `Kubernetes as a Service` easy to deploy, manage, and scale containerized applications using Kubernetes
- **Lambda** `serverless functions` run code without providioning or managing servers. Pay only for the compute time you consume
- **Elastic Beanstalk** orchestrates various AWS services. include EC2, S3 simple notification service (SNS), cloudwatch, autoscaling, autoscaling, and elastic load balancers
- **AWS Batch** plans, schedules, and executes your batch computing workloads across the full range of AWS compute services and features, such as **Amazon EC2** and **Spot Instances**

## Storage Service
- **S3** simple storage service - `object` storage
- **S3 Glacier** - low cost storage for archiving and long-term backup
- **Storage Gateway** - hybrid cloud storage with local caching
  - file gateway
  - volume gateway
  - tape gateway
- **EBS** - Elastic Block Storage - hard drive in the cloud you attach to EC2 instances eg. SSD, IOPS SSD, Throughput HHD, Cold HHD
- **EFS** - Elastic File Storage - file storage mountable to multiple EC2 instances at the same time
- **Snowball** - Physically migrate lots of data via a computer suitcase 50-80 TB
  - **Snowball Edge** a better version of snowball - 100TB
  - **Snowmobile** Shipping container, pulled by a semi-trailer trucj - 100PB

## Business Centric Services
- **Amazon Connect** - `Call Center` - Cloud-based call center services you can setup in just a few click
- **WorkSpaces** - `Virtual Remost Desktop` - Secure managed service for provisioning
- **WorkDOcs** - content creation and collaboration service (`AWS Sharepoint`)
- **Chime** - AWS platform for **online meetings, video conderancing**
- **WorkMail**
- **Pinpoint** - marketing compaign management system `use for sending targeted email`, SNS, voice message
- **SES - Simple Email Service** - send marketing , notification, and emails (for marketers)
- **QuickSight** - A Business Intelligence (BI) service. Connect multiple datasource and quickly visualize data

## Enterprise Integration
- **Direct Connect** dedicated Gigabit network connection from your premises to AWS imgagine
- **VPN** secure connection to your AWS network
- **Storage Gateway** a hybrid storage service that enables your on-permises applications to use AWS cloud storage
- **Active Directory** the AWS directory service dor MS Active Directory - AWS Managed MS AD]

## Logging Service
- **CloudTrail** -logs all `API calls`(SDK, CLI) between `AWS services`
  - Detect developer misconfiguration
  - Detect malicious actors
  - Automate responses
- **CloudWatch** a collection of multiple services
  - **Logs** performance data about AWS services
  - **Metrics** represents a time-ordered set of data points. A variable to monitor
  - **Events** trigger an event based on a condition 
  - **Alarms** triggers notifications based on metrics
  - **Dashboard** create visualizations based on metrics

## Initialism
Check [AWS docs](https://docs.aws.amazon.com/general/latest/gr/glos-chap.html) for more info.