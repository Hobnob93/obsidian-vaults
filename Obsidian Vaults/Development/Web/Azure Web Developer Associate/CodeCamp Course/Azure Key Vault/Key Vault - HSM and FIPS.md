#azure #az-204 

An HSM is a **Hardware Security Module**.
It's a piece of hardware designed to store encryption keys.
An example would be Gemalto.

FIPS is the **Federal Information Processing Standard**.
It's a US and Canadian government standard that specifies the security requirements for cryptographic modules that protect sensitive information.

HSMs that are multi-tenant are FIPS 140-2 Level 2 compliant.
- Multiple customers virtually isolated on an HSM

HSMs that are single-tenant are FIPS 140-2 Level 3 compliant.
- Single customer on a dedicated HSM