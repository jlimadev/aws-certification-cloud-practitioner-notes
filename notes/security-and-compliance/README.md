# 📝Security and Compliance

- [AWS Shared Responsibility Model](#aws-shared-responsibility-model)
- [AWS Shield](#amazon-shield) [Standard and Advanced, layer 3 and 4]
- [AWS Web Application Firewall](#aws-web-application-firewall) [WAF, layer 7]
- [Penetration Testing](#penetration-testing)
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

<p align="center" width="100%"><img src="assets/shared-responsibility.jpg" alt="shared-responsibility" width="500"/></p>

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

  ## AWS against DDoS Attack

  In a Distributed Denial of Service (DDoS) attack, an attacker uses multiple sources—such as distributed groups of malware infected computers, routers, IoT devices, and other endpoints—to orchestrate an attack against a target. This is a example of how we can get protected into AWS using firewall and other security services.

  <p align="center" width="100%"><img src="assets/ddos.jpg" alt="ddos" width="500"/></p>

- AWS Shield Standard: protects against DDOS attack for your website and applications, for all customers at no additional costs
- AWS Shield Advanced: 24/7 premium DDoS protection
- AWS WAF: Filter specific requests based on rules
- CloudFront and Route 53:
  - Availability protection using global edge network
  - Combined with AWS Shield, provides attack mitigation at the edge

## AWS Shield

AWS Shield Standard:

- It is a free service available for every AWS Customer and it provides a protection from common attacks such as SYN/UDP floods, reflection attacks and other layer 3 and 4 attacks (tcp/ip). It can be deployed on HTTP friendly services (ALB, API Gateway, CloudFront)

AWS Shield Advanced:

- It is a option DDoS mitigation ($3000 month/organization) and it protects against the most sophisticated attacks on EC2, ELB, CloudFront, Global Accelerator and Route53. It is a high level defense.
- 24/7 access to AWS DDoS response team (DRP)
- Protect against higher fees during spikes of DDoS

## AWS Web Application Firewall

WAF protects our web apps from common web exploit attacks (layer 7, http).

- Define a Web Access Control List (Web ACL):
  - Rules can include IP addresses, HTTP headers, HTTP body or strings
  - protection from common attacks (SQL Injection and Cross-Site Scripting)
  - Size constraints, geo-match (block a few countries)
  - Rate-based rules (count occurrence of events) - this one is against DDoS attacks

## Penetration Testing

AWS customers are welcome to carry out security assessments or penetration tests against their AWS infrastructure without prior approval for 8 services. For any other simulated events, contact aws-security-simulatedevent@amazon.com.

This kind of testing can be done for 8 services:

- Amazon EC2 instances, NAT Gateways, and Elastic Load Balancers
- Amazon RDS
- Amazon CloudFront
- Amazon Aurora
- Amazon API Gateways
- AWS Lambda and Lambda Edge functions
- Amazon Lightsail resources
- Amazon Elastic Beanstalk environments

And we have some Prohibited Activities such as:

- DNS zone walking via Amazon Route 53 Hosted Zones
- Denial of Service (DoS), Distributed Denial of Service (DDoS), Simulated DoS, Simulated DDoS
- Port flooding
- Protocol flooding
- Request flooding (login request flooding, API request flooding)

[Read more](https://aws.amazon.com/security/penetration-testing/)

[UP](#security-and-compliance)
