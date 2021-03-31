# 📝S3 - Simple Storage Service

S3 stands to Simple Storage Service and it is one of the main services of AWS. S3 is a Regional service. This service is basically "Infinity Scaling" storage.

### S3 Use cases:

- Backup and Storage
- Disarter Recovery (copying data in multiple regions)
- Archive data
- Application Hosting / Web site hosting (static websites uses Amazon S3 as backbone)
- Media Hosting
- Data Lakes & Big Data Analytics
- Software delivery
- Many AWS services uses Amazon S3 as integration/storage as well, such as [EBS Snapashots](../ec2-instance-storage/README.md/#EBS-Snapshots).

### S3 Buckets

Amazon S3 allows people to store `objects` (files) in `buckets` (directories).

- Buckets must have a unique name (across all regions and accounts)
- Buckets must be created inside a specific Region.
- Naming Convention: To give a name to the bucket must follow this naming convention
  - No uppercase, No underscore, 3-63 characters long, Not an IP, Must start with lowercase letter or number"
