# Account Management, Billing and Support

- [AWS Organizations](#aws-organizations)
- [Multi Account Strategies](#multi-account-strategies)
- [Service Control Policy](#service-control-policy)
- []()
- []()
- []()
- []()

## AWS Organizations

It is a global service that allows to manage multiple AWS Accounts. The main account is the Master account and the other are the child accounts.

- It has an API to automate the creation of child accounts.
- Since we can have multiple accounts, we can restrict actions within them with SCP (Service Control Policies)

Cost Benefits of AWS Organizations:

- Consolidate Billing across all accounts - which generates a single payment method
- Benefits of aggregated usage (use massive volumes of services generates discounts)
- Shared (pooling) EC2 Reserved Instances for optimal savings.

## Multi Account Strategies

We have various modes to create accounts in AWS:

- per Department
- per Environment (DEVL, QUAL, PROD)
- based on regulatory restrictions (using Service Control Policy)
- for better isolation (using different VPC per account)
- to have separate per account service limits
- account for loggings
- use Organization Units (OU)

<p align="center" width="100%"><img src="assets/organizational-units.jpg" alt="organizational-units" width="500"/></p>

Besides this strategies, we can also monitor all accounts by:

- using tags standards to billing purposes
- enable CloudTrail in all accounts to monitor all API Calls and send it to central S3 account
- enable cloudwatch logs to central account logging

## Service Control Policy

Service Control Policy (SCP) allows us to create Whitelist or Blacklist to IAM actions. We can apply it on Organization Unit (OU) or Account Level.

- **Does not apply to the root account**
- SCP is applied to all users and roles of the account (even the root user of the account)
  - Example: a rule saying that X account cannot create EC2 instances. Not even the root user of the account can create it.
- Must have EXPLICIT allow to any service, by default nothing is allowed.
- Deny in a higher level has precedence

The use cases for Service Control Policy (SPC):

- Restrict access to specific services
- Enforce PCI compliance by explicitly disabling services

Example of Service Control Policy:

<p align="center" width="100%"><img src="assets/service-control-policy.jpg" alt="service-control-policy" width="700"/></p>

- Here we have our root Organizational Unit (OU) and the master account. The root OU allows all services, and there is a DenyAccessAthena SCP on master account. This deny will not work, because the master account is not affected by SCP.
- Inside our root OU we have a PROD OU that explicitly deny redshift access (DenyRedshiftAccess). It will make all accounts inside it to not have access to redshift, even the Account A that tries to access Redshift with a AuthorizeRedshift SCP. But the higher one is a deny and it has precedence in this case.
- HR OU has no access to redshift and has no access to Lambda (due DenyAWSLambda SCP)
- Finance OU has no access only to Deny

Example of SCP allowing access to all resources but not to DynamoDB in all accounts.

```JSON
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowsAllActions",
      "Effect": "Allow",
      "Action": "*",
      "Resource": "*"
    },
    {
      "Sid": "DenyDynamoDB",
      "Effect": "Deny",
      "Action": "dynamodb:*",
      "Resource": "*"
    }
  ]
}
```
