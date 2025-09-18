##### What is a Security Group?
A **Security Group (SG)** is a **virtual firewall** that controls **inbound** and **outbound** traffic for AWS resources (mainly EC2).  
- Works at the **instance level** (subnet-level = **NACLs**)  
- **Stateful:** if inbound is allowed, the response outbound is auto-allowed  

##### How Security Groups Work
- **Inbound rules:** define allowed traffic into instance  
  - Example: allow **SSH (22)** from office IP, allow **HTTP (80)** from anywhere  
- **Outbound rules:** define allowed traffic out  
  - Default: all outbound allowed  
- **Attached at launch:** one or more SGs can be attached  
- **Multiple SGs:** rules are cumulative (union of all)  
