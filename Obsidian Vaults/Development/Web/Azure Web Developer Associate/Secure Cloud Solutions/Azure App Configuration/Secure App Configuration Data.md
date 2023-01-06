#azure #az-204 #cli 

## Encrypt Configuration Data By Using Customer-Managed Keys
Azure App Config encrypts sensitive information at rest using a 256-bit AES encryption key provided by Microsoft.
Every App Config instance has its own encryption key managed by the service.
When ==customer-managed== key capability is enabled, App Config uses a managed identity assigned to the App Config instance to authenticate with [[About Azure Active Directory|Azure Active Directory]] (AAD).
- The managed identity then calls [[Azure Key Vault]] and wraps the App Config instance's encryption key
- Wrapped key is then stored and the unwrapped encryption key is cached within App Config for *one hour*.
- App Config refreshes unwrapped version of App Config instance's encryption key hourly.

## Enable Customer-Managed Key Capability
The following components are required to enable it for Azure App Configuration:
1. Standard tier Azure App Configuration instance
2. Azure Key Vault with soft-delete and purge-protection features enabled
3. An RSA or RSA-HSM key within the Key Vault
	- Key must not be expired
	- It must be enabled
	- Must have wrap and unwrap capabilities enabled

Once resources are configured, two steps are required to allow Azure App Config to use the Key Vault key:
1. Assign managed identity to Azure App instance
2. Grant identity `GET`, `WRAP`, and `UNWRAP` permissions to target Key Vault's access policy

## Use Private Endpoints for Azure App Configuration
Allows clients on a virtual network (VNet) to securely access data over a private link.
The endpoint uses an IP address from the VNET address space for App Configuration store.
Network traffic between clients on VNet and App Config store traverses over the VNet using a private link on the MS backbone network.
- Eliminates exposure to public internet

Using private endpoints in App Configuration store allows you to:
- Secure app config by configuring firewall to block all connections to App Configuration on the public endpoint
- Increase security for VNet ensuring data doesn't escape
- Securely connect to the App Configuration store from on-premises networks that connect to VNet using VPN or ExpressRoutes with private-peering

## Private Endpoints for App Configuration
Specify App Configuration store a private endpoint connects to when creating it.
If you have multiple stores, you need a separate endpoint for each.
Azure relies on DNS resolution to route connections from VNet to the config store over a private link.
Quickly find connections strings in the Azure portal by selecting your App Configuration store, and selecting `Settings` > `Access Keys`.

## DNS Changes for Private Endpoints
When you create a private endpoint, the DNS CNAME resource record for config store is updated to an alias in a subdomain with prefix `privatelink`.
Azure also creates a ==private DNS zone== corresponding to the subdomain.

When endpoint URL is resolved from within the VNet hosting the private endpoint, it resolves to the private endpoint on the store.
When resolved from outside the VNet, the endpoint URL resolves to the public endpoint.
When you create a private endpoint, the public endpoint is disabled.

## Managed Identities
A [[Managed Identities|Managed Identity]] from AAD allows App Configuration to easily access other AAD-protected resources.
Identity is managed by the Azure platform.
It does not require you to provision or rotate any secrets.

## Add A System-Assigned Identity
You can use the `appconfig identity assign` to set up a managed identity using an existing config store.
```shell
az appconfig identity assign --name myConfigStore --resource-group myRG
```

## Add A User-Assigned Identity
You first need to create the identity:
```Shell
az identity create --resource-group myRG --name myUserAssignedIdentity
```
Then you can assign the new user-assigned identity to an existing config store:
```Shell
az appconfig identity assign --name myConfigStore \
	--resource-group myRG \
	--identities myUserAssignedIdentity
```