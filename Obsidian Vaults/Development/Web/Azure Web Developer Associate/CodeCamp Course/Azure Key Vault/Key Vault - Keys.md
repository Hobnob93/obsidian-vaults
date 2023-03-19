#azure #az-204 

When creating a key there are three options:
- **Generate**
	- Azure will generate the key
	- You can set an activation and expiration date
		- Recommended as it forces you to refresh the keys after some time
	- Can set to use either RSA or EC
		- RSA: Rivest-Shamir-Adleman at 2048, 3072, or 4096 bit
		- EC: Elliptic-curve cryptography at P-256, P-384, P-521, or P-256K
- **Import**
	- Import an existing RSA key
- **Restore backup**
	- Restore a key from backup

You can create new versions of keys.
You can download backups of keys.
- Backups can only be restored within the same Azure subscription and within Azure Key Vault

For Premium you'll have similar options for HSM:
- Generate an RSA-HSM or EC-HSM key
- Import an RSA-HSM key