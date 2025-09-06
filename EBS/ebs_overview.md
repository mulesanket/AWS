------------------------
AWS: Elastic Block Store
------------------------
- AWS Elastic Block Store (EBS) provides durable, high-performance block-level storage volumes that you can attach to Amazon EC2 instances, acting like virtual hard drives. Key features include persistence (data remains even if an instance is shut down), various volume types for different workloads (SSD and HDD-backed), reliable EBS snapshots for backups, and the ability to dynamically attach, detach, and scale volumes to meet changing storage needs.
- EBS volumes are automatically replicated within a specific Availability Zone (AZ) for durability and protection against component failures. 

EBS Volume Types:
------------------
- Amazon EBS (Elastic Block Store) offers different volume types optimized for specific workloads, allowing you to balance performance and cost. These types fall into two categories: SSD-backed volumes for transactional, IOPS-intensive applications and HDD-backed volumes for throughput-intensive, large-data workloads.

- SSD-backed volumes
General Purpose SSD (gp3 and gp2): 
gp3 is recommended for various workloads and offers configurable performance, while gp2 is a previous generation where performance scales with size up to 16,000 IOPS. gp2 smaller volumes can burst to 3,000 IOPS.
Provisioned IOPS SSD (io2 Block Express and io1): These provide high performance for mission-critical applications. io2 Block Express is the highest performance option with high IOPS and durability. io1 is the first generation, suitable for demanding database workloads. 

- HDD-backed volumes Throughput Optimized HDD (st1): 
Offers low-cost storage and high throughput for frequently accessed large workloads.
Cold HDD (sc1): Provides the lowest cost per GB for infrequently accessed data like backups, with lower throughput than st1. 
When selecting an EBS volume type, consider performance requirements, cost, access patterns, and durability needs. More details can be found on Amazon EBS Volume Types. 