# acloudguru-aws-cda
Study Notes From https://acloud.guru Certified Developer Associate Course

Released June 2018

Can Skip
 - IAM
 - EC2
 - Parts of Chapter 5 (serverless, alexa)

## Exam Blue Print
  - Scoring - 100-1000, min passing 720
      - Deployment - 22%
      - Security - 26%
      - Development w/ AWS Services - 30%
      - Refactoring - 10%
      - Monitoring and Troubleshooting - 12%
  - Length - 120 Minutes, 65 Questions
  - Cost - $150USD

## White Papers
  - Understand Blue/Green Deployments

## Exam Tips  
  - Always use roles over having secret access key/secret

## IAM
  - Users - real people
  - Groups - collection of users
  - Roles - assignable to resources
  - Policy - defines permissions (JSON), can be attached to users groups and roles

username/password are used to log into the web console
accesskey/secretaccesskey - programatic access

### iam exam tips
  - IAM is universal
  - Root account - email you registered with
  - New users have **NO PERMISSIONS** by default
  - Know how to read JSON policies going into exam

## EC2 - Elastic Cloud Compute
Scale Up - Bigger/Beefier (quality) boxes
Scale Out - Get more (quantity) boxes
user data - bootstrap scripts for EC2 instances, run at root level
ec2-user - default user on ec2 instance
roles can be applied while ec2 instance running, they are applied immidiately

- Pricing Options
  - On Demand
  - Reserved - contract 1 or 3 years
    - Standard
    - Convertible
    - Scheduled
  - Spot - bid pricing
  - dedicated hosts - physical machine dedicated to you

  Instance Types
  F - field programable gate array
  I - high speed storage
  G - graphics
  H - high throughput
  T - lowest cost (cheap)
  D - dense storage
  R - ram
  M - main choice
  C - compute optimized
  P - gPu
  X - xtreme memory

  ### EBS - Elastic Block Storage
  Disk in the cloud, attachable to EC2
  Root volume is where OS installed

  Types
  - General Purpose - balance price + performance, <= 10,000IOPS
  - Provisioned IOPS - relational dbs, > 10,000IOPS
  - Throughput Optimized - big data, log processing, not boot volumes
  - Cold HDD - Lowest cost, think file server
  - Magnetic - legacy, lowest cost of bootable types

  Create a volume from encrypted snapshot, the volume will be encrypted
  Create a volume from an unencrypted snapshot, the volume will be unencrypted
  You can created encryted volumes
  root device volume can be encrypted by an OS level application, or creating a snapshot -> create a copy of the snapshot and select encrypt -> create image
  **ebs volume has to be in same az as ec2 instance**

### ELB - Elastic Load Balancer
 - Application Load Balancer - Layer 7 - HTTP/S routing, URL matching/routing
 - Network Load Balancer - Layer 4 - Latency, extreme performance
 - Classic Load Balancer - Layer 4 & 7 - HTTP/S, TCP, sticky sessions

 You can have multiple SSL certs per application load balancer

### Route53
AWS DNS service
Alias record - points to AWS resources
Naked domain - aka Apex record - domain.com (no www)

### RDS - Relational Database Service
DBs available
 - MSSQL
 - ORACLE
 - MySQL
 - PostgreSQL
 - Amazon Aurora - Compatible with MySQL and PostgreSQL
 - MariaDB

Types of Backups
1. Automated Backups - Point In Time (1-35 days) - daily backup with transaction logs during the day (1 second) - enabled by default
1. Snapshot - Always done manually

To Encrypt an Existing DB you must create a snapshot, then make a copy with the encryption setting set.

Multi AZ - Disaster Recovery
Read Replica - Performance

 OLTP vs OLAP
 OLTP - Online Transaction Processing - Pulls up a row of data (simple, frequent)
 OLAP - Online Analytics Processing - running aggregate queries (complex, infrequent)

 #### Working w/ RDS
  - when initially creating RDS instance you provide server identifier, db name, username, password
  - always given dns address as endpoint
  - port 3306 is sql port
  - make sure you open up ports in SGs

 ### Non-Relational Databases
 Don't have to define schema ahead of time
  - DynamoDB

 ### Data Warehousing
  - Redshift - OLAP

### Elasticache
Offload performance from EC2 or common DB queries that don't change oftent
 Types
  - Memcached - no replication, simple, scale out
  - Redis - multi AZ w/ failover, sorting/ranking, pub/sub, data persistence



### CLI - Command Line Interface
- Give users **least privilege** - minimum amount of access required
- Create groups, then assign users to groups

  ### EC2 Exam Tips
  - If spot instance is terminated by amazon, you will **not** be charged for a partial hower. However if you termate the instance yourself, you will be charged for the **complete** hour in which the instance ran
  - Remember FIGHTDRMCPX
  - Remember EBS types and what they are used for
  - always use roles over access keys

## S3 - Simple Storage Service
Object Storage
File Size - **0 Bytes** to 5TB, **single PUT request 5GB**
Unlimited Storage Capacity
S3 namespace is **universal** (https://<region>.amazonaws.com/<bucketname>)

Data Consistency
  - Read after write consistency for PUTS (creates)
  - Eventual Consistency for overwrite PUTS and DELETES

99.99% available (designed), 99.9% guaranteed
99.999999999% durable (11 x 9s)

### Performance
100 PUT/LIST/DELETE
<= 300 GET
if going over these limits use Cloudfront / Transfer acceleration
**prefix with random key names - for better IO**
**Update** 3,500 PUTS/sec, 5,500 GETS/sec meaning previous random guidance is not applicable. July 2018 Test - Possibly still using old  values. Just be aware.

### Security
- By default, all newly created buckets are **private**
- access
    - Bucket policy (JSON) - bucket level
    - Access Control List - object level
- can be configured to create access logs

### Encryption
- Encryption in Transit (SSL/TLS)
- At Rest
    1. SSE-S3 - S3 Managed Keys
    1. S3-KMS - AWS key management service
    1. SSE-C - Server side encryption with Customer Provided Keys
    1. Client Side Encryption (Encrypt before uploading)

Headers
  - x-amz-server-side-encryption
      - AES256 (SSE-S3)
      - ams:kms (SSE-KMS)

you can enforce only encrypted objects be stored by making a bucket policy to deny any PUTS w/o the header

### Tiered Storage
  - S3 - 99.99% avail, 11 x 9s durable, loss of 2 facilities
  - S3 - IA (Infrequently accessed)
  - S3 - 1 zone IA - same as IA, only 99.5% avail. Cost 20% less than regular S3 - IA
  - Reduced Redundancy storage 99.99% durable and avail - for easily reproducible data - going to be phased out, no longer recommended by aws
  - * Glacier - not really S3, but used for archives (3-5 hour retrieval)

### CORS
Must be using s3 website url
https://<bucketname>.s3-website.<region>.amazonaws.com

Lifecycle Management - surprisingly wasn't touched on in this course

### S3 Exam Tips
**Not for OS or databases**
Universal namespace
Read S3 FAQ

### Cloudfront
CDN - Content Delivery Network
Geographically distributed users
Cloudfront - Faster Downloads
S3 Transfer Acceleration - Faster Uploads
Key Terminology
  - Edge Location - where object is cached
  - Origin - S3 Bucket, EC2 instance, ELB, Route53
  - Distribution - network of edge locations
    - Web Distribution (websites)
    - RTMP (Real Time Messaging Protocol) - Media Streaming

## Serverless

### Lambda
Under the Compute Services
Event (trigger) driven compute service
Supported Languages:
  - Node.js
  - Java
  - Python
  - C#
  - Go

#### Lambda Version Control
Each lambda version has a unique arn and is **immutable**
qualified arn - has version or **$LATEST** at the end
unqualified arn - does not have version
versioning can be use to do splits between traffic
  - cannot split traffic to $latest, must first make alias to $latest and route traffic to alias

#### Lambda Exam Tips
- Scales out, not up
- Functions are independent, 1 event = 1 Function
- lambda is serverless
- know which services are support serverless
    - api gateway
    - Lambda
    - s3
    - DynamoDB
- functions can trigger other functions
- debug lambda - aws xray
- lambda can be used global resources, but live in a region
- know triggers!
    - API Gateway
    - AWS IOT
    - alexa skills kit
    - alexa smart home
    - cloudfront
    - cloudwatch events
    - cloudwatch logs
    - code commit
    - cognito sync trigger
    - DynamoDB
    - kinesis
    - s3
    - sns

### API Gateway
Features
  - Scaling
  - Throttling
  - API Key
  - CORS
API caching - caching path responses for a ttl
you can import apis from swagger files

### Step Functions

### X-Ray
