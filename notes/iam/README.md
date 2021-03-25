# 📝IAM - Identity Access Management

Identity Access Management is a Global Service.

- First we have our Root Account. This account should not be shared or even used. We must use only to Create another users, called IAM Users.
- Users are people in our organization and they can be grouped.
- The Groups only contain users. (Not allowed Group Chain).
- Groups and Users are needed, because AWS Services needs Permissions, and we create these permissions for each group or user.

### IAM Permissions

**Policies**

- Users and Groups can be assigned to JSON Documents that contains the permissions (allowing or denying).
- Policies define the permissions to users/groups.
- Apply the "Least Privilege Principle". Only give the needed permissions.

**Roles**

- Are created for another Services, so they can access or execute a process inside another service.
- Some AWS service will need to perform actions on your behalf. To do so, we will assign permissions to AWS services with IAM Roles.
- We need to create or attach policies to this Role to grant the permitions.
- CamelCaseNamed
- The most common roles: [EC2 Instance Roles, Lambda Function Roles, Roles for CloudFormation]

### IAM Account Security

AWS Provides more security abling us to add pretection mechanisms to our account.

**MFA (Multi Factor Authentication)**

- Password that you know + security device you own.
- Main benefit of MFA: if a password is stolen or hacked, the account is not compromised.
- MFA Devices: Virtual Devices (Authy, Google Authenticator), Universal 2nd Factor (U2F) Security Key, Hardware Key Fob MFA Device, Hardware Key Fob MFA Device for AWS GovCloud (US)

**Password Policy**

- Set a minimum password length.
- Require specific characters in the password: Upper/Lower, numbers, non-alphanumeric.
- Allow IAM users to change theyr passwords.
- Require password change each X days.
- Prevent password reuse.
