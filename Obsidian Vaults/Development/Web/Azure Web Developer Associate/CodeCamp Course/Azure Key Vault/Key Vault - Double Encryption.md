#azure #az-204 

Using two layers of encryption mitigates threads that come with encrypting data.

### Storage Accounts
Uses **Infrastructure Encryption**.
- By default, Azure encryptions storage account data at rest
- Infrastructure encryption adds a second layer of encryption to your storage account's data

### Azure Disks
Uses **Double Encryption**.
- Where two or more independent layers of encryption are enabled to protect against compromises of any one layer of encryption.

### Data-At-Rest
- Disk encryption using customer-managed keys
- Infrastructure encryption using platform-managed keys

### Data-In-Transit
- Transit encryption using Transport Layer Security (TLS) 1.2
- Additional layer of encryption provided at the infrastructure layer