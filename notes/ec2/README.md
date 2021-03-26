# 📝EC2 - Elastic Cloud Compute

- EC2 is one of the most popular of AWS services. EC2 extends to Elastic Compute Cloud and is a service where you can rent virtual servers from AWS. This Cloud Computing is from Infrastructure as a Service (IaaS) type.
- EC2 is a Region Scoped Service.

### How to Create a Basic EC2 Instance

To create an EC2 Instance we need to follow the bellow steps on EC2 Console:

- Select an AMI (Amazon Machine Image). It is the operating system. (most common is Amazon Linux 2 and it is free tier)
- Select the Instance Type. It is the server hardware configurations (t2-micro is free tier)
- Configure Instance Details if you want to change anything. In this case, we can create the `user data` to instance, that is the code start to it. Bellow a script to print hello world on our instance.

```bash
#!/bin/bash
# Use this for your user data (script from top to bottom)
# install httpd (Linux 2 version)
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>Hello World from $(hostname -f)</h1>" > /var/www/html/index.html
```

- Create the storage: It is data disk available in our instance and it is customizable. By default Whenever you launch an EC2 instance, the instance store volume type is ephemeral (Amazon EC2 instance store)

- Create a Security Group (SG) and add a rule to HTTP allows access from anywhere, `Port 80 and Source 0.0.0.0/0, ::/0`

- Finally Review and Launch. (Save the Key/Par Generated). A few seconds later the instance will be available and accessible.

- When finish it, just stop/terminate the instance.

---

### EC2 Instance Types

**AWS has the following naming convention:**
m5.2xlarge

- m: instance class
- 5: generation of the instance (AWS improve them over time)
- 2xlarge: the size of the instance. (Memory, CPU, etc... )

There are a few [instance types](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instance-types.html):

**General Purpose**:

- Great for a diversity of workloads such as web services and code repositories.
- Use cases: Small and midsize databases, Data processing tasks that require additional memory, Caching fleets.
- This one have a good balance between the compute, memory and networking.
- t2.micro is an example

**Compute Optimized**:

- Great for compute-intensive workloads that require high performance processors.
- Services such as Batch processing, media transcode, High performance web servers, High performance compute (HPC), Scientific modeling and Machine Learning or Dedicated Gaming Servers.
- For now, all the Compute Optimized Instance have naming starting with _C_, like c5.large.

**Memory Optimized**:

- These types have fast performance for workloads that require in-memory processing.
- Use cases: High-performance, relational (MySQL) and NoSQL (MongoDB, Cassandra) databases. Distributed web scale cache stores that provide in-memory caching of key-value type data (Memcached and Redis). In-memory databases using optimized data storage formats and analytics for business intelligence (for example, SAP HANA). Applications performing real-time processing of big unstructured data (financial services, Hadoop/Spark clusters). High-performance computing (HPC) and Electronic Design Automation (EDA) applications.

- Most of the instances of this type starts with _R_ (that remembers RAM). We also have instances starting with _X_.

**Storage Optimized**

- Made for storage-intense tasks that require high, sequential Read and Write access to large data sets on local storage
- Use cases: High Frequency Online Transaction Processing (OLTP) systems, Relational and NoSQL databases, Cache for in-memory database (like Redis), Data warehousing, Distributed file systems.

**Accelerated Computing**:

- This one use hardware accelerators, or co-processors, to perform functions such as floating point number calculations, graphics processing, or data pattern matching, more efficiently than is possible in software running on CPUs.
