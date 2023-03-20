#azure #az-204 

A certificate authority can issue multiple certificates in the form of a tree structure (a chain of trust).

#### Root Certificate Authority (Root CA)
A self-signed certificate.
Its private key is used to sign other certificates.
It's important that the private key of roots are protected.

#### Intermediate Certificate Authority (ICA)
Intermediate Certificates are signed by the root private key.
They act as entities that can issue certificates.
They protect the root certificate because the root certificate does not have to sign every issued certificate.

#### End Entity Certificate
A certificate by the ICA used by the end entity.
The entity in this case is an SSL certificate for a website.

#### Example Chain of Trust
- Amazon Root CA 1
	- Amazon (ICA)
		- \*.exampro.co