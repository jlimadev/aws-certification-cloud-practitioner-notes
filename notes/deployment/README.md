# Deploy and Managing Infrastructure at Scale

In this section we are going to understand how to deploy our workload into AWS

- [Cloud Formation](#cloud-formation)
- [Elastic Beanstalk](#elastic-beanstalk)
- [AWS CodeDeploy](#aws-codedeploy)
- [CodeCommit](#codecommit)
- [CodeBuild](#codecommit)
- [CodePipeline](#CodePipeline)
- [CodeArtifact](#CodeArtifact)
- [CodeStar](#CodeStar)
- [Cloud9](#Cloud9)

## Cloud Formation

Cloud Formation is a Declarative way to deploy our resources into AWS. It is used when you need to create and repeat an architecture in different environments, regions or AWS accounts

With cloud formation you can "say": I want a S3 Bucket, I want an EC2 instance, i want a EBS as storage to that instance and so on. Cloud formation creates everything in the right order and with the exact configuration;

Infrastructure as a Service (IaaS):

- Nothing is created by the console, it is code
- Changes can be reviewed as code review and storage in repositories

Costs:

- Each deploy resource is tagged (easy to identify and understand costs)
- You can estimate costs of resources by using a template
- Savings strategies: example: In DEVL environment destroy everything at midnight and build it up again at 7am

Productivity:

- Ability to destroy and re-create an infrastructure on the cloud on the fly
- Automated generation of Diagram for your templates!
- Declarative programming (no need to figure out ordering and orchestration)
- Leverage existing templates on the web!
- Leverage the documentation
- Supports (almost) all AWS resources

We can also use the CloudFormation Stack Designer: here we can see all the resources as a Diagram and we can see the relations between the components.

## Elastic Beanstalk

Elastic Beanstalk (EB) is a developer centric view of deploying an application on AWS. It is a Platform as a Service (PaaS).

Usually developers face a few problems dealing with AWS, but they just want to deploy the code

- Managing Infrastructure
- Configuration of databases, load balancers
- Scaling concerns

Most of the web apps have a similar architecture (ELB + ASG). With Beanstalk we can deploy using all these features but in one view, with full control of the application. You worry about the code, only.

It is a Managed Service

- Instances Configuration are made by beanstalk
- Deployment strategies are configured and made into beanstalk (Internally Beanstalk create a deployment into CloudFormation)
- Capacity Provisioning
- Load Balancing and Auto Scaling
- Application Monitoring and health monitoring (Health agent pushes metrics to cloudwatch, check the app health and publishes health events)

It Support many languages and platforms: Java, Go, NodeJS, Docker or your own platform.

Three Architecture Models:

- Single Instance deployment (good for devl environment)
- LB + ASG: Great for production and pre-production web applications
- ASG only: Great for non-web apps in production (workers)

Difference between CloudFormation and Beanstalk

- CloudFormation is IaaC and you can deploy any AWS Services and integrations
- Beanstalk is PaaS and it uses CloudFormation to deploy the Web Applications and you just need to worry about your code.

## AWS CodeDeploy

AWS Code Deploy is a tool to deploy code automatically.

- AWS CodeDeploy is a Hybrid service and can be used in Amazon EC2, AWS Fargate, AWS Lambda, and your on-premises servers.
- It does not use Beanstalk or CloudFormation behind the scenes. It is a different service.
- You must first create the servers/instances (configured) to CodeDeploy run
- By deploy code we can understand upgrade versions of our software automatically.

## AWS CodeCommit

Is a way to store the code into a Git AWS Repository. It is a competitor to GitHub.
With AWS CodeCommit we can create multiple repositories, we can easily share code into our organization and keep the versions.

- The code is automatically versioned
- It is fully managed
- Scalable & Highly Available
- Private, Secured, Integrated with AWS

## AWS CodeBuild
