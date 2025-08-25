----------------------
S3 LIFECYCLE POLICIES
----------------------
An Amazon S3 lifecycle policy is a set of rules that automates the management of objects stored in an S3 bucket throughout their lifecycle.
These policies help optimize storage costs and simplify data management by defining actions to be taken on objects based on their age or other criteria. 

Key aspects of S3 lifecycle policies:

> Transition Actions:
These actions define rules for moving objects between different S3 storage classes, such as transitioning from S3 Standard to 
S3 Standard-Infrequent Access (S3 Standard-IA), S3 One Zone-Infrequent Access (S3 One Zone-IA), S3 Glacier Instant Retrieval, 
S3 Glacier Flexible Retrieval, or S3 Glacier Deep Archive. 
This is typically done to move less frequently accessed data to more cost-effective storage tiers.

> Expiration Actions:
These actions define rules for automatically deleting objects after a specified period, 
either based on their creation date or when they become a noncurrent version in a versioned bucket.
This helps manage data retention and compliance requirements.

> Customization:
Lifecycle policies are highly customizable. You can apply rules to all objects in a bucket or filter them by prefix 
(e.g., objects starting with a specific name) or object tags.

> Cost Optimization:
By automatically transitioning data to cheaper storage classes and expiring unneeded objects, 
lifecycle policies significantly help in reducing S3 storage costs.

> Automation
Once configured, lifecycle policies run automatically, eliminating the need for manual intervention in managing object storage and deletion.

> Application:
Lifecycle policies apply to both existing objects in a bucket and new objects added after the policy is configured.