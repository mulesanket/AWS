## S3 Scenario #1 — Secure Cross-Account Ingestion + Lifecycle Governance

### Business Context
IRIS UK’s payroll team needs a secure bucket to ingest monthly reports from a vendor account.
Data must be encrypted, non-public, owned by IRIS (not the uploader), and retained for 7 years
with automatic tiering to Glacier. Auditors require access logs and least-privilege access.

### Architecture (at a glance)
- **Account A (Vendor)** → uploads files
- **Account B (IRIS Prod)** → owns S3 bucket `iris-payroll-reports-prod`
- Optional: **Account C (Audit)** → read-only access to a partition `/audit/`

### Objectives (what you’ll build)
1. **Private, encrypted bucket**
   - Bucket with **SSE-KMS** (CMK), **Bucket Key enabled**, and **Block Public Access = ON**.
   - **Object Ownership: Bucket owner enforced** (ACLs disabled).

2. **Cross-account write (Vendor → IRIS)**
   - Allow a role from **Account A** to `PutObject` only under a prefix (e.g., `incoming/`).
   - Ensure **objects are owned by Account B** and **not publicly accessible**.

3. **Data governance (lifecycle + retention)**
   - Lifecycle: `incoming/` → move to **Glacier Instant Retrieval** after 30 days,
     then to **Glacier Deep Archive** after 365 days, **expire after 7 years**.
   - Clean up **noncurrent versions** and **abort incomplete multipart uploads**.

4. **Auditability**
   - Enable **Server access logging** to a separate log bucket
     _or_ **CloudTrail data events** for the reports bucket.
   - Restrict access to logs (write-only from source, read-only for auditors).

5. **Private connectivity**
   - Enforce access via **VPC Gateway Endpoint for S3** (deny requests that don’t come via the endpoint).

6. **Least-privilege consumer access**
   - Create an **IRIS application role** that can only `GetObject` from `processed/` prefix.
   - Create an **Audit role (Account C)** that can list/read only `/audit/` and nothing else.

---

## Acceptance Criteria (how you’ll know it’s done)
- Upload from **Account A** to `incoming/` succeeds; object **owner = Account B**.
- Public access checks show **no public ACLs or policies**; `aws:SecureTransport` enforced.
- Lifecycle transitions occur on schedule (verify storage class changes on sample objects).
- **Access logs** or **CloudTrail data events** capture uploads/reads with correct principals.
- Access via **VPC endpoint** works; direct public internet access is denied by policy.
- The **app role** can read only `processed/`; the **audit role** can read only `audit/`.

---

## Real Issues to Reproduce (and then fix)
1. **“Uploader owns the object” problem**
   - Symptom: Account B can’t read/delete vendor uploads.
   - Goal: Fix by enforcing bucket owner ownership without changing uploader code.

2. **Unexpected S3 charges from abandoned multipart uploads**
   - Symptom: Cost spike in Storage Lens / Cost Explorer.
   - Goal: Abort incomplete multipart after N days and verify cleanup.

3. **Blocked access due to KMS key policy**
   - Symptom: AccessDenied (kms:Decrypt) when reading encrypted objects cross-account.
   - Goal: Adjust **KMS key policy** for the specific roles without over-permitting.

---

## Evidence to Capture (for your portfolio/readme)
- Redacted screenshots: Bucket properties (encryption, Block Public Access, Object Ownership).
- Policy snippets: bucket policy, KMS key policy (principals redacted), lifecycle JSON.
- Logs/screens: CloudTrail data event showing cross-account PutObject, access logs sample.
- Storage class timeline screenshots proving lifecycle transitions on a test object.
- Short note on each “issue → root cause → fix”.

---

## Guardrails & Constraints
- **No public access** anywhere.
- **IAM least privilege** (scope to ARNs/prefixes; avoid wildcards).
- **Separate log bucket**; logs not in the same bucket as data.
- **Versioning enabled** before uploads (so lifecycle rules for noncurrent versions apply).

---

## What to tell interviewers (talk track)
- “We onboarded a third-party uploader (separate account) safely using **bucket-owner-enforced** ownership and a tight **bucket policy** limited to a prefix.”
- “We implemented lifecycle to **Glacier IR + Deep Archive** and proved transitions with timestamps.”
- “We enforced **VPC endpoints** + **HTTPS-only** and captured **CloudTrail data events** for audit.”
- “We hit a KMS decrypt error cross-account and fixed it by adjusting the **key policy** for only the necessary roles.”

