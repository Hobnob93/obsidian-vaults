#azure #az-204 

Azure AD Connect is a hybrid service.
It connects your on-premise Active Directory to your Azure Account.
Azure AD Connect allows for seamless Single Sign On (SSO) from your on-premise workstation to Microsoft Azure.

Azure AD Connect has the following features:
- **Password has authorisation**
	- Sign in method
	- Synchronises a hash of users on-premises AD password with Azure AD
- **Pass-through authentication**
	- Sign in method
	- Allows users to use the same password on-premise and in the cloud
- **Federation integration**
	- Hybrid environment using an on-premise AD FS infrastructure
	- For certificate renwal
- **Synchronisation**
	- Responsible for creating users, groups, and other objects
	- Ensures on-premise and cloud data matches
- **Health monitoring**
	- Robust monitoring and provides a central location to view this activity
	- Azure AD Connect Health is the central location