#azure #az-204 #csharp 

## Overview
Can use Azure CDN Library for .NET to automate creation and management of CDN profiles and endpoints.
Install `Microsoft.Azure.Management.Cdn.Fluent` from NuGet.

## Create A CDN Client
Create a client using the `CdnManagementClient` class:
```csharp
static void Main(string[] args)
{
	CdnManagementClient cdn = new CdnManagementClient(
		new TokenCredentials(authResult.AccessToken)
		{
			SubscriptionId = subscriptionId
		});
}
```

## List CDN Profiles And Endpoints
Can show a list of profiles and endpoints in resource group:
```csharp
var profiles = cdn.Profiles.ListByResourceGroup(resourceGroupName);
foreach (Profile p in profiles)
{
	Console.WriteLine($"CDN profile {p.Name}");
	if (p.Name.Equals(profileName, StringComparison.OrdinalIgnoreCase))
	{
		// profile already created
		profileAlreadyExists = true;
	}

	Console.WriteLine("Endpoints:");
	var endpoints = cdn.Endpoints.ListByProfile(p.Name, resourceGroupName);
	foreach (Endpoint e in endpoints)
	{
		Console.WriteLine($"-{e.Name} ({e.HostName})");
		if (e.Name.Equals(endpointName, StringComparison.OrdinalIgnoreCase))
		{
			// Unique endpoint name already exists
			endpointAlreadyExists = true;
		}
	}

	Console.WriteLine();
}
```

## Create CDN Profiles And Endpoints
Once verified the profiles and endpoints you want to create aren't already created, you can create them:
```csharp
if (profileAlreadyExists)
{
	// Do something else
}
else
{
	// Create new profile
	var profileParms = new ProfileCreateParameters
	{
		Location = resourceLocation,
		Sku = new Sku(SkuName.StandardVerizxon)
	};

	cdn.Profiles.Create(profileName, profileParams, resourceGroupName);
}
```

Once profile is created, we can create the endpoints:
```csharp
if (endpointAlreadyExists)
{
	// Do something else
}
else
{
	var endpointParams = new EndpointCreateParameters
	{
		Origins = new List<DeepCreatedorigin>()
		{
			new DeepCreatedOrigin("Contoso", "www.contoso.com")
		},
		IsHttpAllowed = true,
		IsHttpsAllowed = true,
		Location = resourceLocation
	};

	cdn.Endpoints.Create(endpointName, endpointParams, profileName, 
		resourceGroupName);
}
```

## Purge An Endpoint
A common task that might need to be performed to reset the cached assets.
```csharp
if (PromptUser(String.Format("Purge CDN endpoint {endpointName}")))
{
	Console.WriteLine("Purging endpoint, please wait...");
	cdn.Endpoints.PurgeContent(resourceGroupName, profileName, endpointName, 
		new List<string>() { "/*" });
	Console.WriteLine("Done.");
	Console.WriteLine();
}
```