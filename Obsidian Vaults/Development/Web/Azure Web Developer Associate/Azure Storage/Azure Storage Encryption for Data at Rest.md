#azure #azure-wda #topic 

# Azure Storage Encryption for Data at Rest
Automatically encrypts data when persisting to the cloud.
Protects data and helps meet organisational security and compliance commitments.
Data in *Azure* is encrypted and decrypted transparently using ==256-bit AES encryption==.
This is one of the strongest block ciphers available,. and is ==FIPS 140-2 compliant==.
Similar to *BitLocker* encryption on Windows.

Encryption is enabled for all new and existing storage accounts and *cannot* be disabled.
Due to data being secured by default, no need to modify code or apps to take advantage of *Azure Storage* encryption.

Accounts are encrypted regardless of performance tier or deployment model.
All redundancy options support encryption.
All copies of a storage account are encrypted.
All object metadata is also encrypted.

Encryption does not affect performance.
There is *no additional cost* for encryption.

## Encryption Key Management
Can rely on Microsoft-Managed keys for encryption of storage account.
Or you can manage your own keys.

If you manage with own keys, you have two options:
1. Specify a `customer-managed` key to use for encrypting and decrypting all data in storage account - used to encrypt all data in all services in storage account
2. Can specify `customer-provided` key on Blob storage operations - client can include an encryption key on request for granular control over *how* blob data is encrypted and decrypted

Following table compares key management options for encryption.

|                             | MS-Managed Keys | Customer-managed Keys                                                              | Customer-provided Keys                     |
| --------------------------- | --------------- | ---------------------------------------------------------------------------------- | ------------------------------------------ |
| Enc/Dec operations          | Azure           | Azure                                                                              | Azure                                      |
| Storage Services Supported  | All             | Blob, Files                                                                        | Blob Storage                               |
| Key Storage                 | MS Key Store    | Azure Key Vault                                                                    | Key Vault or other store                   |
| Key Rotation Responsibility | Microsoft       | Customer                                                                           | Customer                                   |
| Key Usage                   | Microsoft       | Portal, Resource Provider, REST API, Storage management libraries, PowerShell, CLI | Storage REST API, Storage client libraries |
| Key Access                  | Microsoft only  | Microsoft, Customer                                                                | Customer only                              | 
