#azure #az-204 #csharp 

# Query Microsoft Graph Using SDKs
*MS Graph* SDKs designed to simplify building apps that access *MS Graph*.

## Components
SDKs include two components.

### Service Library
Contains models and request builders.
Generated from *MS Graph* metadata.
Provides rich, strongly typed, and discoverable experience.
Supports many of the datasets available in *MS Graph*.

### Core Library
Set of features to enhance work with *MS Graph* services.
Embedded support for retry handling, secure redirects, transparent authentication, and payload compression.
Does not add complexity to development.
Leaves the dev completely in control.
Provides support for common tasks such as pagination and batching requests.

## Install Microsoft Graph .NET SDK
The SDK is included in the following packages:
- [`Microsoft.Graph`](https://github.com/microsoftgraph/msgraph-sdk-dotnet)
	- contains models and request builders
	- for accessing `v1.0` endpoint with fluent API
	- has a dependency on `Microsoft.Graph.Core`
- [`Microsoft.Graph.Beta`](https://github.com/microsoftgraph/msgraph-beta-sdk-dotnet)
	- contains models and request builders
	- for accessing `beta` endpoint with fluent API
	- has a dependency on `Microsoft.Graph.Core`
- [`Microsoft.Graph.Core`](https://github.com/microsoftgraph/msgraph-sdk-dotnet)
	- core library for making calls to *MS Graph*
- [`Microsoft.Graph.Auth`](https://github.com/microsoftgraph/msgraph-sdk-dotnet-auth)
	- provides authentication scenario-based wrapper
	- [[Explore Microsoft Authentication Library|MSAL]] for use with *MS Graph* SDK
	- has a dependency on `Microsoft.Graph.Core`

## Create a Microsoft Graph Client
*MS Graph* client is designed to simplify calls.
Can use single client instance for lifetime of application.
Code below illustrates creating client instance.
Authentication provider handles access tokens for application.
Different app providers support different client scenarios ([Choose an Auth Provider](https://docs.microsoft.com/en-us/graph/sdks/choose-authentication-providers)).
```cs
var publicClientApp = PublicClientApplicationBuilder
	.Create("CLIENT-APP-ID")
	.Build();

var authProvider = new DeviceCodeProvider(publicClientApp, graphScopes);
var graphClient = new GraphServiceClient(authProvider);
```

## Read Information From Microsoft Graph
```cs
var user = await graphClient.Me
	.Request()
	.GetAsync();
```

## Retrieve List of Entities
Similar to retrieving single entity, except there is a number of options for configuring request.
The `$filter` param used to reduce result set to those matching the predicate.
The `$orderBy` param will request server sorts entitles by specified properties.
```cs
var messages = await graphClient.Me.Messages
	.Request()
	.Select(m => new {
		m.Subject,
		m.Sender
	})
	.Filter("<filter condition>")
	.OrderBy("receivedDateTime")
	.GetAsync();
```

## Delete Entity
```cs
var messageId = "blahBl4h";
var message = await graphClient.Me.Messages[messageId]
	.Request()
	.DeleteAsync();
```

## Create New Entity
```cs
var calendar = new Calendar
{
	Name = "Volunteer"
};

var newCalendar = await graphClient.Me.Calendars
	.Request()
	.AddAsync(calendar);
```

## Additional Resources
[MS Graph REST API v1.0 Reference](https://docs.microsoft.com/en-us/graph/api/overview)