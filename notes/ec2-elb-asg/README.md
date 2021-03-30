# 💻 Elastic Load Balancing and Auto Scaling Groups

This is where we can see the power of cloud computing, because of the automacally scaling and distribution of loads with low configurations.

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
  - On AWS is easy to scale because of the [**Auto Scaling Groups**]() and [**Load Balancer**]()
  - A few analogies:
    1. Add more instances to our application run (Scale out)
    2. Hire multiple temporary employees to handle with workload. As soon the load is lower you can dismiss them and keep your default number of employees.

**High Availability**: Means that your application is available in multiple locations, in this case that our service running in multi availability zones.

- High Availability means to run our app/system in at least two different AZs
  - This means more Security, Disaster Recover, Keep the work running.
  - To do it in AWS we have ASG and ELB that are multi-az.
- A few analogies:
  1. asdfa
  2. This company has employees in three different cities in the country. So if anything stops one branch, the other two still are working and can handle the workload.
