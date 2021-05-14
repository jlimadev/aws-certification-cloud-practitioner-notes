# AWS Architecting & Ecosystem

AWS Well Architected Framework has general guiding principles to be applied:

- Stop guessing capacity of our needs and start scaling our services
- Test our systems at scale
- Automate to make architectural experimentation easier (using cloudformation, beanstalk, or other for example)
- Allow for evolutionary architectures designing based on changing requirements (using IaaS)
- Drive architectures using data
- Improve through game days: Simulate applications for flash sale days

## AWS Cloud Best Practices – Design Principles

- Scalability: vertical & horizontal
- Disposable Resources: servers should be disposable & easily configured
- Automation: Serverless, Infrastructure as a Service, Auto Scaling…
- Loose Coupling: Monolith are applications that do more and more over time, become bigger. So we need to Break it down into smaller, loosely coupled components. So, a change or a failure in one component should not cascade to other components.
- Services, not Servers: Don’t use just EC2, use managed services, databases, serverless, etc.

# Well Architected Framework

The Well Architected Framework has five Pillar:

- [1st Pillar - Operational Excellence]()
- [2nd Pillar - Security]()
- [3rd Pillar - Reliability]()
- [4th Pillar - Performance Efficiency]()
- [5th Pillar - Cost Optimization]()

## 1st Pillar - Operational Excellence

A well architected framework with Operational Excellence includes the ability to run and monitor the applications to deliver value to the business and continually improve supporting processes and procedures.

The design principles:

- Perform Infrastructure as a Code (IaaC) - CloudFormation
- Documentation - Automate the creation of annotated docs after every build
- Make frequent, small and reversible changes: this will avoid issues in case you need to rollback
- Refine operations procedures frequently
- Anticipate failures and learn from them all

AWS Services to Operational Excellence:

- Prepare phase: Use CloudFormation to have the IaaC, AWS Config to evaluate compliance
- Operate: CloudFormation and AWS Config to perform the resources configuration and AWS CloudTrail and CloudWatch to monitor how it is going and if anything is gone manually
- Evolve: AWS CloudFormation and CI/CD Tools allows to evolve quickly

<p align="center" width="100%"><img src="assets/1st-pillar-operational-excellence.jpg" alt="1st-pillar-operational-excellence" width="700"/></p>
