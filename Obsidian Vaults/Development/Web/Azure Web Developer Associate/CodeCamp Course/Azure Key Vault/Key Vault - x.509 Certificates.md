#azure #az-204 

#### What is a Public Key Infrastructure (PKI)
PKI is a set of roles, policies, hardware, software, and procedures.
They are needed to create, manage, distribute, use, store, and revoke digital certificates.
Also to manage public-key encryption.

#### What is an x.509 Certificate?
A standard defined by the International Telecommunication Union (ITU) for public key certifications.
x.509 certificates are used in many Internet protocols:
- SSL/TLS for HTTPS
- Signed and encrypted email
- Code Signing and Document Signing

A certificate contains:
- An identity
	- Hostname
	- Organisation
	- Or individual
- A public key
	- RSA
	- DSA
	- ECDA
	- etc.

#### What is a Certificate Authority (CA)?
An entity that issues digital certificates.
A CA acts as a trusted third party.
Trusted by both subject (owner) and the third party relying upon the certificate.