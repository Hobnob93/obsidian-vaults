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
- [`Microsoft.Graph.Core`](https://github.com/microsoftgraph/msgraph-sdk-dotnet)
- [`Microsoft.Graph.Auth`](https://github.com/microsoftgraph/msgraph-sdk-dotnet-auth)