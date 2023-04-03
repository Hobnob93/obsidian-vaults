#azure #az-204 #az-tiers 

There are 3 types of access tiers for standard storage; Cool, Hot, and Archive.

##### Hot
Data that's accessed frequently.
Highest storage cost.
Lowest access cost.
Use cases:
- Data in active use or expected to be accessed frequently
- Data staged for processing and eventual migration to the cool access tier

##### Cool
Data infrequently accessed.
Stored for at least 30 days.
Lower storage cost.
Higher access cost.
Use cases:
- Short-term backup and disaster recovery datasets
- Older media content not viewed frequently anymore, but expected to be available immediately when accessed
- Large data sets need to be stored cost effectively while more data is being gathered for future processing

##### Archive
Data that's rarely accessed.
Stored for at least 180 days.
Lowest storage cost.
Highest access cost.
Use cases:
- Long-term backup or secondary backup
- Archival datasets
- Original (raw) data that must be preserved, even after it has been processed into a usable form
- Compliance and archival data that needs to be stored for a long time and is hardly ever accessed

### Account Level Tiering
Any blob that doesn't have an explicitly assigned tier infers the tier from the Storage Account access tier setting.

### Blob Level Tiering
You can upload a blob to the tier of your choice.
Changing tiers happens instantly with the exception of moving out of archive.

### Rehydrating a Blob
When moving a blob out of archive.
It can take several hours.

### Blob Lifecycle Management
Can create rule-based policies to transition data to different tiers.
E.g. after 30 days in hot storage, move to cool storage.

### Moving From A Cooler Tier
Operation is billed as a *write* operation to the *destination* tier.
Where write operation (per 10,000) and data write (per GB) charges of the destination tier apply.

### Moving From a Hotter Tier
Operation is billed from the source tier.
Where the *read* operation (per 10,000) and data retrieval (per GB) charges of the source tier apply.
Early deletion charges for any blob moved out of the cool or archive tier may apply as well.

### Cool and Archive Early Deletion
Any blob moved into cool tier (GPv2 accounts only) is subject to a cool early deletion period of 30 days.
Any blob moved into the archive tier is subject to an archive early deletion period of 180 days.
This charge is prorated.