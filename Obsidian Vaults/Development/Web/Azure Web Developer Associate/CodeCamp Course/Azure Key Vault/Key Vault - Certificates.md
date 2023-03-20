#azure #az-204 

Azure Key Vault allows you to import, generate, and manage [[X.509 Certificates - Introduction|x.509 Certificates]].
Key Vault partners with certificate issuer providers for TLS/SSL:
- DigiCert
- GlobalSign

You can generate self-signed certificates or through a certificate authority.
No need to manage the security of the private key; Azure Key Vault takes care of that.
Allows a certificate owner to create a policy that directs Key Vault to manage the lifecycle of a certificate.
Allows certificate owners to provide contact information for notifications about lifecycle events, such as expiration or renewal of certificates.
Supports automatic renewal with selected issuers.
- Key Vault partner x.509 providers/certificate authorities