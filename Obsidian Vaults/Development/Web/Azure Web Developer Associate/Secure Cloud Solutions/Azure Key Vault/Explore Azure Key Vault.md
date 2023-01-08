#azure #az-204 

## Overview
A service supporting two types of containers; ==vaults== and managed ==hardware security module (HSM) pools==.
Vaults support storing software and HSM-backed keys, secrets, and certificates.
Managed HSM pools only support HSM-backed keys.

Azure Key Vault helps solve the following:
- __Secrets Management__
	- Securely store and tightly control access to tokens, passwords, certificates, API Keys, etc.
- __Key Management__
	- Easy to create and control encryption keys used to encrypt your data.
- __Certificate Management__
	- Easily provision, manage, and deploy public and private Secure Sockets Layer/Transport Layer Security (SSL/TLS) certificates for use with Azure and internally connected resources.

There are ==two tiers==:
- __Standard__
	- Encrypts with a software key
- __Premium__
	- Includes HSM-protected keys

## Key Benefits of Using Azure Key Vault
These are some of the core benefits to using the service:
- __Centralised Application Secrets__
	- Centralised storage allows you to control distribution
	- Apps can securely access information they need using URIs
	- URIs allow apps to retrieve specific versions of a secret
- __Securely Store Secrets and Keys__
	- Access requires authentication and authorisation for the caller
	- Authentication done via [[About Azure Active Directory|Azure Active Directory]] (AAD)
	- Authorisation may be done via ==role-based access control== (Azure RBAC) or ==Key Vault access policy==
		- RBAC used when dealing with management of vaults
		- Access policy used when trying to access data stored in a vault
	- Vaults may be either software-protected or hardware protected with HSMs
		- HSMs only available with premium tier
- __Monitor Access and Usage__
	- Enable logging for vaults to monitor their activity
	- May secure logs by restricting access
	- May delete logs you no longer need
	- It can be configured to:
		- Archive to a [[Types of Storage Accounts|storage account]]
		- Stream to an [[Azure Event Hubs|event hub]]
		- Send logs to [[Explore Azure Monitor|Azure Monitor]]
- __Simplified Administration of Application Secrets__
	- Security information must be secured, follow a life cycle, and be highly available. Vaults simply the process of meeting this requirements by:
		- Removing need for in-house knowledge of HSMs
		- Scaling up on demand to meet organisation's usage spikes
		- Replicating contents of Key Vault within a region to a secondary region
			- Ensures high availability and removes need for admin to trigger any failover
		- Providing standard Azure administration options via Portal, Azure CLI and PowerShell
		- Automating certain tasks on certificates that you purchase from Public CAs, such as enrolment and renewal