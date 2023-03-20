#azure #az-204 

A certificate has metadata attached to it.
This metadata is publicly readable, so anyone is able to review and validate the authenticity of the certificate.
Some of the properties within the metadata includes:
- **Version Number**
	- The version of the x.509 standard
- **Serial Number**
	- A unique serial number assigned to the certificate by the CA
- **Signature Algorithm ID**
	- Algorithm used to sign the certificate e.g. RSA or DSA
- **Issuer Name/Organisation**
	- Name of the Certificate Authority that issued the certificate e.g. Amazon
- **Validity Period**
	- Start and end datetime during which the certificate is valid
- **Subject**
	- Identifier for the individual or organisation cert was issued to
- **Subject Public Key**
	- The public key that is meant to be authenticated by this certificate
	- This field also names the algorithm used for public-key generation
- **Issuer Unique Identifier**
	- Allows multiple CAs to operate as logically a single CA
- **Subject Unique Identifier**
	- Allows multiple cert holders to act as a single logical entity
- **Extensions**
	- Allows a CA to associate additional private information to a certificate
	- Not to be confused with [[Key Vault - Certificate Extensions|certificate file extensions]]

All of the certificate public metadata is *hashed* to produce a single hash "fingerprint".
The hash is signed by a private key to produce a *signature*.
The certificate itself is made up of:
- Metadata
- Signature
- Public key