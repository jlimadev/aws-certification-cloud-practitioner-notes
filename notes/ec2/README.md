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
