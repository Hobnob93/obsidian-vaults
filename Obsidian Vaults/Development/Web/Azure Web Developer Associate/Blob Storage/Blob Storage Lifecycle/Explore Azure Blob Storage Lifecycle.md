#azure #azure-wda 

# Explore Azure Blob Storage Lifecycle
Data sets have unique lifecycles.
Early in the lifecycle, the data is accessed often.
Need for access drops drastically as the data ages.
Some data stays idle in cloud and is rarely accessed once stored.
Some data expires days or months after creation.
Other data may be read and modified throughout their lifetimes.

## Access Tiers
*Azure Storage* offers [[Access Tiers for Block Blob Data|Access Tiers]], allowing you to store blob object data in a cost-effect way.

The following considerations apply to the different tiers:
- Can be sent on a blob during or after the upload
- Only `hot` and `cool` 