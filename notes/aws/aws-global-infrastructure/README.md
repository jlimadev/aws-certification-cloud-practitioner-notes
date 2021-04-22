# 🌎 AWS Global Infrastructure

When we are talking about Global Infrastructure we can understand multiple geographic locations. On AWS This could be Regions and/or Edge Locations.

Benefits of Multiple Geographic Locations:

- Decreasing Latency: less latency between communications and packages transfers. (eg. From Brazil to Japan, it surely will have latency), deploy applications closer to the users (Edge Locations)
- Disaster Recovery (DR): Infrastructure is resilient to disasters, fail-over strategies (move to another region)
- Attack Protection: It is harder to attack a distributed infrastructure

AWS Infrastructure consists in:

- Regions: For deploying applications and infrastructure
- Availability Zones: Made of multiple data centers
- Edge Locations (Points of Presence): for content delivery as close as possible to users

Global Services to Decrease Latency and Improve Availability -[Route53](#route53)

## Route53

It is a Managed DNS (Domain Name System) of AWS.
DNS is a collection of rules and records which helps clients understand how to reach servers through URLs. DNS records examples:

```
• www.google.com => 12.34.56.78 == A record (IPv4)
• www.google.com => 2001:0db8:85a3:0000:0000:8a2e:0370:7334 == AAAA IPv6
• search.google.com => www.google.com == CNAME: hostname to hostname
• example.com => AWS resource == Alias (ex: ELB, CloudFront, S3, RDS, etc…)
```

### Route 53 Routing Policies

- **Simple Routing Policy**: A client (web browser) request through an URL and Route 53 resolves and responds an IP. This one does not have health checks.

  - Example: Web Browser -foo.com---> Route 53 (receives)
    <-11.22.1.2- Route 53 (responds)

- **Weighted Routing Policy**: client (web browser) request through an URL and Route 53 resolves and multiples IPs with a weight to each one. And since we have multiple instances, Route 53 perform health checks.

  - Example: 20% of the users will get response from server 1, 30% of the users will get response from server 2, 50% of the users will get response from server 3. It is like a Load Balancing

- **Latency Routing Policy**: This Latency Routing Policy is made to reduce latency by understanding WHERE is the request coming from, and it will make sure to send a response from the closest server.

  - Example: We have an application global application published in South America (Brazil) and Europe (France). Our users are around the globe, so if we receive an request from Argentina it will get the response from the server in South America.

- **Failover Routing Policy**: We have two instances, main instance and failover instance, if the main one fails it will redirect automatically to the failover instance. It performs health checks on the main instance.

## Summary

- Route 53: Great to route users to the closest deployment with least latency and good for disaster recovery strategies.
- CloudFront: Replicate part of your application to AWS Edge Locations and cache common requests (less latency)
- S3 Transfer Acceleration: Accelerate S3 Downloads and Uploads
- AWS Global Accelerator: Improve Global Availability and Performance of your apps.
