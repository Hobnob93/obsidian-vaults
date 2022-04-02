#azure #az-204 

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
- Only `hot` and `cool` can be set at the *account* level
- `Archive` tier can only be set at *blob* level
- Data in `cool` tier has slightly lower availability but high durability, retrieval latency and throughput similar to `hot`
- Data in `archive` is stored ==offline==!
- The `hot` and `cool` tiers support *all* [[Azure Storage Redundancy Options|redundancy options]]
- The `archive` tier *only* supports LRS, GRS and RA-GRS
- Data storage limits set at account level and *not* per tier
- Can choose to use all of this limit across all three tiers or in one tier

## Manage Data Lifecycle
*Azure Blob* storage lifecycle offers a rich, rule-based policy for *General Purpose v2* and *Blob Storage* accounts.
Use policy to transition data to appropriate access tier.
Can expire data at natural end of its lifecycle.
The lifecycle policy lets you manage:
- Transitioning blobs to "cooler" storage tiers to optimise performance and costs
- Delete blobs at end of their lifecycles
- Define rules run once a day at storage account level
- Apply rules to containers or subset of blobs

`Hot` storage preferable for young data.
`Cool` storage appropriate for occasional access.
`Archive` storage for long-term or legally required data.