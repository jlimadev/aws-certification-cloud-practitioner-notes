# 💻 Elastic Load Balancing and Auto Scaling Groups

This is where we can see the power of cloud computing, because of the automacally scaling and distribution of loads with low configurations.

- [Scalability & High Availability](#scalability--high-availability)
- [Scalability vs Elasticity (vs Agility)](#scalability-vs-elasticity-vs-agility)
- [Elastic Load Balancer (ELB)](#elastic-load-balancer-elb)
- [Auto Scaling Groups (ASG)](#auto-scaling-groups-asg)

### Scalability & High Availability

**Scalability**: Scalability is linked but is different from High Availability, Scalability means that the appliation or system can handle different amounts of load by adapting. There are two different kinds of scalability:

- **Vertical Scalability**: Means increasing the size of the instance:

  - Add more resources (like CPU power, RAM, Storage, etc...).
  - It is limited due the hardware limitations.
  - It is recommended to non-distributed systems as Databases.
  - Scale Up (increasing) or Scale Down (decreasing)
  - A few analogies:
    1. Instead of using a t2.micro, use a t2.large (increasing)
    2. Instead of have a Junior employee, we hire a Senior employee because him can handle more workloads and solve it faster.

- **Horizontal Scalability (elasticity)**: Means increasing the number of instances or systems to our application.
  - Have no limitations, we can always add more instances
  - Implies to distributed systems and web apps/modern apps
  - In AWS **Scale Out** means increasing the number of instances and **Scale In** meanns decreasing the number of instances.
  - On AWS is easy to scale because of the [**Auto Scaling Groups**](#auto-scaling-groups-asg) and [**Load Balancer**](#elastic-load-balancer-elb)
  - A few analogies:
    1. Add more instances to our application run (Scale out)
    2. Hire multiple temporary employees to handle with workload. As soon the load is lower you can dismiss them and keep your default number of employees.

**High Availability**: Means that your application is available in multiple locations, in this case that our service running in multi availability zones.

- High Availability means to run our app/system in at least two different AZs
  - This means more Security, Disaster Recover, Keep the work running.
- A few analogies:
  1. To do it in AWS we have ASG and ELB that are multi-az.
  2. This company has employees in three different cities in the country. So if anything stops one branch, the other two still are working and can handle the workload.

### Scalability vs Elasticity (vs Agility)

- **Scalability**: is the ability for a system to accommodate a larger load by making the hardware stronger (vertical scale, scale-up) or by add nodes (horizontal scale, scale-out).

- **Elasticity**: Once the system is scalable, elasticity means that there will be some "auto-scaling" so that system can scale based on the load. This is "cloud-friendly": pay-per-use, match demand, optmize costs.

- **Agility**: (not related to scale - distractor), new IT resources available very quickly. (one click away, what used to happen in weeks)

### Elastic Load Balancer (ELB)

Elastic Load Balancer are managed by AWS and they are servers that forward the internet traffic to multiple servers (EC2 Instances). They are the _backend of EC2 Instances_. The ELB is what will be exposed to the users and when receive the connection/access it will redirect traffic to instances.

**Why use a Load Balancer?**

- Spread the load accross multiple downstream instances.
- Expose a single point of access (DNS) to our application.
- Handle with failures of instances (Regular health checks to the instances)
- Provide SSL termination (HTTPS) for our websites
- High Availability across zones

**Why use a Elastic Load Balancer?**

### Auto Scaling Groups (ASG)
