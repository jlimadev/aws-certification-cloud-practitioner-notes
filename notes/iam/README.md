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
