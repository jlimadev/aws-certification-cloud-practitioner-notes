# 📝Security and Compliance

- [AWS Shared Responsibility Model](#aws-shared-responsibility-model)
- [Shield]()
- [WAF]()
- [Penetration Testing]()
- [KMS]()
- [CloudHSM]()
- [Artifact]()
- [GuardDuty]()
- [Inspector]()
- [Config]()
- [Macie]()
- [CloudTrail]()
- [AWS Security Hub]()
- [Amazon Detective]()
- [AWS Abuse]()
- [Root user privileges]()

## AWS Shared Responsibility Model

AWS responsibility - Security **of the Cloud**:

- Infrastructure (hardware, software, facilities and network)
- Managed Services like S3, DynamoDB, RDS

Customer Responsibility - Security **in the Cloud**:

- For EC2 instance, customer is responsible for management of the guest OS
  (including security patches and updates), firewall & network configuration, IAM
- Encrypting application data

Shared controls:

- Patch Management, Configuration Management, Awareness & Training

<p align="center" width="100%"><img src="assets/shared-responsibility.jpg" alt="drawing" width="500"/></p>

RDS examples of shared responsibility

- AWS responsibility:
  - Manage the underlying EC2 instance, disable SSH access
  - Automated DB patching
  - Automated OS patching
  - Audit the underlying instance and disks & guarantee it functions
- Your responsibility:
  - Check the ports / IP / security group inbound rules in DB’s SG
  - In-database user creation and permissions
  - Creating a database with or without public access
  - Ensure parameter groups or DB is configured to only allow SSL connections
  - Database encryption setting

S3 examples of shared responsibility

- AWS responsibility:
  - Guarantee you get unlimited storage
  - Guarantee you get encryption
  - Ensure separation of the data between different customers
  - Ensure AWS employees can’t access your data
- Your responsibility:
  - Bucket configuration
  - Bucket policy / public setting
  - IAM user and roles
  - Enabling encryption

[UP](#-security-and-compliance)
