#azure #az-204 

When you create a certificate within Key Vault, the following is created:
- Key Vault key
	- Allows key operations
- Key Vault secret
	- Allows retrieval of the certificate value as a secret
- Certificate metadata
	- Public [[X.509 Certificates - Format|certificate data]]

Certificates can be downloaded in either:
- CER format
- PEM/PFX format
	- Based on the content type you chose when generating the certificate OR when deciding on the [[Key Vault - Certificate Policy|policy]] (PKCS #12 or PEM)