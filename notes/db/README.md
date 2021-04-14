# 🎲 Database and Analytics

Storing data on disk (EFS, EBS, S3, EC2 Instance Store) can have limits, so if we need to store data with some structure or definition, we may want to use database.
What is a database:

- Can structure the data
- Can build indexes to perform queries/search through the data
- Can define relationship between datasets.

Databases are optimized for a purpose and come with different features, shapes and constraints, thats why exists multiple types of databases:

- [Relational Databases](#relational-databases)
  - [Relational Database Service - RDS](#rds---relational-database-service)
  - [Amazon Aurora](#amazon-aurora)
- [NoSQL Databases](#noSql-databases)
  - [Amazon Elasticache](#amazon-elasticache)
  - [Amazon DynamoDB](#amazon-dynamodb)
  - [Amazon DynamoDB Accelerator - DAX](#amazon-dynamodb-accelerator---dax)
- [Databases and Shared Responsibility on AWS](#Databases-and-Shared-Responsibility-on-AWS)
- [Amazon Redshift](#Amazon-Redshift)
- [Amazon Elastic MapReduce - EMR](#amazon-elastic-mapReduce---emr)
- [Amazon Athena](#amazon-athena)
- [Amazon Quicksight](#amazon-quicksight)

## Relational Databases

- Use table to each Entity, the tables have attributes
- We can create a relationship between the tables by using keys (Primary Key/Foreign Key/Indexes)
- Looks like an excel spreadsheet, with link (relationship) between them.
- We can use the SQL (Structured Query Language) to perform queries

Basically we have two ways to create Relational Databases in AWS: RDS and Aurora. They are both managed by AWS, but Aurora is a cloud native and more cloud friendly while RDS will be running known technologies directly in a managed service.

## NoSQL Databases

- NoSQL means non relational databases. They are built for a specific purpose and specific data models. They have flexible schemas for building modern applications.
- Types: Key-Value, Document, Graph, in-memory, search databases
- We can have the data in JSON (Javascript Object Notation) format (we can add new fields, nest data, support arrays, etc.)
- Benefits:
  - Flexibility: easy to evolve data model
  - Scalability: designed to scale-out by using distributed clusters
  - High-performance: optimized for a specific data model
  - Highly functional: types optimized for the data model

Example of JSON data

```json
{
  "name": "John",
  "age": 30,
  "cars": ["Ford", "BMW", "Fiat"],
  "address": {
    "type": "house",
    "number": 23,
    "street": "Dream Road"
  }
}
```

Amazon provides multiple services of NoSQL databases: Elasticache, DynamoDB, DynamoDB Accelerator

## Databases and Shared Responsibility on AWS

AWS Manages the databases, it has multiple benefits:

- Quick Provisioning, High Availability, Vertical and Horizontal Scaling
- Automated Backup & Restore, Operations, Upgrades
- Operating System Patching is handled by AWS
- Monitoring, alerting

We can have our own database (and others technologies) in EC2 Instances, but we must handle and manage it (the resiliency, backup, patching, high availability, fault
tolerance, scaling)

## RDS - Relational Database Service

RDS Stands to Relational Database Service and it is a managed DB by AWS for databases that uses SQL as query language. We can create multiple relational databases types in the cloud, fully managed by AWS:

- Postgres
- MySQL
- MariaDB
- Oracle
- Microsoft SQL Server
- Aurora (AWS Proprietary database)

Advantages of using RDS instead of using a EC2 deployed database:

RDS is a managed service:

- Automated provisioning, OS Patching
- Continuos backup options and restore to specific timestamp (Point in time to restore)
- Monitoring dashboards
- We can create scale to read data from replicas for improved read performance
- Setup Multi AZ setup (Disaster Recovery and Highly Available)
- Setup Maintenance windows for upgrades
- Scaling capability (vertical and horizontal)
- Storage in a EBS (Elastic Block Store GP2 or io1) inside an EC2 instance

**Important**: We cannot use SSH into our database instances.

Example of usage:

`Elastic Load Balance <-> EC2 Instances <-R/W-> RDS`

- The ELB will receive the web requests
- The EC2 instances doing/hosting the application logic
- RDS doing Reads and Writes

- RDS Deployment Options:
  - **RDS Read Replicas**: Here we can scale the workload of our DB, we can create up to 15 replicas. The data is written only to main DB and we can read the data from the replicas.
  - **RDS Multi-AZ**: Failover in case of AZ outage (high availability), data is read/written to main database. Can have only one other AZ as failover (the data will be replicated to failover db, that will be used only if the main db has any kind of issue)
  - **RDS Multi-Region** (read replicas): Disaster recovery strategy in case of Region issue, local performance for global reads (Example: so if we have the main db in us-east-1 and replica in sa-east-1, we can read locally from region sa-east-1 with less latency, but if we need to write, it goes to main db, in us-east-1) replications costs

RDS is good for OLTP (Online Transaction Processing)

## Amazon Aurora

It is an AWS proprietary technology (not open-source) of a Relational database. Aurora is Cloud Optimized, so it have much more performance compared Relational Database Service (RDS).

- Amazon Aurora supports Postgres and MySQL
  - Compared to RDS running a MySQL database, Aurora MySQL has 5x more performance
  - Compared to RDS running a Postgres database, Aurora Postgres has 3x more performance
- Aurora storage automatically grows in increments of 10GB, up to 64 TB.
- Aurora costs more than RDS (20% more) – but is more efficient
- Not included into Free Tier

## Amazon Elasticache

Is used to get a Redis or Memcached managed database.

- Caches are in-memory databases with high performance, low latency
- Cache databases Helps reduce load off databases for read intensive workloads, instead of use the repetitive query hitting the database, we can get common responses from our cache.
- Very readily available, easy accessible and they can relieve the pressure on main database by returning common results.
- AWS takes care of OS maintenance / patching, optimizations, setup, configuration, monitoring, failure recovery and backups.
- Keywords: In-memory database
- Architecture example:

```
Elastic Load Balance <-> EC2 Instances (possible ASG) <-R/W-> RDS
                                                      <-R/W-> Elasticache
```

## Amazon DynamoDB

DynamoDB is a fully managed and High Available NoSQL Key/Value Database with replications across 3 AZs.

- Scales to massive workloads, distributed “serverless” database (We don't need to manage any server related to this database)
- Millions of requests per seconds, trillions of row, 100s of TB of storage
- Fast and consistent in performance
- Single-digit millisecond latency – low latency retrieval
- Integrated with IAM for security, authorization and administration
- Low cost and auto scaling capabilities
- Keywords: Serverless, low-latency and single digit millisecond.

## Amazon DynamoDB Accelerator - DAX

Amazon DynamoDB Accelerator is a in-memory cache for DynamoDB and it is fully managed by AWS.
It has 10x performance improvement

- single digit millisecond latency to `microseconds` latency when accessing tables.
- Secure, highly available and high scalable

Main difference between DAX and Elasticache: DAX is used only with DynamoDB while Elasticache is used with another databases.

- Architecture example:

```
Application <-R/W-> DynamoDB Accelerator (DAX) <-R/W-> DynamoDB
```

## Amazon Redshift

Based on Postgres database, but this one is not used to `OLTP - Online Transaction Processing`, this one is used to `OLAP - Online Analytical Processing`, this type of database is for analytics and data warehousing.

Usually the exam ask what kind of database is used for analytics and data warehousing, so Amazon Redshift is the answer.

- Load data once every hour, not every second.
- 10x performance compared to others data warehouses, scale to PBs of data.
- The data is stored in Columns (columnar storage of data)
- Massive Parallel Query Execution (MPP)
- High Availability
- Pay as you go, based on the launched instances
- Has SQL interface to perform queries.
- Integrated with BI tools such as Amazon Quicksight and Tableau.

## Amazon Elastic MapReduce - EMR

EMR stands to Elastic MapReduce and it is a tool to perform big data processing and analysis by provisioning Hadoop Clusters.

- EMR helps us to create Hadoop Clusters (it can be hundreds of EC2 instances) to do big data processing and analysis
- Supports Apache Spark, HBase, Presto, Flink and others.
- EMR takes care of provisioning EC2 Instances and the configurations
- Autoscaling Groups integration
- Spot instances integration

Use Cases: data processing, big data, machine learning, web indexing...

## Amazon Athena

Amazon Athena is a serverless database to perform SQL queries on S3.

- It does not need a server to run, and for this, we don't need manage any infrastructure, so we pay only per executed query.
- Pay per query, not for database
- Used to query data in S3
- Outputs are stored in S3
- Secured by IAM

Use cases: One-time SQL queries, serverless queries on S3, log analytics.

## Amazon Quicksight

It is a serverless learning-powered Business Intelligence (B.I) service to create interactive dashboards.

Fast, auto scalable, embeddable, with per-session pricing;

Use cases: Business Analytics, Building Visualizations, Perform ad-hoc analysis, get insights using data

Fully integrated with AWS DBs: RDS, Aurora, Athena, S3, DynamoDB, Redshift
