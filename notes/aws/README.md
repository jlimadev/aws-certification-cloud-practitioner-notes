# 📝How AWS Works

AWS is a cloud computing provider. It has services to multiple demands of any size.

### AWS Global Infrastructure

AWS has a global infra that can attend customers in multiple locations. The infra is composed by:

##### AWS Regions

- A regions is a cluster of data centers.
- They are all around the world and have names (us-east-1, sa-east-1)

##### AWS Availability Zones (AZ's)

- Availability Zones (AZ) give customers the ability to operate production applications and databases that are more highly available, fault tolerant, and scalable than would be possible from a single data center.
- Each region has many AZ. Usually 3, min 2 max 6
- Each availability zone (AZ) is one or more  discrete data centers with redundant power, networking, and connectivity
- They’re separate from each other, so that they’re isolated from disasters
- They’re connected with high bandwidth, ultra-low latency networking
- All AZs together will form a **region**

##### AWS Points of Presence/Edge Locations

- Deliver customer’s content through a worldwide network of Points of Presence (PoP) locations, which consists of Edge Locations and Regional Edge Cache servers. 
- AWS has 216 Points of Presence (205 Edge Locations & 11 Regional Caches) in 84 cities across 42 countries
- Content is delivered to end users with lower latency

##### AWS Data Centers

- Amazon Data Centers where they have the physical computers

##### AWS Local Zones

- AWS Local Zones are a new type of AWS infrastructure deployment that places AWS compute, storage, database, and other select services closer to large population, industry, and IT centers. 

