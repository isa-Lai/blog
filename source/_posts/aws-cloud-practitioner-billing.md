---
layout: post
title: AWS Cloud Practitioner - Billing
date: 2021-09-10 14:35:34
categories: [Certification,AWS]
tags: [AWS]
toc: true
---

Billing take 18% of the total exam. However, there are many aspects can appear in the exam.  Since this part mainly relies on memory, it is important to understand every concept of billing in the AWS webpage.

<!-- more -->

## Free services
- IAM - Identity Access Managment
- Amazon VPC
- Organizations & Consolidated Billing
- AWS Cost Explorer

THese are free but can procision AWS services which cost
- Auto Scaling
- CloudFormation
- Elastic Beanstalk
- Opsworks
- Amplify
- AppSync
- CodeStar

## AWS Support Plans
- Basic: Email Support for bulling and account
- Developer
- Business
- Enterprise
![Plan Details](https://i0.wp.com/awsnewbies.com/wp-content/uploads/2018/09/supportplans.png?resize=690%2C243)

Key Concept
- Difference
- Support Time
- Third Party Support

## AWS Marketplace
- [Marketplace](https://aws.amazon.com/marketplace/) is curated digital catelogue with thousand of software listings from independent software vendors
- Easily find, buy, test, and deploy on AWS
- Some free, some associated charge which be part of the AWS bills
- The sales channel for ISVs and COnsulting Partners allows you to sell your solutions to other AWS costomers

## Trusted Advisor
[Advises](https://aws.amazon.com/premiumsupport/technology/trusted-advisor/) on
- Security
- Saving Money
- Performance
- Service limits
- Fault tolerance

## Consolidated Billing
- One bill for all of our accounte
- Accross **Multi** AWS accounts into one bill
- SWA treats all the accounts in an organization as if they were one account
- Can designate one **Master account** that pays the charges of all the other **member accounts**
- Offered no additional cost
- Use **Cost Explorer** to visialize usage for consolidated billing

### Volume DIscounts
The more you use, the more ou save.
Usage from different accout can combine.
Example:
| Data Transfer |              |
|---------------|--------------|
| First 10TB    | $0.17 per GB |
| Next 40TB     | $0.13 per GB |


### Cost Explorer
Visualize, understand and manage the AWS cost and usage.
Consolidated in the master account

## Budgets
Plan usage service costs and istance reservations
- First two budegt are free
- Each cost $0.02 per day. ~0.60 USD per mo
- 20,000 budgets limit
- Set up alerts if exceeed or are approaching the budget, notify by
  - email
  - chatbot
- Creat budget for
  - Cost
  - Usage
  - Reservation, support for
    - EC2, RDS, Redshift, ElasticCache
- Track monthly, quarterly, or yearly
- Manage on **AWS Budgets** dashboard or **Budgets API**

## TCO Calculator
[Total Cost of Ownership](https://calculator.aws/#/)
- estimate how much can save when moving to AWS from on-premise
- Details set of reports, can use in presentation
- Approximation purposes only

## Landing Zone
[Landing Zone](https://aws.amazon.com/solutions/implementations/aws-landing-zone/)
- Help **enterprises** quickly set-up a secure, AWS multi account
- Provice **baseline environment** to start **multi account architechture**
- AWS Account Vending Machine (**AVM**)
  - Auto procisions and configure new account via **Service Catalog Template**
  - Uses SIngle Sign-on (**SSO**) for manageing and accessing
  - The environment is customizable to allow costomer to implement account base line through Landing Zone configuration and update pipeline 

## Resource Groups and Tagging
- Tags: Word or phrase that act as metadata for organizing AWS resources
- Resource Groups: Collection of Resources that share one or more tages. Desplay detail based on
  - Metrics
  - Alarms
  - Configuration Settings

## QuickStart
**Prebuild Tamplate** by AWS or AWS partners help to deploy popular stacks on AWS
Composed of 3 parts
1. A reference architechture for the deploymenet
2. **AWS CloudFormation** templates that automate and condigure the deployment
3. A deployment guide explaining the architecture and implementation in detail.

## Cost and Usage Reports
Generate in spreadsheet, and analyze
- Places the reports into S3
- Use Athena to make queryable databse
- Use QuickSight to visualize your billing data as graphs
