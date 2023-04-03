#azure #az-204 #az-tiers 

There are 2 types of performance tiers for storage accounts; Standard and Premium.
The higher the IOPS (I/O per second) the faster the drive can read and write.

#### Standard Performance
Stored on an HDD (Hard Disk Drive).
Varied performance based on [[Storage Accounts - Access Tiers|access tier]].
Use cases:
- Backup and disaster recovery
- Media content
- Bulk data processing

An HDD has moving parts; an arm that needs to read and write data sequentially to a disk.
It is very good at writing or reading large amounts of contiguous data.

#### Premium Performance
Stored on an SSD (Solid State Drive).
Optimised for low latency.
Higher throughput.
Use cases:
- Interactive workloads
- Analytics
- AI or ML
- Data transformation

An SSD has no moving parts, and data is distributed randomly.
This is why it can read and write so fast.