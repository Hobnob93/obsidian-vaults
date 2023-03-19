#azure #az-204 

Azure has 2 pricing tiers for Key Vault:
1. **Standard**
2. **Premium**
	- Support for HSM

##### Both Tiers
Secrets operations: $0.03/10,000 transactions.
Certificate renewal: $3 per renewal request.
Managed Azure Storage account key rotation: $1 per renewal.
Managed HSM Pools: $3.20/hour.

##### Software-Protected Keys
RSA 2048-bit keys: $0.03/10,000 transactions.
Advanced key types such as RSA 4096-bit: $0.15/10,000 transactions.

##### HSM-Protected Keys
RSA 2048-bit keys: $1/key/month + $0.03/10,000 transactions.
Advanced key types such as RSA 4096-bit:
- $5/key/month at 250 keys or less
- $2.50/key/month at 251-1500 keys
- $0.90/key/month at 1501-4000 keys
- $0.40/key/month at more than 4000 keys
- PLUS $0.15/10,000 transactions