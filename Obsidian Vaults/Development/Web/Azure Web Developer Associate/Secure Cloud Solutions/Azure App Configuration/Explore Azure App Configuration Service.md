#azure #az-204 

## Overview
Modern programs, especially those in the cloud, have many components that are distributed in nature.
Spreading config settings across components can lead to difficult debugging sessions.
Use ==App Configuration== to store all settings for an app in one secure place.

App Configuration offers the following benefits:
- A fully managed service which can be set up in minutes
- Flexible key representations and mappings
- Tagging with labels
- Point-in-time replay of settings
- Dedicated UI for feature flag management
- Comparison of two sets of config on custom-defined dimensions
- Enhanced security through Azure-managed identities
- Complete data encryptions, at rest or in transit
- Native integration with popular frameworks

App Configuration complements [[Azure Key Vault]].
It makes it easier to implement the following scenarios:
- Centralise management and distribution of hierarchical config data for different environments and geographies
- Dynamically change app settings without need to redeploy or restart application
- Control feature availability in real-time

## Use App Configuration
Add App Configuration through a client library provided by Microsoft.
See table below for which method to use based on language and framework.
| Language & Framework       | How to Connect                     |
| -------------------------- | ---------------------------------- |
| .Net Core and ASP.NET Core | App Config provider for .NET Core  |
| .NET Framework and ASP.NET | App Config builder for .NET        |
| Java Spring                | App config client for Spring Cloud |
| Others                     | App config REST API                |