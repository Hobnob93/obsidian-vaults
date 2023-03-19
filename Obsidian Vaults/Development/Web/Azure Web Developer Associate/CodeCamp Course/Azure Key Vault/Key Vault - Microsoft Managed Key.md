#azure #az-204 

Microsoft Managed Key (MMK) are keys managed by Microsoft.
They do not appear in the vault.
In most cases, are used by default for many Azure services.

Customer Managed Key (CMK) are keys you create in Azure Key Vault.
You need to select a key from a vault for various services.

Sometimes "customer managed" means the customer has *imported* cryptographic material.
Generated or imported keys are considered as CMK in Azure.

In order to use a key, an Azure service needs an identity (within Azure AD) for permission to access they key from the vault.

**Infrastructure encryption** is sometimes an option.
By default, Azure encrypts storage account data at rest.
Infrastructure encryption adds a second layer of encryption to your storage account's data.
See [[Key Vault - Double Encryption]].