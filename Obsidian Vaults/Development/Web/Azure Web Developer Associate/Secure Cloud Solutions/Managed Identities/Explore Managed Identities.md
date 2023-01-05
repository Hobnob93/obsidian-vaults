#azure #az-204 

## Overview
Provides identities for apps when connecting to Azure resources supporting [[About Azure Active Directory|AAD]] (Azure Active Directory).
Apps may use managed identity to obtain Azure AD tokens.

## Types of Managed Identities
There are two types of managed identities:
- __System-assigned managed identity__
	- Enabled directly on Azure service instance
	- When enabled, Azure creates identity for the instance in the Azure AD tenant trusted by the subscription of the instance
	- When created, credentials are provisioned to the instance
	- Lifecycle of this identity is tied to the instance it is enabled on
		- If instance is deleted, credentials and identity are automatically cleaned up by Azure
- __User-assigned managed identity__
	- Created as a standalone Azure resource
	- Azure creates an identity in the Azure AD tenant trusted by the subscription in use
	- 
