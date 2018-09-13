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
  - Memcached
  - Redis

### CLI - Command Line Interface
- Give users **least privilege** - minimum amount of access required
- Create groups, then assign users to groups
  
  ### EC2 Exam Tips
  - If spot instance is terminated by amazon, you will **not** be charged for a partial hower. However if you termate the instance yourself, you will be charged for the **complete** hour in which the instance ran
  - Remember FIGHTDRMCPX
  - Remember EBS types and what they are used for
  - always use roles over access keys
  
  
