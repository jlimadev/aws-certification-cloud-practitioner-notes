# 💾 EC2 Instance Storage

- [EBS Elastic Block Store - Volumes](#ebs-elastic-block-store---volumes)
- [EBS Snapshots](#EBS-Snapshots)
- [EC2 Instance Store](#EC2-Instance-Store)
- [EFS Elastic File System]()
- [EC2 Storage Shared Responsibility Model]()

### EBS Elastic Block Store - Volumes

**Main Informations about Elastic Block Store**:

- An EBS Volume is a **network drive** that you can attach to your instance while they run. It uses the network to communicate with the instance, so it might have a little bit of latency.
- It can be detached from an instance and attached to other quickly (benefit of network driver)
- It Can persist data even if the instance is terminated.
- Can be mounted to one instance at a time (On CCP level exam). One instance can have more than one EBS at a time.
- They are bound to a specific availability zone, this means if your instance is in us-east1-a and your EBS is in us-east1-b, they cannot be bound to each other. To do it across AZs, we need **Snapshots** or create an EBS Volume to the same AZ.
- It have a provisioned capacity in GBs or IOPs (inputs and outputs per second). The billing is based on this capacity, and this capacity can be increased/decreased over time.

**Good to know about EBS**:

- Free tier: 30 GB of EBS on General Purpose (SSD) or Magnetic per Month.
- Analogy to a "network USB stick" that you can plug in other computers.
- We can have existing EBS volumes that keeps unattached.
- EBS Volumes are network drives with good but 'limited' performance: EC2 Instance Store have the best performance, because they are the hard disk, physical, on the data-center attached on the machine that runs the server.

---

### EBS Snapshots

Snapshot is a backup of our EBS Volumes at a point in time. It keeps available in one Region. But to use it in a volume, we need to create the volume inside an AZ.

- To Create this snapshot you don't have to detach the volume from an instance (besides it is recommended)
- With the Snapshot we can Copy to other regions or AZ's or Create a brand new EBS Volume.
- This snapshot will be a "start" to the new EBS Volume. So the new volume will start with the data starting from the snapshot. The new volume will be a Restore from a snapshot.

---

### EC2 Instance Store

This is the **physical HARD DRIVE** attached to the server. Limited space, but higher performance. It is called by **ephemeral**

- Better I/O performance. It is good to buffer/cache/scratch data/temp files. Always with short worloads.
- EC2 Instance Store lose their storage and data if they are stopped.
- Risk of losing data (because it is a physical hardware)
- Backups and Replications are our responsibility.

---
