#azure #az-204 

RBAC helps you manage who has access to Azure resources.
Determines what they can do with those resources.
Determines what areas they have access to.

**Role Assignments** are the way you control access to resources.
They consist of 3 elements:
1. Security principal
2. Role definition
3. Scope

Azure RBAC includes over 70 built-in roles.

##### Security Principal
Represents the identities requesting access to an Azure resource, such as:
- **User**
	- An individual who has a profile in [[CodeCamp - Azure Active Directory|Azure Active Directory]]
- **Group**
	- A set of users created in Azure Active Directory
- **Service Principal**
	- A security identity used by applications or services to access specific Azure resources
- **Managed identity**
	- An identity in Azure AD that is automatically managed by Azure

##### Role Definition
A collection of permissions.
It determines the operations that can be performed by the user.
Roles can be high-level, like "Owner", or specific like "VM Reader".
Azure has built-in roles, but you can define your own.

There are 4 fundamental Azure role definitions:
- **Owner**
	- Read, Grant, Create, Update, Delete
- **Contributor**
	- Read, Create, Update, Delete
- **Reader**
	- Read
- **User Access Administrator**
	- Grant

##### Scope
The set of resources that access for the Role Assignment applies to.
Scope Access Controls at the Management, Subscription, or Resource Group level.