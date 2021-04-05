# 📝S3 - Simple Storage Service

S3 stands to Simple Storage Service and it is one of the main services of AWS. This service is basically "Infinity Scaling" storage.
Amazon S3 Console is a global console, that means that we can see all buckets in all regions, but the buckets itself, needs to be bound to a region.

- [S3 Use cases](#s3-use-cases)
- [S3 Buckets](#s3-buckets)
- [S3 Objects](#s3-objects)
- [S3 Create a Bucket and Add Objects](#s3-create-a-bucket-and-add-objects)

### S3 Use cases

- Backup and Storage
- Disarter Recovery (copying data in multiple regions)
- Archive data
- Application Hosting / Web site hosting (static websites uses Amazon S3 as backbone)
- Media Hosting
- Data Lakes & Big Data Analytics
- Software delivery
- Many AWS services uses Amazon S3 as integration/storage as well, such as [EBS Snapashots](../ec2-instance-storage/README.md/#EBS-Snapshots).

### S3 Buckets

Amazon S3 allows people to store `objects` (think as files) in `buckets` (think as directories).

- Buckets must have a unique name (across all regions and accounts)
- Buckets must be created inside a specific Region.
- Naming Convention: To give a name to the bucket must follow this naming convention
  - No uppercase, No underscore, 3-63 characters long, Not an IP, Must start with lowercase letter or number"

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

### S3 Create a Bucket and Add Objects

- Creating the bucket
  - In AWS Console we can create the bucket, and choose the name (Globally unique name) and the Region. We can also copy the settings from an existing bucket.
  - Choose if we are blocking Global Access (on the internet)
  - Enable versioning
  - Add Tags and Encryption
  - Click in create
- Adding Objects
  - Inside the bucket, just click in Upload (or drag and drop) and select the file.
