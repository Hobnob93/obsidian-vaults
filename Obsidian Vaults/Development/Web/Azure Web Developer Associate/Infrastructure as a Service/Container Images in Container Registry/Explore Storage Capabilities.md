#azure #azure-wda 

# Explore Storage Capabilities
Every *ACR* [[Discover Azure Container Registry#Azure Container Registry Service Tiers|tier]] benefits from advanced *Azure* storage features:
- **Encryption-at-rest**
	- All container images automatically have this
	- Encrypted before storing
	- Decrypts on-the-fly when app and services pull the image
- **Regional storage**
	- Stores data in region where registry is created
	- Helps meet data residency and compliance requirements
	- May also store data in paired region in same geography
	- Enable geo-replication for better resiliency
- **Zone redundancy**
	- Only for ==premium== service tier
	- Replicate registry to a minimum of three separate zones in each enabled region
- **Scalable storage**
	- Create as many repositories, images, layers, or tags as you need
	- Up to the registry storage limit

Very high numbers of repositories and tags can impact performance of registry.
Periodically delete unused items; be warned they *cannot* be recovered once deleted.