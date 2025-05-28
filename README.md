# aws-control-policies
Contains basic Service and Resource Control Policies for use in AWS Organisations

## Introduction
## Service Control Policies and Resource Control Policies
Analysis
…
# Service Control Policies
## Prevent deletion or modification of CCS_TechOps_Admin role
[link](iam_role_deletion_protection.json)

## Prevent launching EC2 instances without IMDSv2
[link](prevent_imdv2_ec2s.json)
https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps_examples_ec2.html#example-ec2-2 

## Prevent launching EC2 instances without EBS encryption
[link](prevent_unencrypted_ebs.json)

## Deny access to AWS based on the requested AWS Region
[link](restrict_regions.json)
https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps_examples_general.html#example-scp-deny-region 

# Resource Control Policies

## Restrict access to only HTTPS connections to your resources
All buckets
https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_rcps_examples.html

## Consistent Amazon S3 bucket policy controls
All buckets
Encryption by default 
https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_rcps_examples.html 