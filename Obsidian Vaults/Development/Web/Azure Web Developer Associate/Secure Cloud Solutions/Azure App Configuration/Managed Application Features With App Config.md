#azure #az-204 #csharp #json 

## Overview
[[Manage App Features|Feature Management]] is a modern software development practise.
it decouples feature release from code deployment, and allows for quick changes to features on demand.
Uses a technique called feature flags (aka feature toggles, switches, etc).

## Basic Concepts
Some terms related to feature management:
- __Feature flag__
	- A variable with a boolean state
	- Has an associated code block
	- State of the feature flag controls whether the code block executes
- __Feature manager__
	- An application package handling lifecycle of all feature flags in an app
	- Typically provides additional functionality. such as caching feature flags and updating their states
- __Filter__
	- A rule for evaluating the state of a feature flag
	- A group, device, geographic location, time window, etc. are all examples of what a filter can represent

Effective implementation of feature management consists of two components:
1. An app that makes use of feature flags
2. A repository of feature flags and their current states

## Feature Flag Usage In Code
Can think of a feature flag as a boolean state variable used with a conditional statement:
```csharp
if (featureFlag)
{
	// Do something
}
else
{
	// Optionally can do something else instead
}
```

Can set the state statically, or based on certain rules:
```csharp
bool featureFlag = true;
// or
bool featureFlag = IsBetaUser();
```

## Feature Flag Declaration
Each feature flag has two parts; a ==name== and a list of one or more ==filters== used to evaluate if a state is on. 
When a feature has multiple filters, its list traversed in order until one filter determines feature should be enabled.
- Any remaining filters are skipped
If no filter indicates it should be on, then filter is off.

Feature manager supports `appsettings.json` as a config source for feature flags. Here is an example:
```json
"FeatureManagement": {
	"FeatureA": true,
	"FeatureB": false,
	"FeatureC": {
		"EnabledFor": [
			{
				"Name": "Percentage",
				"Parameters": {
					"Value": 50
				}
			}
		]
	}
}
```

## Feature Flag Repository
You should externalise all feature flags used in an application.
This allows you to change feature flags without modifying and/or redeploying the application.

Azure App Configuration is designed to be a centralised repository for feature flags.
Can use it to define different kinds of flags and manipulate their states easily.
Can use the App Config libraries for various languages and frameworks to easily access feature flags from your application.