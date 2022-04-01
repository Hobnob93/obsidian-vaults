#azure #azure-wda #csharp #shell 

# Explore Stored Access Policies
Provides additional level of control over service-level SAS on server side.
Groups SAS and provides additional restrictions for signatures bound by the policy.
Can be used to change start time, expiry time, or permissions for a signature, or revoke it after it's been issued.

The following resources support stored access policies:
- Blob containers
- File shares
- Queues
- Tables

## Creating a Stored Access Policy
Access policy for SAS consists of start time, expiry time, and permissions for signature.
Can specify all in parameters on signature URI and none within stored access policy.
This can also be vice-versa or anything in between.
You cannot specify a parameter in BOTH!

To create or modify a policy, call the `Set ACL` operation for the resource.
Provide request body specifying terms of access policy.
Body request includes unique signed identifier of your choosing, up to 64 chars.

Below are examples of creating a policy by using either C# or *Azure CLI*.
```cs
var identifier = new BlobSignedIdentifier
{
	Id = "stored access policy identifier",
	AccessPolicy = new BlobAccessPolicy
	{
		ExpiresOn = DateTimeOffset.UtcNow.AddHours(1),
		Permissions = "rw"
	}
};

blobContainer.SetAccessPolicy(permissions:
	new BlobSignedIdentifier[] { identifier });
```

```shell
az storage container policy create
	--name <stored access policy identifier>
	--container-name <container name>
	--start <start time UTC datetime>
	--expiry <end time UTC datetime>
	--permissions <a, c, d, l, r, w>
	--account-key <storage account key>
	--account-name <storage account name>
```

## Modifying or Revoking a Storage Access Policy
Can call the access control *list* operation for resource type to replace existing policy.

To revoke a policy you can delete it, rename it by changing signed identifier, or change expiry time to something in the past.
Changing identifier breaks association between existing signatures and policy.
Changing expiry time to the past causes any associated signatures to expire.
Deleting policy immediately affects all SAS associated.

To remove a single access policy, call resource's `Set ACL` operation, passing set of signed identifiers you wish to maintain on container.
To remove all, do the same but with empty request body.