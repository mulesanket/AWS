## AWS Secrets Manager

### What is AWS Secrets Manager?
- A fully managed service for storing, rotating, and accessing **secrets**.  
- **Secrets** = credentials, API keys, tokens, certificates, etc.  
- Integrates with **RDS, DynamoDB, EC2, Lambda, ECS, EKS**, and basically anywhere you need credentials.  
- You can control access with **IAM policies**.  
- Secrets are encrypted with **AWS KMS** by default.  

---

### Key Features
- **Centralized secret storage** (no hardcoding in code/repos).  
- **Automatic rotation** (e.g., auto-change DB passwords every 30 days).  
- **Fine-grained access control** (IAM-based).  
- **Auditing with CloudTrail** (who accessed what, when).  
- **SDK/CLI integration** (apps fetch secrets at runtime).  
