# Amazon S3 Storage Classes – Interview Notes

---

## S3 Standard
- Default storage class (if not specified).
- Durability: 99.999999999% (11 nines).
- Availability: 99.99% across 3+ AZs.
- Retrieval: Milliseconds.
- Cost: Highest (for frequently accessed data).

**Use cases:** Static website hosting, mobile app content, real-time log analytics.  
**Interview tip:** Use for *hot data* where latency & availability are critical.

---

## S3 Intelligent-Tiering
- For unpredictable/unknown access patterns.
- Auto moves objects between:
  - Frequent  
  - Infrequent  
  - Archive Instant  
- Monitoring fee (per 1,000 objects).
- Retrieval: Milliseconds.

**Use cases:** Data lakes, media libraries.  
**Interview tip:** Good when access patterns are unknown; no need for lifecycle rules.

---

## S3 Standard-IA
- Durability: 11 nines, multi-AZ.
- Availability: 99.9%.
- Retrieval: Milliseconds.
- Cheaper than Standard, retrieval fee applies.

**Use cases:** Compliance data, monthly reports, DR datasets.  
**Interview tip:** Best for *cold but instantly needed data*.

---

## S3 One Zone-IA
- Like Standard-IA but only in **1 AZ**.
- Durability: 11 nines (but no multi-AZ).
- Availability: 99.5%.
- ~20% cheaper than Standard-IA.

**Use cases:** Re-creatable data, secondary backups.  
**Interview tip:** Pick if cost matters and AZ failure risk is tolerable.

---

## S3 Glacier Instant Retrieval
- Archive storage, but instant retrieval.
- Durability: 11 nines.
- Availability: 99.9%.
- Retrieval: Milliseconds.
- Cheaper than Standard-IA, retrieval fee applies.

**Use cases:** Medical images, old media files.  
**Interview tip:** For rare data that must be instantly available.

---

## S3 Glacier Flexible Retrieval (former Glacier)
- Cheapest archive with flexible retrieval:
  - Expedited: 1–5 min  
  - Standard: 3–5 hrs  
  - Bulk: 5–12 hrs  
- Durability: 11 nines.
- Availability: 99.99%.

**Use cases:** Long-term archives, DR backups, regulatory docs.  
**Interview tip:** Use when *cost matters more than speed*.

---

## S3 Glacier Deep Archive
- **Cheapest class**.
- Durability: 11 nines.
- Availability: 99.99%.
- Retrieval: 12–48 hrs.
- Designed for 7–10 years retention.

**Use cases:** Govt archives, financial/legal records, historical data.  
**Interview tip:** Ideal for compliance retention (rarely accessed data).

---

## S3 Express One Zone (newest)
- High-performance, single-AZ.
- Sub-millisecond latency.
- Optimized for latency-sensitive workloads.
- Trade-off: No multi-AZ durability.

**Use cases:** High-frequency trading, AI/ML inference, low-latency delivery.  
**Interview tip:** Choose if *ultra-low latency* is more important than AZ resilience.
