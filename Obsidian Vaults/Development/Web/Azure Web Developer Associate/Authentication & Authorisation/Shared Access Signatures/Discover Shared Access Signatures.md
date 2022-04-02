#azure #az-204 

# Discover Shared Access Signatures
(SAS) is a signed URI pointing to one or more storage resources.
It includes a token containing a set of query parameters.
Token indicates how resources may be accessed by client.
The signature query param is constructed from SAS parameters and signed with key used to create the SAS.
This signature is used by *Azure Storage* to authorise access to storage resource.

## Types of Shared Access Signatures
*Azure Storage* supports three types of shared access signatures:
1. **User delegation SAS**
	- secured with *AAD* credentials
	- as well as by permissions specified for SAS
	- applies to *Blob* storage only
2. **Service SAS**
	- secured with storage account key
	- delegates access to resource in *Blob* storage, *Queue* storage, *Table* storage, or *Azure Files*
3. **Account SAS**
	- secured with storage account key
	- delegates access to resources in one or more storage services
	- All operations available via a service SAS or user delegation SAS are also available

## How Shared Access Signatures Work
When using SAS to access data stored in *Azure Storage*, you need two components:
1. URI to the resource to be accessed
2. SAS token you've created to authorise access to that resource

The token in the URI appears to be everything from the `sp` query param.

The token itself is made up of several components:
| Component | Description                                                                                      |
| --------- | ------------------------------------------------------------------------------------------------ |
| `sp`        | Controls access rights - `a` add, `c` create, `d` delete, `l` list, `r` record - can be combined |
| `st`      | Date and time when access starts                                                                 |
| `se`      | Date and time when access ends                                                                   |
| `sv`      | Version of storage API to use                                                                    |
| `sr`      | Kind of storage being accessed, i.e. `b` for blob                                                |
| `sig`     | The cryptographic signature                                                                      |

## Best Practises
To reduce risks of using SAS, there is some guidance:
- Always use HTTPS to prevent man-in-the-middle attacks and distribute securely
- User delegation SAS is most secure 
	- use wherever possible
	- removes need to store storage account key
	- must use *AAD* to manage credentials
	- might not be possible for solution
- Set expiration time to as short as possible
	- so if it becomes compromised, can only be exploited for a short time
- Apply rule of minimum-required privileges
	- only grant access that is required
- Some situations where SAS isn't correct solution
	- create a middle-tier service to manage users and access to storage

The most flexible way to use a service or account SAS is to associate tokens with a [[Explore Stored Access Policies|stored access policy]].