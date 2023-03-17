#azure #az-204 

Contains all your Azure Storage data objects:
- blobs
- files
- queues
- tables
- disks

Azure Storage offers several types of storage accounts (called *Account Kind* in the portal).
Each kind has different features with their own pricing models:
- General purpose v1 (legacy)
- General purpose v2
- BlobStorage (legacy)
- BlockBlobStorage
- FileStorage

Storage accounts vary with the following features:
- **Supported Services**
	- Determines what can be put in the storage account
	- Includes Blob, File, Queue, Table, Disk, and Data Lake Gen2
- **Performance Tiers**
	- How fast will the read and writes be
	- Standard and Premium
- **Access Tiers**
	- How often do you need quick access to a file
	- Hot, Cool, and Archive
- **Replication**
	- How many redundant copies should be made and where
	- LRS, GRS, RA-GRS, ZRS, GZRS, RA-GZRS
- **Deployment Model**
	- Who should deploy the supported services
	- Resource Manager or Classic