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
  
