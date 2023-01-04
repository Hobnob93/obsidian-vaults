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
Transport Layer Security (TLS) protocol is used to protected data between vaults and clients.
Clients negotiate a TLS connection with vaults.
TLS provides strong authentication, message privacy, integrity, interoperability, algorithm flexibility, and ease of deployment/usage.

Perfect Forwarded Secrecy (PFS) protects connections between client systems and MS cloud services by unique keys.
Connections also use RSA-based 2,048-bit encryption key lengths.
Both make it difficult to intercept and access data in transit.

## Other Best Practises
- __Use separate key vaults__
	- A vault per application per environment is recommended
	- Avoids sharing secrets across environments
	- Reduces thread in case of a breach
- __Control access to your vault__
	- Ensure only authorised apps and users have access to the vaults
- __Backup__
	- Create regular backups of the vaults on update/delete/create of objects within
- __Logging__
	- Turn on logging and alerts
- __Recovery options__
	- Turn on [soft-delete](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview) and purge protection if you want to guard against force deletion of a secret