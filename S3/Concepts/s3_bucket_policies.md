# Amazon S3 – Key Concepts

## 🟦 Object Ownership & ACLs

### 1. ACLs Disabled (Recommended)
- All objects in the bucket are **owned by the bucket owner**, regardless of who uploads them.
- Access is managed only via **IAM policies, bucket policies, and SCPs**.
- Simplifies management and avoids confusion from per-object ACLs.

**Real-world example**:  
If a partner account uploads logs into your bucket, you automatically own them. No need to manage ACLs.

### 2. ACLs Enabled
- Objects are owned by the **uploader’s AWS account**.
- You may need ACL permissions from that account to read/delete objects.
- Legacy approach; not recommended.

**Real-world example**:  
A consultant uploads files to your bucket → you may not have access until they set ACLs correctly.

### 3. Bucket Owner Enforced
- Works when ACLs are disabled.
- Ensures **bucket owner always owns all objects**.
- ACLs are completely ignored.

**Analogy**: Any file dropped in your “drawer” (bucket) automatically belongs to you.

---

## 🟦 Block Public Access

### Block All Public Access = ON (Recommended)
- Prevents the bucket and its objects from being exposed to the internet.
- Overrides any ACLs or bucket policies that try to allow public access.
- Ideal for **private data, backups, internal apps**.

**Real-world example**:  
You store invoices or customer data. Even if someone misconfigures permissions, AWS won’t allow the bucket to become public.

### Block All Public Access = OFF
- Allows you to selectively make buckets/objects public via bucket policies or ACLs.
- Needed only for **public-facing buckets** like static websites or software downloads.

**Real-world example**:  
You host a static website (HTML/CSS/JS) in S3. You intentionally turn off Block Public Access to allow the world to see it.

---

## 🔑 Summary

| Setting                   | Behavior | When to Use |
|---------------------------|----------|-------------|
| **ACLs Disabled**         | Bucket owner owns all objects | ✅ Best practice |
| **ACLs Enabled**          | Uploader owns their objects | ⚠️ Legacy, avoid |
| **Bucket Owner Enforced** | Bucket owner enforced, ACLs ignored | ✅ Strongest |
| **Block Public Access ON**| No public access possible | ✅ Default/safe |
| **Block Public Access OFF**| Allow public content | ⚠️ Use only if serving public data |


# Amazon S3 – Bucket Policies

## 🔹 What is a Bucket Policy?
- A **bucket policy** is a **resource-based JSON policy** attached directly to an Amazon S3 bucket.  
- It controls **who (Principal)** can access the bucket, **what actions (Action)** they can perform, and **on which resources (Resource)**.  
- Works alongside **IAM identity-based policies**, but applies rules at the bucket level.  

👉 Think of it as **rules posted on the bucket itself**.

---

## 🔹 Key Components of a Bucket Policy
- **Version** → Policy language version (`"2012-10-17"` is always used).  
- **Statement** → One or more permission blocks.  
- **Effect** → `"Allow"` or `"Deny"`.  
- **Principal** → The user, AWS account, or `*` (public).  
- **Action** → What actions are allowed/denied (e.g., `s3:GetObject`).  
- **Resource** → The bucket and/or objects the rule applies to.  
- **Condition** → Optional filters (IP, HTTPS, encryption, etc.).  

---

## 🔹 Example 1: Deny Non-HTTPS Requests
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "DenyInsecureAccess",
      "Effect": "Deny",
      "Principal": "*",
      "Action": "s3:*",
      "Resource": [
        "arn:aws:s3:::my-secure-bucket",
        "arn:aws:s3:::my-secure-bucket/*"
      ],
      "Condition": {
        "Bool": {
          "aws:SecureTransport": "false"
        }
      }
    }
  ]
}
