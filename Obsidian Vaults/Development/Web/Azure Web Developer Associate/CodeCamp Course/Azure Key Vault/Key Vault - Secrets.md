#azure #az-204 #cli #csharp 

Azure Key Vault Secrets provides secure storage of generic secrets.
This includes passwords and database connection strings.

Key Vault APIs accept and return secret values as strings.
Internally, Key Vault stores and manages secrets:
- As sequences of octets (8-bit bytes)
- With a maximum size of 25k bytes each
Key Vault service doesn't provide schematics for secrets.
- Accepts the data, encrypts it, stores it, and returns a secret identifier

For highly sensitive data, clients should consider additional layers of protection for data.
Encrypting data using separate protection key prior to storage in Key Vault is one example.

Key Vault also supports `contentType` field for secrets.
- Can specify content type of a secret to assist in interpreting the secret data when it is retrieved
- Maximum length of this field is 255 characters

All secrets in your Key Vault are stored encrypted.
Key Vault encrypts secrets at rest with a hierarchy of encryption keys.
- All keys in that hierarchy are protected by modules that are FIPS 140-2 compliant
- The encryption leaf key of they key hierarchy is unique to each Key Vault
- Encryption root key of the key hierarchy is unique to the security world
	- Protection level varies between regions e.g. China uses FIPS 140-2 Level 1
	- All other regions use Level 2 or higher

Secret attributes:
- `exp`
	- Expiration time
	- After which secret data should not be retrieved
- `Nbf`
	- Not before (default value is `now`)
	- The time before which secret data should not be retrieved
- `enabled`
	- Whether secret data can be retrieved
	- Default is `true`
- `created`
	- Read-only
- `updated`
	- Read-only

Can use the Azure CLI to retrieve secrets:
```shell
az keyvault secret show
	[--id] [--name] [--subscription] [--vault-name] [--version]
```

Or you can access them programmatically:
```cs
using Azure.Identity;
using Azure.Security.KeyVault.Secrets;
using Azure.Core;

var options = new SecretClientOptions()
{
	Retry = {
		Delay = TimeSpan.FromSeconds(2),
		MaxDelay = TimeSpan.FromSeconds(16),
		MaxRetries = 5,
		Mode = RetryMode.Exponential
	}
};

var uri = new Uri("https://<key-vault-name>.vault.azure.net/");
var creds = new DefaultAzureCredential();
var client = new SecretClient(uri, creds, options);

var secret = client.GetSecret("<mySecret>");
var secretValue = secret.Value;
```