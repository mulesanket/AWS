--------------------------
VERSIONING IN S3
--------------------------
Amazon S3 Versioning is a feature that enables the storage of multiple versions of an object within a single S3 bucket. 
This functionality allows for the preservation, retrieval, and restoration of every version of an object, providing a robust mechanism for data recovery and compliance.

How S3 Versioning Works:
-------------------------
Enabling Versioning:
Versioning is enabled at the bucket level. Once enabled, it applies to all objects within that bucket.

> Version IDs:
When versioning is enabled, S3 automatically assigns a unique version ID to each object stored in the bucket. This ID distinguishes different versions of the same object. 

> Storing Multiple Versions:
When an object is uploaded to a versioning-enabled bucket, if an object with the same key already exists, S3 does not overwrite the existing object. Instead, it creates a new version of the object with a new version ID, while the previous version remains accessible.

> Delete Markers:
When an object in a versioning-enabled bucket is deleted, S3 does not permanently remove the object. Instead, it places a "delete marker" as the current version. This marker indicates that the object is logically deleted, but previous versions remain available for recovery. 
To permanently delete an object and its versions, the delete marker and specific versions must be explicitly removed. 

> Retrieval and Restoration:
Users can retrieve specific versions of an object by referencing their unique version ID. This allows for restoration of previous states of an object, recovering from accidental deletions or overwrites.

