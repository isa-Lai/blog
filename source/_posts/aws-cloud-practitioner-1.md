---
layout: post
title: AWS Cloud Practitioner - Cloud Concept
toc: true
date: 2021-09-09
categories: [Certification,AWS]
tags: [AWS]
---

## CCP
AWS Cetified Cloud Practitioner only require fundationa knowledge in AWS. It focus on blling and business-vertric concepts. 

<!-- more -->

## Cloud Concepts Intro
Cloud concepts take 28% in the exam. It required
1. Define AWS Cloud and its value proposition
2. Identify aspected of AWS Cloud ecomonics
3. List the differenct cloud architechture design principles

## Cloud Computing
The definition of Cloud Computing is the practice of using a network of remote servers hosted on the Internext to store, manage, and process data, rather than a local server or a personal computer.

### Pros
1. Trade capital expense for variable expence. No upfront-cost, Pay on-demand
2. Benefit from massive economies of scale.
3. Stop guessing capacity.
4. Increase speed and agility
5. Stop spending money on running and maintaining data centers
6. Go global in minutes

### Type
1. SaaS: Software as a Service for customers
2. PaaS: Platform as a Service for developer
3. Iaas: Infrastructure as a Service for admins

### Cloud Computing Deployment Models
1. Cloud: Fully utilizing cloud computing.
2. Hybrid: Using both cloud and on-premise
3. On-Premise: Private cloud, deloying resources on-permises, using cirtualization and resource management tools.

## Global Infractructure 
69 **Availablility zones** with in 22 **Geographic Regions** around the world 
Way more **edge locations** than AZs.

Region: physical location with mult AZ
Availability Zones: one ore more discrete data centers.
Edge Location: datacenter owned by a trusted partner of AWS.

### Region
- Region: physical location with multi datacenters
- Each region has at least **2** AZ
- AWS lergest region is **US-EAST**
- Not all services are available in all regions
- **US-EAST-1** is the region where you see all your billing info
- Check the newest region and AZ info on [AWS Regions](https://aws.amazon.com/about-aws/global-infrastructure/regions_az/)

### AZs
- An AZ is a datacenter owned and operated by AWS in which AWS services run
- AZ are represented by a Region code + a letter identifier eg. us-east-1a
- **Multi-AZ** distrubuting your instances across multiple AZs allows failover configuration for handling requests when one goes down
- < 10ms latency between AZs

### Edge Location
- Edge Location is a datacenter owned by a trusted partner of AWS which has a **direct connection** to the AWS network.
- These server requests for **CloudFront** and **Route 53**. Requests going to either of these services will be routed to the nearest edge location automatically
- **S3 Transfer Acceleration** traffic and **API Gateway** endpoint traffic also use the AWS Edge Nework
- This allows for **Low Latency** nomatter where the end user is geographically located

### GovCloud Regions
- AWS GovCloud Regions allow customers to host sensitive **Controlled Unclassified Info** and other types of regulated workloads
- Only operated by employees who are US citizens on US soil
- They are only accessible to US entities and root account holders who pass a screening process