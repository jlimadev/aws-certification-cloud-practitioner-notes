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

- [1st Pillar - Operational Excellence](#1st-pillar---operational-excellence)
- [2nd Pillar - Security](#2nd-pillar---security)
- [3rd Pillar - Reliability](#3rd-pillar---reliability)
- [4th Pillar - Performance Efficiency](#4th-pillar---performance-efficiency)
- [5th Pillar - Cost Optimization](#5th-pillar---cost-optimization)
- [Summary](#Summary)

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

## 2nd Pillar - Security

Security includes the ability to protect the information, applications and assets while delivering business value trough risk assessment and mitigation strategies. It will also save costs from avoidable disasters and failures.

Design Principles:

- Implementing a Strong Identity Foundation: Centralized Privileges and Management. Rotate credentials often.
- Enable Traceability: integrate logs and metrics with systems to automatically respond and take actions.
- Apply security at all layers:
- Automate security best practices
- Protect data in transit and at rest - Encryption, tokenization, and access control
- Keep people away from data - eliminate or reduce the need of direct access to manual data processing
- Prepare for security events - Run incident response simulations and use tools with automation to increase your speed for detection, investigation, and recovery

<p align="center" width="100%"><img src="assets/2nd-pillar-security.jpg" alt="2nd-pillar-security" width="700"/></p>

## 3rd Pillar - Reliability

Ability of a system to recover from infrastructure or service disruptions,
dynamically acquire computing resources to meet demand, and mitigate
disruptions such as misconfigurations or transient network issues.

**Design Principles**:

- Test recovery procedures: Use automation to simulate different failures or to recreate
  scenarios that led to failures before
- Automatically recover from failures: Anticipate and remediate failures before they occur
- Stop guessing capacity: Auto scaling whenever is possible (Horizontal scaling) Load Balancing (Distribute requests across multiple, smaller resources to ensure that they don't share a common point of failure)
- Management changes through automation: Use automation to make changes to infrastructure

<p align="center" width="100%"><img src="assets/3rd-pillar-reliability.jpg" alt="3rd-pillar-reliability" width="700"/></p>

## 4th Pillar - Performance Efficiency

Includes the ability to use computing resources efficiently to meet system requirements, and to maintain that efficiency as demand changes and technologies evolve.

Design Principles:

- Democratize advanced technologies - Advance technologies become services and hence you can focus more on product development
- Go global in minutes - Easy deployment in multiple regions
- Use serverless architectures - Avoid burden of managing servers
- Experiment more often - Easy to carry out comparative testing
- Mechanical sympathy - Be aware of all AWS services

<p align="center" width="100%"><img src="assets/4th-pillar-performance-efficiency.jpg" alt="4th-pillar-performance-efficiency" width="700"/></p>

## Summary

- **1st Pillar - Operational Excellence**: Ability to run and Monitor applications/systems while deliver business value + improvement through time. (Have great operations)
- **2nd Pillar - Security**: Ability to protect the data, applications and assets + risk management. (Make secure environments)
- **3rd Pillar - Reliability**: Ability to recover from infrastructure issues and scale/get elastic to meet demand. (Ensure the application runs no matter what)
- **4th Pillar - Performance Efficiency**: Meet system requirements and maintain efficiency while adapting to technologies (Adapting and providing the best performance and look for new technologies)
- **5th Pillar - Cost Optimization**:
