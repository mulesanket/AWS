##### What is EC2 in AWS?
**Amazon EC2 (Elastic Compute Cloud)** lets you rent **virtual servers (instances)** on AWS.  
- Launch a **virtual server** in minutes instead of buying physical ones  
- Choose **CPU, memory, storage, OS** (Linux/Windows)  
- Pay only for actual usage (**per sec/min/hr**)  

##### Key Features
- **Scalability** – Handle load via **Auto Scaling**  
- **Flexibility** – Instance types (e.g., **t2.micro**, **m5.large**)  
- **Security** – Control via **Security Groups**, **IAM Roles**  
- **Integration** – Works with **S3, RDS, Load Balancer, CloudWatch**  

##### Pricing Options
- **On-Demand** – Pay-as-you-go  
- **Reserved** – Commit **1–3 yrs** for discounts  
- **Spot** – Cheapest, but can be reclaimed  
- **Savings Plan** – Flexible discount commitment  

##### Example Scenarios
- **Web Hosting** → Website on **Linux EC2** with Apache/Nginx  
- **Dev/Test** → Temporary test servers  
- **Big Data** → EC2 clusters for **analytics**  
- **Gaming** → Host **multiplayer servers**  
---
##### AWS Instance Types & Families
| **Family** | **Optimized For**       | **Example Use Case**                       |
|------------|--------------------------|--------------------------------------------|
| **T/M (General)** | Balanced workloads       | Web apps, dev/test, microservices |
| **C (Compute)**   | High CPU                 | Web servers, analytics, encoding |
| **R/X/Z (Memory)**| Large memory             | Databases, caching, in-memory analytics |
| **I/D/H (Storage)**| High storage & IOPS     | Data warehousing, NoSQL DBs |
| **P/G/F (Accel.)** | GPUs, hardware accel.   | AI/ML, graphics, FPGA workloads |
---
##### EC2 Pricing Models
**1. On-Demand Instances**  
- **Pay-as-you-go** (per sec/min/hr depending on OS)  
- No upfront or long-term commitment  
- **Best for:** short-term, unpredictable workloads, testing, dev, POCs  
- **Example:** “We used On-Demand EC2 during performance testing because we only needed servers for a few hours.”  

**2. Reserved Instances (RI)**  
- Commit **1 or 3 yrs** → up to **72% discount** vs On-Demand  
- Payment: no upfront / partial upfront / all upfront  
- **Best for:** stable workloads, prod apps (24x7)  
- **Example:** “For our main app servers, we used Reserved Instances to save costs since those servers run 24x7.”  

**3. Spot Instances**  
- Bid on unused capacity → up to **90% cheaper** than On-Demand  
- Risk: AWS can terminate anytime (**2-min warning**)  
- **Best for:** fault-tolerant workloads, batch jobs, big data, CI/CD agents  
- **Example:** “For Jenkins CI/CD build agents, we used Spot Instances to save cost since jobs can restart without impacting production.”  

**4. Savings Plans**  
- Flexible discount model → commit to spend **$X/hr** for 1–3 yrs  
- Works across **instances, regions, Fargate, Lambda**  
- Types:  
  - **Compute Savings Plan** – flexible, covers EC2/Fargate/Lambda  
  - **EC2 Instance Savings Plan** – family/region specific, bigger savings  
- **Best for:** predictable compute spend with flexibility  
- **Example:** “At IRIS UK, we used Compute Savings Plans to cover both EC2 and Fargate since workloads were distributed.”  
---
##### What is an Amazon Machine Image (AMI)?
An **Amazon Machine Image (AMI)** is a **blueprint/template** for EC2 instances.  
It includes:  
- **Operating System** (Linux/Windows)  
- **Pre-installed software**  
- **Configuration & permissions**  
When launching an **EC2 instance**, you must **choose an AMI first**.  
