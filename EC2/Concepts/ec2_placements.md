##### What is a Placement Group?
When you launch EC2s, AWS decides where to place them in the data center (rack/server).  
A **Placement Group** is a *hint* to AWS:  
“Place my EC2s in a certain way to meet my needs.”  

It’s not new hardware → just how AWS **arranges EC2s** on racks.  

##### Types of Placement Groups

**1. Cluster Placement Group**  
- EC2s close together (same rack/switch)  
- **Benefit:** very low latency, high bandwidth  
- **Downside:** rack failure = all EC2s fail  
- **Best for:** HPC, big data analytics, ML training  
- **Example:** 10 EC2s for real-time stock trading → use **Cluster PG**  

**2. Spread Placement Group**  
- EC2s spread across different racks  
- **Benefit:** high availability (one rack failure won’t kill all)  
- **Downside:** only 7 EC2s per AZ  
- **Best for:** critical apps where servers must not fail together  
- **Example:** 7 domain controllers for auth → use **Spread PG**  

**3. Partition Placement Group**  
- Infra divided into **partitions** (racks, power, network)  
- Each partition = independent fault domain  
- **Best for:** large distributed systems (Hadoop, Kafka, Cassandra)  
- **Example:** Hadoop cluster with 3 partitions → losing one doesn’t kill all  
---
##### What is a Dedicated Host?
A **Dedicated Host** is a **physical EC2 server** in an AWS data center dedicated to your account.  
- Normal EC2 = shared hardware  
- Dedicated Host = exclusive access  
- Can launch multiple EC2s (only one instance family, e.g., **m5**)  
Think of it as renting the **whole house 🏠** vs just a room.  

##### Why Use Dedicated Hosts?
**1. Compliance & Security**  
- Needed in banking, healthcare, govt. (hardware isolation)  
- Guarantees no sharing with other companies  
- **Example:** Bank runs payment app only on Dedicated Hosts to meet **PCI DSS compliance**  

**2. Bring Your Own License (BYOL)**  
- Many vendors (MS, Oracle, SQL Server) license per **physical CPU core/socket**  
- Shared EC2 → can’t prove physical server  
- Dedicated Host → exact server known → reuse licenses, save cost  
- **Example:** IRIS UK reused **SQL Server Enterprise (48 cores)** on an **m5.24xlarge Dedicated Host** instead of paying AWS  

**3. Visibility & Control**  
- Detailed info: **sockets, cores, vCPUs**  
- See which EC2s run on which host  
- Control placement for audits & optimization  
- **Example:** IRIS UK security audits required mapping apps → Dedicated Host gave visibility  
---
##### What is a Capacity Reservation?
An **EC2 Capacity Reservation** guarantees AWS will have space for your **instance type** in a specific **Availability Zone (AZ)**.  
- You choose: **Instance type** (e.g., m5.large), **AZ** (e.g., us-east-1a), **quantity** (e.g., 5)  
- AWS “blocks” that capacity for you  
- You can launch anytime without “Insufficient capacity” errors  
- You pay whether you use it or not  
Think of it like booking **flight seats** → always reserved for you  

##### Why Use Capacity Reservations?
**1. Guaranteed Availability**  
- Peak times may cause shortage in AZs  
- Reservation ensures instances always launch  
- **Example:** IRIS UK reserved **20 × m5.large** in us-east-1a for payroll week → guaranteed  

**2. Mission-Critical Apps**  
- Apps that must not fail to scale  
- **Example:** E-commerce reserved **50 × c5.2xlarge** before Black Friday → no scaling issues  

**3. Works with Pricing Models**  
- Only guarantees capacity  
- Can combine with **On-Demand, RI, or Savings Plans**  
- **Example:** IRIS UK used **RI + Capacity Reservations** → discounts + guaranteed servers  

##### Key Difference
- **Reserved Instance (RI):** billing discount (1–3 yrs) → **no capacity guarantee**  
- **Capacity Reservation:** guarantees AZ capacity → ensures availability  
- **Dedicated Host:** entire physical server (for compliance/licensing)  
