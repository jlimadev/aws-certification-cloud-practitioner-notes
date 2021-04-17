# ECS, Fargate and ECR

In AWS we have services to run and manage our applications into containers. In order to understand how these services works, we must first understand what is Docker.

## Docker

Docker is a software development platform to deploy apps. With docker we pack our app into a container and can be run in any OS.

Docker can run in any machine, and it brings some benefits:

- Any Machine and OS
- No compatibilities issues
- Predictable behaviors
- Less work
- Easy to maintain and deploy
- Easy to scale up and down

Inside an EC2 instance we can have multiple docker containers running: An image with node, another with java, another with mysql, etc. When our application is packed into a container it is easy to run inside the EC2.

Docker images can be stored privately or publicly: **Private** are stored into ECR (Elastic Container Registry from Amazon) and the **Public** ones are stored into Docker Hub

## Elastic Container Service:

## Fargate:

## Elastic Container Register:

---

On (CCP) practitioner level is required to understand what is the main differences between ECS Fargate and ECR.
