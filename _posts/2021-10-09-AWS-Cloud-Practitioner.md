---
title: AWS Cloud Practitioner
tags: [AWS, Cloud, Technology]
style: 
color: success
description: AWS Cloud Practitioner is the first of many certifications you can gain in Amazon Web Services (AWS). This is a guide for passing the AWS Cloud Practitioner Certification and leaning the fundamental concepts of the AWS cloud.  
---



A few months ago I decided that I wanted to gain the AWS Cloud Practitioner Certification. The case for moving data and computing processes from on-premise to the cloud is becoming more and more compelling. If you work in technology and you are not already working with cloud computing, it's very likely you will be working with it in future. Making a start now to learn the core concepts of cloud computing will give you a head start and position you well to secure your digital future.

AWS (Amazon Web services) is one of the top cloud providers offering their cloud-based platform, infrastructure, application, or storage services. Leaning the AWS cloud is a good place to start, however, Microsoft Azure and Google Cloud also offer great learning materials and certifications. 

Anyways, here is a guide to what you need to know before taking the AWS Cloud Practitioner Certification exam:

# Contents

{% capture list_items %}
Introduction to AWS
Networking 
Compute services
Business Services 
Business Centric Services 
Provisioning Services 
Storage Services 
Security 
Architecting 
Pricing and Support
{% endcapture %}
{% include elements/list.html title="Table of Contents" type="toc" %}

# Introduction to AWS
- On-demand delivery of IT resources. Can scale up and down based on needs.
- Fosters agility (number one reason why customers switch to cloud computing): Speed (global reach), experimentation (operations as code, templated environments with CloudFormation) and culture of innovation (experiment quickly with low cost)
- Using Auto Scaling and ELB, scale up and down and only pay for what you use.
- Ability to deploy systems in multiple regions (lower latency)
- Ability to choose the region where data is stored
- AWS is responsible for data centre security
- Security policy can be formalized (as code)
- Ability to recover from failures

## Region:
Region is a geographically distinct location in the world which contains multiple AZs. Every region is physically isolation from and independent of every other region. Each region has at least 2 AZs. AWS largest and most available region is US-EAST. Not all services are available in all regions. 

##Availability Zone (AZ): 
AZs contain one or more discrete data centres with independent resources and housed in different facilities. <10ms latency between AZs. 

## Edge Locations: 
Datacentre owned by a trusted partner of AWS, there are away more Edge Locations than Availability Zones (AZs). These locations serve requests for CloudFront and Route 53, requests automatically go to edge locations. Also used by S3 transfer acceleration traffic and CPI gateway endpoint traffic. 

## GovCloud (US) Regions: Operated by US citizens on US soil only. Allow customers to host sensitive Controlled Unclassified Information. E.g., complies with department of defence security requirements. 


# Networking

## Virtual Private Cloud (VPC)
- Uses same concepts as on-premise networking
- VPC can span across multiple AZs
- Supports multiple subnets (each of which can be deployed in a different AZ)
- Can create public-facing subnets and private-facing subnets within the same VPC
- Each account can create multiple VPCs
- Using fewer VPCs is recommended to avoid complexity
- Can assign Internet Gateways to specific subnets to allow public access

## internet Gateway
- An internet gateway is a connection between a VPC and the internet. You can think of an internet gateway as being similar to a doorway that customers use to enter the coffee shop. Without an internet gateway, no one can access the resources within your VPC.

## Virtual Private Gateway 
- The virtual private gateway is the component that allows protected internet traffic to enter into the VPC. Even though your connection to the coffee shop has extra protection, traffic jams are possible because you’re using the same road as other customers.

## AWS Direct Connect
- AWS Direct Connect is a service that enables you to establish a dedicated private connection between your data center and a VPC.

# Compute Services

## Amazon Lightsail: Managed Virtual Private Servers service
- Fixed price.
- Includes a static IP, DNS management and storage
- Fixed configuration
- Uses t2 class EC2 instances under the hood

## AWS Elastic Compute Cloud (EC2)
- ‘launching a server’ involves, 1. choose what OS to use 2. Choose the size the server 3. Choose how many instances (servers) 4. Create IAM role 5. Launch EC2
### Difference between EC2-Classic and EC2-VPC
- EC2-Classic: Your instances run in a single, flat network that you share with other customers.
- EC2-VPC: Your instances run in a virtual private cloud (VPC) that’s logically isolated to your AWS account.
- Connecting to an instance: using SSH (with a key pair) or with Simple Sessions Manager (SSM) (recommended) or EC2 instance connect 
### Pricing:
- Dedicated hosts: a physical server with EC2 instance capacity fully dedicated for use – is physically isolated
- On-demand: you pay by the hour for usage of an AWS instance 
- Spot: user bids for the price of spare EC2 instances
- Reserved: Lock in AWS instances for a span of 1 to 3 tears and get discount compared to on-demand. 

## AWS Elastic Container Service (ECS)
- Highly scalable, high-performance container management system that enables you to run and scale containerized applications on AWS. 
- Amazon ECS supports Docker containers. Docker is a software platform that enables you to build, test, and deploy applications quickly. 
- With Amazon ECS, you can use API calls to launch and stop Docker-enabled applications.
Kubernetes as a Service (EKS) 
- Easy to deploy, manage and scale containerised applications using Kubernetes 

## Amazon Machine Image (AMI)
- An AMI is a template that contains the software configuration (operating system, application server and applications) required to launch your instance (server). You can select an AMI provided by AWS, the user community of the AWS marketplace, or you can select one of your own AMIs.

## Auto Scaling
- Help ensure that multiple instances (servers) are running (at least one server continuously running at all times) 
- Adding more instances: Scaling out, terminating instances: Scaling in
- Launch configuration answers “What” (AMI, Instance type, Security Groups, Roles). Creating an LC is similar to creating a new EC2 instance.
- Auto Scaling Group answers “Where” (VPC and subnet(s), load balancer, minimum and maximum instances, desired capacity)
- Auto Scaling Policy answers “When” (Scheduled/on-demand/scale out or in policy)
 
## AWS Lambda
- Run code with no servers to manage
- Set code to trigger from an event source
- Pay as you go: Only pay for the time your code runs. Supports sub second metering. Charged for every 100 milliseconds of execution time
- Some limitations apply: AWS Lambda Limits
- Can only run for up to 15 minutes max

## Application Load Balancer (ALBs)
- Handles layer 7 (Application) requests
- Supports routing to containers
- Key terms:
- Listeners: A process that checks for connection requests using the configuration (protocol, port)
- Target: Destination for traffic
- Target Group: Each target group routes requests to one or more registered targets
- Target checks can be performed per target group basis
- Integrates with ECS and supports dynamic ports utilized by scheduled containers
- Need to create at least 2 AZs when creating an Application Load Balancer
- Ability to route to different target groups based on port or path

## Elastic Load Balancer (ELBs)
- Enable you to put a load balancer in front of your instances so that when traffic comes into your application it is going to evenly distribute that traffic to available instances.
- Supports sticky sessions
- Supports multiple AZs and cross-zone balancing
- For HTTP/HTTPS it uses “Least Outstanding” method to route the request. For TCP, it uses “Round robin”. The least outstanding routing algorithm is defined as “A ‘least outstanding requests routing algorithm’ is an algorithm that choses which instance receives the next request by selecting the instance that, at that moment, has the lowest number of outstanding (pending, unfinished) requests.”

## Network Load Balancer (NLBs) 
- Handles Layer 4 (Transport) requests
- TCP and TLS traffic where extreme performance is required 
- Capable of handling millions of requests per second while maintaining ultra-low latencies 
- Optimised for sudden and volatile traffic patterns while using a single static IP address per Availability zone. 

## CloudFront
- CloudFront is used as a CDN (content distribution network) – sharing files across the world but to load as fast as possible using the shortest route to the user.  
- Copies content to multiple edge locations across the world. 

## Amazon Glacier
- Vaults have access and lock policies attached to them
- Each AWS account can create up to 1000 vaults
- Can create an S3 lifecycle policy to move to Glacier then delete after a period of time
- Supports up to 40TB max item size (S3 supports 5TB)
- It costs more per retrieval
- Vault Lock allows you to easily deploy and enforce compliance controls for individual Amazon Glacier vaults with a vault lock policy. You can specify controls such as “write once read many” (WORM) in a vault lock policy and lock the policy from future edits. Once locked, the policy can no longer be changed

# Business Services 

## Amazon Relational Database Service (RDS)
- Can create a standby copy in a different AZ within the same VPC
- Can create multiple read replicas (in different regions as well)
### Aurora
- Amazon Aurora – a MySQL and PostgreSQL compatible enterprise-class database – the most expensive option
- Managed MySQL-clone (compatible with MySQL)
- After a crash it doesn’t need to redo log files. It performs it on every read operation which reduces the restart time
### Aurora Serverless 
- Only runs when you need it, like AWS Lambda

## DynamoDB
- NoSQL key/value database
- Always uses SSD for storage
- Supports auto-scaling. Increases/decreases the throughput based on load
- Tables are partitioned by primary key
- Two query methods: Query and Scan
- Query uses the primary key to find items. Scan can use any attribute.
- Scan is slower than Query as it needs to look at all items

## DocumentDB
- NoSQL document database that is MongoDB compatible

## Amazon Redshift
- Managed data warehouse
- Supports standard SQL
- Supports ODBC/JDBC connectors

## ElastiCache
- Redis or Memcached database

## AWS Trusted Advisor
- Advises you on security, saving money/cost optimisation, performance, service limits and fault tolerance. 
- FREE: 7 trusted advisor checks 
- Business, Enterprise: All trusted advisor checks/recommendations
- Checks all the resources used and gives advice based on best practices
- Has an API and can be used to automate optimisations
- Can use it with CloudWatch alarms

# Business Centric Services 

## Amazon Connect 
- Call Centre – cloud-based call centre service you can set up in just a few clicks – based on the same proven system used by the Amazon customer service teams 

## WorkSpaces 
- Virtual Remote Desktop – Secure managed service for provisioning either Windows or Linux desktops in just a few minutes which quickly scales up to thousands of desktops 

## WorkDocs 
- A content creation and collaboration service – easily create, edit and share content saved centrally in AWS. (the AWS version of SharePoint) 

## Chime 
- AWS platform for online meetings, video conferencing, and business calling which elastically scales to meet your capacity needs 

## WorkMail 
- Managed business email, contacts, and calendar service with support for existing desktop and mobile email client applications. (IMAP) 

## Pinpoint 
- Marketing campaign management system you can use for sending targeted email, SMS, push notifications and voice messages. 

## SES – Simple Email Service
- A cloud-based email sending service designed for marketers and application developers to send marketing notification and emails.
- Sends HTML emails whereas SNS cannot

## SNS – Simple Notification Service
- Send notifications to subscribers of topics via multiple protocol e.g. HTTP, Email, SQS, SMS. 
- SNS is generally used for sending plain text emails which is triggered via other AWS services. 

## SQS - Simple Queue Service
- Places messages into a queue, applications pull queue using AWS SDk. 

## QuickSight 
- A Business Intelligence (BI) service. Connect multiple datasource and quickly visualise data in the form of graphs with little to no programming knowledge. 

# Provisioning Services 

## Elastic Beanstalk
- Platform as a service
- Allows quick deployments of applications
- Allows HTTPS on load balancers
- Supports various platforms (node.js, python etc)
- Provisions the resources required (EC2, ELB etc) automatically

## AWS QuickStart 
- Prebuilt templates by AWS and AWS partners to help you deploy populate stacks on AWS and reduce hundreds of manual procedures into just a few steps. 
oA Quick Start is comprised of 3 parts:
1. A reference architecture for the deployment 
2. AWS CloudFormation templates that automate and configure the deployment 
3. A deployment guide explaining the architecture and implementation in detail 

## OpsWorks 
- Configurations management service that provides managed instances of Chef and Puppet

## CloudFormation 
- Infrastructure as code JASON or YAML 

# Storage Services 

## S3 – Simple Storage Service 
- Object storage 
- S3 does not require a region selection (it is global) but the buckets we create (to contain files) must be region specific/globally unique.
- Objects are stored redundantly across multiple facilities withing the same region
- Can configure cross-region replication for backup and disaster recovery
- Amazon S3 Transfer Acceleration enables fast, easy, and secure transfers of files over long distances between your client and an S3 bucket
- Costing is based on the storage class, requests and data retrievals and data transfer OUT from Amazon S3 to internet. 
- HTTP code 200 indicates successful upload of an object to Amazon S3

## S3 Glacier 
- Low-cost storage for archiving and long-term backup
- Wait several hours to retrieve files and there is a retrieval cost
- Useful for organisations with sensitive data they must hold onto for 7-10 years

## Storage Gateway 
- Hybrid cloud storage with local caching 
- File Gateway, Volume Gateway, Tape Gateway 

## EBS – Elastic Block Storage
- Hard drive in the cloud you attach to EC2 instances 
- SSD, IOPA SSD, Throughput HHD, Cold HHD
- Allows point-in-time snapshots and creation of a new volume from a snapshot
- Supports encrypted volumes free of charge
- EBS volume must be created in the same AZ as the EC2 instance that will use it

## EFS – Elastic File Storage 
- File storage mountable to multiple EC2 instances at the same time 

## Snowball 
- Physically migrate lots of data via a computer suitcase 50-80 TB
- Snowball Edge – a better version of Snowball – 100 TB 
- Snowmobile – Shipping container, pulled by truck – 100 TB

# Security 

## The AWS Shared Responsibility Model
- AWS handles infrastructure security
- AWS provides 3rd party audit reports
- AWS’s responsibilities include: OS and database patching, firewall configuration and disaster recovery
- Customer is responsible for putting logical access controls in place and protect account credentials
- Customers are responsible to secure everything they put in the cloud
  
## AWS Service Catalogue
- Allows to centrally manage common IT services that are approved for use on AWS

## AWS IAM
- Controls access to AWS resources
- Handles Authentication (who can access resources) and authorization (how they can use resources)
- Users can have programmatic access and/or console access.
### Best practices
- Delete root account keys. Instead use IAM accounts
- Use MFA (Multi Factor Authentication)
- Create Individual IAM users
- Use groups to assign permissions
- Apply an IAM password policy 
- Use roles
- Rotate credentials
- Remove unnecessary users

## AWS Security Compliance Programs
- Risk Management: Follow the following standards:
- COBIT
- AICPA
- NIST
- HIPAA – Health Insurance Portability and Accountability Act 
- PCI – The Payment Card Industry Data Security Standard (PCI DSS)

## AWS Security Resources
- AWS Trusted Advisor: Helps to follow best practices
- AWS Account Teams: First point of contact
- AWS Enterprise Support: 15-minute response time, 24x7 availability
- AWS Partner Network
- AWS Advisories and Bulletins
- AWS Auditor Learning Path
- AWS Compliance Solutions Guide: https://aws.amazon.com/compliance/solutions-guide/
- AWS Security Blog: https://aws.amazon.com/blogs/security/

## AWS Artefact 
- How do we prove AWS meets a compliance? 
- No cost, self-service portal for on-demand access to AWS compliance reports
- On-demand access to AWS’ security and compliance reports and select online agreements 
- These checks are based on global compliance frameworks

## AWS WAF – Web Application Firewall
- AWS Web Application Firewall protect your web applications from common web exploits
- Write your own rules to ALLOW or DENY traffic based on the contents of a HTTP requests 
- Use a ruleset from a trusted AWS Security Partner in the AWS Rules Marketplace 
- WAF can be attached to either CloudFront or an Application Load Balancer
- Protect web applications from attacks covered in the OWASP top 10 most dangerous attacks (e.g., injection, broken authentication, sensitive data exposure and more) 
 
## AWS Shield
- AWS Shield is managed DDoS (Distributed Denial of Service) protection service that safeguards applications running on AWS 
- What is a DDoS attack? A malicious attempt to disrupt normal traffic by flooding a website a large amount of fake traffic 
- All AWS customers benefit from the automatic protections of AWS Shield Standard, at no additional charge 
- When you route traffic through Route 53 or CloudFront you are using AWS Shield Standard 
- Protects you against Layer 3 (Network), 4 (Transport) and 7 (Application) attacks 
 
## AWS Direct Connect 
- Gives you a private, dedicated connection not shared with anyone else
- Gives the lowest amount of latency possible with the highest amount of security possible
- Allows you to establish a completely private and dedicated fibre connection form your data centre to AWS
- Provides a physical line that connects your network to your AWS VPC.

## Amazon Guard Duty 
- How do we detect if someone is attempting to gain access to our AWS account or resources?
- Guard Duty is a threat detection service that continuously monitors for malicious, suspicious activity and unauthorised behaviour. It uses Machine Learning to analyse the following AWS logs: 
- CloudTrail Logs 
- VPC Flow Logs 
- DNS logs

## Key Management Service (KMS) 
- A managed service that makes it easy for you to create and control the encryption keys used to encrypt your data.  
- KMS is a multi-tenant HSM (Hardware Security Module)
- Many AWS services are integrated to use KMS to encrypt your data with a simple checkbox 
- KMS uses Envelope Encryption
 
## Amazon Macie 
- Macie is a fully managed service that continuously monitors S3 data access activity for anomalies and generates detailed alerts when it detects risk of unauthorised access or inadvertent data leaks. 
- Macie works by using Machine Learning to Analyse your Cloud Trail logs 
- Macie has a variety of alerts 
- Macie’s will identify your most at-risk users which could lead to a compromise. 

## Security Groups Vs NACLs 
- Security Groups – Act as a firewall at the instance level. Implicitly denies all traffic. You create Allow rules. E.g., allow an EC2 instance access on port 22 for SSH
- NACLs (Network Access Control Lists – Act as a firewall at the subnet level. You create Allow and Deny rules. E.g., block a specific IP address known for abuse

# Architecting 

## Well-architected framework: 
- https://aws.amazon.com/architecture/well-architected/

## Fiver pillars of the framework
- Operational excellence
- Security
- Reliability
- Performance efficiency
- Cost optimization

## Fault Tolerance
- Remain operational even if components fail
- Built-in redundancy of an application’s components

## High-Availability
- A concept for the whole system
- “Always” functioning and accessible
- Without human intervention
- HA Service Tools:
- Elastic Load Balancer
- Elastic IP Addresses
- Amazon Route 53
- Auto Scaling
- Amazon CloudWatch

## Organisations and Accounts 
- Useful for isolating different departments and what they have control of

# Pricing and Support

## Core concepts in billing
- Pay as you go: No up front expenses
- Pay less when you reserve: Reserved instances cost less
- Pay even less per unit by using more: Tiered pricing for services such as S3, EC2 etc. Data transfer in is always free of charge.
- Pay even less as AWS grows
 
## Consolidated Billing 
- A feature turned on by default when you are using AWS organisations 
- All billing information is sent to the master account 
- Offered at no additional cost
- Can use Cost Explorer to view usage across the account 
- Volume discounts: the more you use something the more you will save
 
## Cost Explorer 
- AWS cost explorer lets you visualise, understand, and manage your AWS costs and usage overtime. If you have multiple AWS accounts within an AWS organisation, cost will be consolidated in the master account.
- Forecasting allows you to view future costs 
- Useful for consolidated billing

## AWS Budgets 
- Service which helps you plan service usages, service costs and instance reservations. (billing alarms on steroids)
- First two budgets are free each budget is $0.02 per day, 20,00 budgets limit 
- Gives you the ability to setup alerts if you exceed or are approaching your defined budget. 
- Create cost, usage or reservation budgets.
- Can be tracked, monthly, quarterly or yearly. 
- Alerts support EC2, Redshift and ElastiCache reservations. 
- Can easily be managed from the AWS budgets dashboard or via the budgets API
- Get notified by chatbot or email

## TCO (Total Cost of Ownership) Calculator 
- Allows you to estimate how much you would save when moving to AWS from on-premises
- Provides you a detailed set of reports that can be used in executive presentations 
- The tool is for approximation purposes only 
- Describe your environment -> view a 3 year summary of cost comparisons

## AWS Landing Zone 
- Helps enterprises quickly set-up a secure, AWS multi-account 
- Provides you with a baseline environment to get started with a multi-account architecture 
- AWS Account Vending Machine (AVM) automatically provisions and configure new accounts via Service Catalogue Template Uses Single Sign-On (SSO) for managing and accessing accounts. 
- Main account, shared services account, log archive account, security account.
 
## AWS Resource Groups and Tagging
- Tags are words or phases that act as metadata for organising your AWS resources 
- Resource Groups are a collection of resources that share one or more tags 
- Helps you organise and consolidate information based on your project and the resource that you use. 
- Resource Groups can display details about a group of resource based on: Metrics, Alarms, Configuration Settings
- At any time, you can modify the settings of your resource groups to change what resources appear. 

## AWS Cost and Usage report 
- Generate a detailed spreadsheet, enabling you to better analyse and understand your AWS costs
- Places the reports into S3
- Use Athena to turn the report into a query able database 
- Use QuickSight to visualise your billing data as graphs

## CloudWatch
- CloudWatch displays all billing data and alarms in US-East region.
- Can set alarms based on what amount you are going to be billed and if this is over your budget. 

## CloudTrail 
- Logs all API calls (SDK – software development kits, CLI) between AWS services (who can we blame) 
- Who created this bucket?
- Who spun up that expensive EC2 instance?
- Who launched this SageMaker Notebook? 
- Detect developer misconfiguration 
- Detect malicious actors 
- Automate responses

## AWS Inspector 
- How do we prove an EC2 instance is harden? 
- Hardening – the act of eliminating as many security risks as possible 
- AWS inspector runs a security benchmark against specific EC2 instances. You can run a variety of security benchmarks. 
- Can perform both Network and Host assessments. 
1. Install the AWS agent on your EC2 instances. 
2. Run an assessment for your assessment target
3. Review your findings and remediate security issues 

## Amazon RDS Costs
- Clock hours of server time
- Database characteristics
- Database purchase type
- Number of DB instances
- Provisional storage
- No charge for backup storage of up to 100% of database storage for active databases. After terminated, the backups are charged
- Additional storage
- Requests
- Deployment type
- Data transfer

## Amazon EC2 Costs
### On-Demand
- Least commitment
- Low cost and flexible 
- Only pay per hour 
- Cannot be interrupted 
### Spot 
- Biggest Savings
- Request spare computing capacity 
- Flexible start and end times
- For non-critical background jobs
- Can handle interruptions (sever randomly starting and stopping)
### Reserved 
- Best Long-term
- Steady state or predictable usage 
- Commit to EC2 over 1-3 years 
- Can resell unused reserved instances 
### Dedicated 
- Most Expensive 
- Dedicated servers 
- Can be on-demand or reserved 
- When you need a guarantee of isolate hardware (enterprise requirements)
 
## Support Plans
- Tech support
- Third party support 
- Production system impaired/down 



