# 📝S3 - Simple Storage Service

S3 stands to Simple Storage Service and it is one of the main services of AWS. This service is basically "Infinity Scaling" storage.
Amazon S3 Console is a global console, that means that we can see all buckets in all regions, but the buckets itself, needs to be bound to a region.

- [S3 Use cases](#s3-use-cases)
- [S3 Buckets](#s3-buckets)
- [S3 Objects](#s3-objects)
- [S3 Create a Bucket and Add Objects](#s3-create-a-bucket-and-add-objects)
- [S3 Security](#s3-security)
  - [S3 Bucket Policy](#s3-bucket-policy)
- [S3 Static Website](#s3-static-website)
- [S3 Versioning](#s3-versioning)
- [S3 Server Access Logging](#s3-server-access-logging)
- [S3 Replication](#s3-replication)
- [S3 Storage Classes](#s3-storage-classes)
- [S3 Glacier Vault Lock and Object Lock](#s3-glacier-lock-and-object-lock)

---

### S3 Use cases

- Backup and Storage
- Disarter Recovery (copying data in multiple regions)
- Archive data
- Application Hosting / Web site hosting (static websites uses Amazon S3 as backbone)
- Media Hosting
- Data Lakes & Big Data Analytics
- Software delivery
- Many AWS services uses Amazon S3 as integration/storage as well, such as [EBS Snapashots](../ec2-instance-storage/README.md/#EBS-Snapshots).

---

### S3 Buckets

Amazon S3 allows people to store `objects` (think as files) in `buckets` (think as directories).

- Buckets must have a unique name (across all regions and accounts)
- Buckets must be created inside a specific Region.
- Naming Convention: To give a name to the bucket must follow this naming convention
  - No uppercase, No underscore, 3-63 characters long, Not an IP, Must start with lowercase letter or number"

---

### S3 Objects

The `objects` are the files to be stored in S3 Bucket.

- Objects (files) must have a Key, the key is the full path to the object:
  - The key is composed of prefix + object name
    - s3://my-bucket/**my_file.txt**
    - s3://my-bucket/**my_folder1/another_folder/my_file.txt**
  - In this first example the file has only the name, so it has not prefix. It is just 'my_file.txt'
  - In this second example, the prefix is 'my_folder1/another_folder/' and the object name is 'my_file.txt'
- There is no concept of "directories” within buckets. Just keys that contains slashes ('/').
- The objects values are the content of the body.
- Max Object size is 5TB (but can be splitted "multi-part upload" and have multiple files of 5 TB)
- The object contains Metadata: list of key/value pairs, Track data, Security and lifecycle goals
- The Object contains Tags to identify better
- Version ID (S3 Allows Versioning)

---

### S3 Create a Bucket and Add Objects

- Creating the bucket
  - In AWS Console we can create the bucket, and choose the name (Globally unique name) and the Region. We can also copy the settings from an existing bucket.
  - Choose if we are blocking Global Access (on the internet)
  - Enable versioning
  - Add Tags and Encryption
  - Click in create
- Adding Objects
  - Inside the bucket, just click in Upload (or drag and drop) and select the file.
  - We can also create folder and objects to it.

---

### S3 Security

**User Based:**

- IAM Policies - attach IAM policies to users or groups and them you be allowed to access the bucket from console/cli/sdk

**Resource Based:**

- [Bucket Policies](#s3-bucket-policy): Rules attached directly to S3 Buckets where we can allow or deny access/actions in our bucket.
- Object Access Control List (ACL) - Object level. Grant or Deny access, but this rule is attached directly to the object. More common ACL.
- Bucket Access Control List (ACL) - Bucket level. Less commom, normally use Bucket Policies.

**Encryption:** We can encrypt objects in S3 using encryption keys.

An IAM Principal can access S3 objects if:

- The IAM Permissions allows it **OR** if the Resource Policy allows. (an user that does not contain the IAM Policy to access the bucket, can access a bucket where the Resource Policy allows IAM Users)
- There is not Deny

A few exemples of usage of S3 Security:

- Your site exposed to web, by default nobody can access it, to allow it we need to create to attach the **S3 Bucket Policy** to allow the public access.
- An IAM User that already has a policy attached to the account allowing S3 access. In this case there is no need to create the S3 Bucket Policy.
- An EC2 instance wants to access our S3, so we need to create a Role to EC2 and attach the permisions(policies) to it and attach the role in our EC2. Now the instance will be able to access the bucket.
- Cross-Account-Access: For this case we may use the S3 Bucket Policy, which will allow the cross-account access.

#### S3 Bucket Policy

Bucket policies are JSON based policies, looks like the IAM Policy; In this document we need to define:

- Resources: The AWS S3 Resource. We can use, for example, the ARN like `arn:aws:s3:::jlimadev-demo-april-2021/*` to allow everything inside the resources. In this case read all objects from my bucket. (Example policy bellow)
- Action: Set of API to allow or deny (e.g. S3:GetObject)
- Effect: Allow or Deny
- Principal: Who can access?

Usually we use S3 Bucket to:

1. Grant Public Access to the bucket; (for this we must remove the public access settings on the bucket on `Block all public access` settings on bucket permissions tab)
2. To force objects to be encrypted at the upload
3. Grant access to another account (cross-account)

Public access policy exemple, generated by AWS Policy Generator:

```json
{
  "Id": "Policy1617654569293",
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Stmt1617654567141",
      "Action": ["s3:GetObject"],
      "Effect": "Allow",
      "Resource": "arn:aws:s3:::jlimadev-demo-april-2021/*",
      "Principal": "*"
    }
  ]
}
```

---

### S3 Static Website

S3 Can host static websites and have them accessible on the www.
S3 website has an URL an this URL can be public or not.

- URL structure:
  - `bucket-name`.s3-website-`AWS-region`.amazonaws.com (inside the region)
  - `bucket-name`.s3-website.`AWS-region`.amazonaws.com (outside the region)

To create an Static Web site we can upload a `index.html` in our bucket and, in Bucket Properties, activate the `static websites hosting` option.

- We cannot forget to allow all the public access to our website and create the Bucket Policy to allow internet access.
- If try to access a not public S3 Bucket, a 403 error will show up.

---

### S3 Versioning

Keep versions of the objects in S3 Bucket. Anytime we update a file, it will get a new version. Versioning is activated in bucket level. To enable it in AWS Console, we need to go in our Bucket and enable `Bucket Versioning`.

Advantages by activating the versioning feature:

- Protection to file deletion (intended or unintended).
- Restore versions of the file.
- Easy rollback to previous versions.

The file when is versioned, it keeps the same key, but Increment the key by 1.

Important to understand about versioning:

- By default, versioning is not enabled, but we can enable whenever we want.
- File onlly start to get versions when we enable this feature to the bucket.
- Files prior the versioning will get the first version as null.
- Suspending versioning will not suspend versioned files.

About deleting versioned objects:

- To delete permanently an object, we need to select the specific version to delete.
- When we delete without choosing the version, it will add a `Delete Mark` to the object. To delete permanently we need to do it in each version.
- If we want to restore an object with delete mark, we need to perform the delete action again, but in this case, it will delete the delete mark, making the the object be available.

---

### S3 Server Access Logging

It is for audit purposes, enables log access to S3Bucket. Any access (allowed, denied) will be logged into another S3 bucket.

- The logs are written in a specific bucket for logs.
- This data can be analyzed: Get errors, issues, audit, suspicious patterns.

We can enable it in our bucket properties and change the `Server access logging` and select the target bucket. So, we cannot forget to create the target bucket, where the logs will be stored.

---

### S3 Replication

We have two types of data replication: `Cross-Region-Replication (CRR)` and `Same-Region-Replication (SRR)`.

- Replicate all the content continuously to another bucket, it happens asynchronously.
- For this we must enable versioning in **Source** and **Destination** Bucket.
- The buckets can be in different accounts. (Need the prorper IAM permissions)
- The replication rule needs a IAM Role to perform the replication. It creates one automatically or we can create our own role.

Cross-Region-Replication (CRR) use cases: Compliance, lower latency access, replication cross-account.

Same-Region-Replication (SRR) use cases: log aggregation, live replication between test and prod environments.

- It does not replicate files before the replication setting be set, only new files. To replicate existing files we must re-upload or use s3 sync tool.
- If we need to deletions we also need to set this option.

---

### S3 Storage Classes
