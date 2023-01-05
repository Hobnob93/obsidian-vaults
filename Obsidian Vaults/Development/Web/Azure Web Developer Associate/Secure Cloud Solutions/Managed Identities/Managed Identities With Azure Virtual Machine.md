#azure #az-204 

## How a System-Assigned Managed Identity Works with an Azure Virtual Machine
1. [[Explore Azure Resource Manager|Azure Resource Manager]] (ARM) receives request to enable the identity on a VM
2. ARM creates service principal in [[About Azure Active Directory|Azure Active Directory]] (AAD) for the identity of the VM.
	- Principal is created in AAD tenant trusted by subscription
3. ARM configures identity on VM by updating Azure Instance Metadata Service identity endpoint with principal client ID and certificate
4. Use service principal information to grant VM access to Azure resources
	- To call ARM, use role-based access control in AAD to assign appropriate role to VM service principal
	- To call Key Vault, grant code access to specific secret or key in the vault
5. Code running on VM can request a token from Azure Instance Metadata service endpoint
	- Accessible only from the VM: `http://169.254.169.254/metadata/identity/oauth2/token`
6. A call is made to AAD to request access token using client ID and certificate
7. AAD returns a [[JSON Web Tokens|JSON Web Token]] (JWT) access token
8. Your code sends access token on a call to a service that supports AAD authentication

## How a User-Assigned Managed Identity Works With an Azure Virtual Machine
