# 🎲 Database and Analytics

Storing data on disk (EFS, EBS, S3, EC2 Instance Store) can have limits, so if we need to store data with some structure or definition, we may want to use database.
What is a database:

- Can structure the data
- Can build indexes to perform queries/search through the data
- Can define relationship between datasets.

Databases are optimized for a purpose and come with different features, shapes and constraints, thats why exists multiple types of databases:

- [Relational Databases](#relational-databases)
- [NoSQL Databases](#noSql-databases)
- [Databases and Shared Responsibility on AWS](#Databases-and-Shared-Responsibility-on-AWS)

---

## Relational Databases

- Use table to each Entity, the tables have attributes
- We can create a relationship between the tables by using keys (Primary Key/Foreign Key/Indexes)
- Looks like an excel spreadsheet, with link (relationship) between them.
- We can use the SQL (Structured Query Language) to perform queries

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

---

## Databases and Shared Responsibility on AWS

AWS Manages the databases, it has multiple benefits:

- Quick Provisioning, High Availability, Vertical and Horizontal Scaling
- Automated Backup & Restore, Operations, Upgrades
- Operating System Patching is handled by AWS
- Monitoring, alerting

We can have our own database (and others technologies) in EC2 Instances, but we must handle and manage it (the resiliency, backup, patching, high availability, fault
tolerance, scaling)

---
