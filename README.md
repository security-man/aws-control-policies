# aws-control-policies
This repository contains basic Service Control Policies and Resource Control Policies for use in AWS Organisations to harden your AWS estate.

[Service Control Policies](#service-control-policies)(SCPs) are a type of organisation policy that you can use to manage permissions in your organisation. SCPs offer central control over the maximum available permissions for the <ins>IAM users and IAM roles</ins> in your organisation. SCPs help you to ensure your accounts stay within your organisation’s access control guidelines. SCPs do not grant permissions to the IAM users and IAM roles in your organisation. No permissions are granted by an SCP. An SCP defines a permission guardrail, or sets limits, on the actions that the IAM users and IAM roles in your organisation can perform.

[Resource Control Policies](#resource-control-policies)(RCPs) are another type of organisation policy that you can use to manage permissions in your organisation. RCPs offer central control over the maximum available permissions for <ins>resources</ins> in your organisation. RCPs help you to ensure resources in your accounts stay within your organisation’s access control guidelines. RCPs alone are not sufficient in granting permissions to the resources in your organisation. No permissions are granted by an RCP. An RCP defines a permissions guardrail, or sets limits, on the actions that identities can take on resources in your organisation. 

For SCPs and RCPs, the administrator must still attach identity-based policies to IAM users or roles, or resource-based policies to resources in your accounts to actually grant permissions.

# Service Control Policies
## Prevent deletion or modification of CCS_TechOps_Admin role
The policy ['iam_role_deletion_protection.json'](scps/iam_role_deletion_protection.json) ensures that IAM roles of a specific name cannot be deleted or modified by any IAM user once created. This control aims to prevent local IAM users / roles from deleting or modifying cross-account administrator roles. This is useful in the event of a sub-account compromise to prevent would-be attackers from revoking administrator access to system administrators.

## Prevent launching EC2 instances without IMDSv2
The policy ['prevent_imdv2_ec2s.json'](scps/prevent_imdv2_ec2s.json) ensures that EC2 instances cannot be launched with Instance Metadata V1 (IMDV1). Instead, only IMDV2 is allowed (IMDV1 is known to be vulnerable and is only persisted as an option for legacy purposes).

## Prevent launching EC2 instances without EBS encryption
The policy ['prevent_unencrypted_ebs.json'](scps/prevent_unencrypted_ebs.json) ensures that EC2 instances cannot be launched with unencrypted EBS volumes.

## Deny access to AWS based on the requested AWS Region
The policy ['restrict_regions.json'](scps/restrict_regions.json) ensures that REGIONAL resources cannot be deployed outside of eu-west-2 or eu-west-1 (such regions can be modified according to your specific business needs).

# Resource Control Policies
## Restrict access to only HTTPS connections to your resources
The policy ['enforce_https_on_networks.json'](rcps/enforce_https_on_networks.json) ensures that access to STS, S3, SQS, SecretsManager, and KMS resources only occurs on encrypted connections over HTTPS (TLS). This can help to prevent potential attackers from manipulating network traffic.

## Enforced S3 encryption-in-transit
The policy ['enforce_https_s3.json'](rcps/enforce_https_s3.json) ensures that both internal and external access to S3 objects must be performed only on encrypted connections with a minimum protocol standard of TLSv1.2. This can help to prevent potential attackers from manipulating communications both to / from an S3 endpoint.

## Enforced S3 encryption-at-rest
The policy ['enforce_s3_object_encryption.json'](rcps/enforce_s3_object_encryption.json) ensures that all objects stored within any S3 buckets must be encrypted at rest using an encryption key managed through AWS KMS.