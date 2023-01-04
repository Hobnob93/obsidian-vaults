#azure #az-204 

## Authentication
Need to authenticate to do any operations with Key Vault.
==Three== ways to authenticate:
- __Managed Identities for Azure Resources__
	- Assign identity (which has Key Vault access) to app deployed on Azure VM
	- Assign identities to other Azure resources
	- Benefit is app or service isn't managing rotation of the first secret
		- Azure automatically rotates service principal client secret associated with identity
	- ==Azure recommends this==
- __Service Principal and Certificate__
	- Use a service principal and associated certificate that has access to key Vault
	- ==NOT recommended by Azure==
		- Application owner or developer *must* rotate certificate
- __Service Principal and Secret__
	- Can use service principal and secret to authenticate to Key Vault
	- ==NOT recommended by Azure==
		- Hard to automatically rotate bootstrap secret used to authenticate to Key Vault

## Encryption of Data in Transit
