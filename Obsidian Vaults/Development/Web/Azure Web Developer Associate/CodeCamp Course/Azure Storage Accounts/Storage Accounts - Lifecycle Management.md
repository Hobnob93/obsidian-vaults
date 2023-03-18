#azure #az-204 

Azure Storage lifecycle management offers a rule-based policy.
Can use to transition blob data to appropriate access tiers.
Can also use to expire data at the end of the data lifecycle.

With lifecycle management, you can:
- Transition blobs from one [[Storage Accounts - Access Tiers|access tier]] to another
- Delete blobs, blob versions, and blob snapshots at the end of their lifecycles
- Define rules to be run once per day at the storage account level
- Apply rules to containers or a subset of blobs, using name prefixes or blob index tags as filters
- Move files to cooler tiers if they haven't been used for a number of days

To manage lifecycle of blobs within a container, you need to create a lifecycle management rule.
- In Azure Storage Account go to Lifecycle Management, under Blob Service add a rule
You may apply this rule to all blobs inside storage account, or apply to blobs within account using a filter.