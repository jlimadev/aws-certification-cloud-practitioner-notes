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

- Simmilar to Memory optimized, but this one use hardware accelerators, or co-processors, to perform functions such as floating point number calculations, graphics processing, or data pattern matching, more efficiently than is possible in software running on CPUs.

---

### Security Groups (SG)

- They are fundamentaal of newtwork security in AWS. Theys control how traffic is allowed into our EC2 instances. It is the Firewall of the instance.
- They contain only **Allow** rules
- Reference by IP or by other Security Group
- Regulate the Access to the Ports, Authoirized IP ranges (IPV4 and 6)
- Control of inbound network (from outside to inside the instance)
- Control of outbound network (from instance to outside) - by default, all traffic outbound (from our instance to the rest of the world) is allowed.
- Common Ports that we need to know

```
22 - SSH (Secure Shell) - log into EC2 Linux instance
22 - SFTP - (Secure File Transport Protocol) - upload file using SSH
21 - FTP (File Transfer Protocol) - upload files into a file share
80 - HTTP - access unsecured websites
443 - HTTPS - access secured websites
3389 - RDP (Remote Desktop Protocol) - Log into a windows instance
```

### SSH and Instance Connect

- SSH is one of the most important function. It allows you to control a remote machine, uptade, and lots of configurations, all using the command line.
- Mac, Linux and Win 10+ = SSH and Windows <10 = Putty

```bash
# check permissions on .pem file (must be chmod 0400)
# and then log using ssh:

ssh -i permissionsfile.pem ec2-user@ec2-public-ip
```

- **EC2 Instance Connect** is an Second Option to run SSH directly from Console. It runs a browser based SSH instance connection/terminal. In this case a temporary Key is uploaded to EC2 instance by AWS. Works only out-of-the-box with Amazon Linux 2.

- Remember to Allow port 22 in Security Group.

### EC2 Instance Roles

In order to run or access aws services, usually in our terminal we would use `aws configure`and pass our credentials. But in EC2 instance it is not a good practice, since it is a server and can be managed by more than one person. So if you want to EC2 to performe an action in other services in our behalf, we need to create a role to this EC2.

- For example: if we want to execute the command `aws iam list-users` we need to create a role to that contains the IAM Policy, in this case, the read user permission. To do it we need to create the policy and the role in our IAM Console and after that, in EC2 console, attach the role to the EC2 instance. Now our instance can perform this list-users action without require your secret keys directly inside the server.

### EC2 Instances Purchasing Options

EC2 Instances in the cloud, the default type of EC2 is on-demand instances.

**On-demand instances**

- No commiment to user to specific time.
- Full control over the life-cycle of instance: when start, stop, etc.
- Pay only for the seconds that the instance is on state Running.
- Recommend to short workloads and irregular runnings that cannot be stoped until finish.

**Reserved Instances**:

- Minimum commitment of one year, maximum of three years.
- Can buy a instance that runs in one specifc Region [Regional] or Specifc Zone [Zonal] - it affects the price.
- There are three kinds of reserved instances:

1. **Reserved Instances**: for long workloads and always use the selected type of instance during the commitment time. (use case: host a database)
2. **Convertible Reserverd Instances**: long workloads with flexible instances (can change the type of the instance over time)
3. **Scheduled Reserverd Instances**: When you need to use the instance only in scheduled time. For example: when you need to use the instance every monday from 6am to 11am for one year.

About the prices: A Standard Reserved Instance provides a more significant discount than a Convertible Reserved Instance.

| Action                                       | Standard Reserved Instance | Convertible Reserved Instance                                                                  |
| -------------------------------------------- | -------------------------- | ---------------------------------------------------------------------------------------------- |
| Modify Instance                              | Modify Attributes          | Modify Attributes                                                                              |
| Exchanging Reserved Instances                | Can't be exchanged.        | Can be exchanged during the term for another Convertible Reserved Instance with new attributes |
| Selling in the Reserved Instance Marketplace | Can be sold.               | Can't be sold.                                                                                 |
| Buying in the Reserved Instance Marketplace  | Can be bought.             | Can't be bought.                                                                               |
