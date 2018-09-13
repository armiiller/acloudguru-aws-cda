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
  
## EC2 - Elastic Cloud Compute
Scale Up - Bigger/Beefier (quality) boxes
Scale Out - Get more (quantity) boxes

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
  
  ### EC2 Exam Tips
  - If spot instance is terminated by amazon, you will **not** be charged for a partial hower. However if you termate the instance yourself, you will be charged for the **complete** hour in which the instance ran
  - Remember FIGHTDRMCPX
  - Remember EBS types and what they are used for
  
