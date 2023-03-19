#azure #az-204 

A Vault stores secrets and keys.
They can be protected either by software or FIPS 140-2 Level 2 validated [[Key Vault - HSM and FIPS|HSMs]].

Azure Key Vault provides two types of containers:
1. **Vaults**
	- Supports software and HSM-backed keys
2. **HSM Pools**
	- Only supports HSM-backed keys

To activate HSM you will need to
- provide a minimum of 3 RSA key-pairs (up to a maximum of 10)
- specify the minimum number of keys required to decrypt the security domain (called a *quorum*)

You do not choose the container on creation.
You choose between Standard and Premium.
When choosing Premium and you create enough RSA key pairs, you will begin to use HSM pools.