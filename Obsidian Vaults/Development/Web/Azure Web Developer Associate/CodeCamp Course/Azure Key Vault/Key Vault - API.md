#azure #az-204 

Azure Key Vault has a REST API.
Can be used for programmatically managing Azure Key Vault resources.
It allows you to perform operations such as:
- Create a key or secret
- Import a key or secret
- Revoke a key or secret
- Delete a key or secret
- Authorise user or apps to access its keys or secrets
- Monitor and manage key usage

Azure Key Vault API supports 3 different types of authentication:
1. **Managed Identities**
	- Recommended as best practise
	- Identity managed by Azure AD
2. **Service Principal and Certificate**
	- Uses a certificate
3. **Service Principal and Secret**
	- User and secret key