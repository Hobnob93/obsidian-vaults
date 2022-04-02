#azure #az-204 #feature-flags #csharp

# Manage App Features
Feature management is a modern software development practise.
Decouples feature release from code deployment.
Enables quick changes to feature availability on demand.
Uses a technique called `feature flags`.

## Basic Concepts
Several terms related to feature management:
- `Feature flag`
	- A variable with a binary state
	- has an associated *code block* within the application
	- State of the flag triggers whether the block runs
- `Feature manager`
	- An application package that handles the lifecycle of all feature flags in an app
	- Typically provides additional functionality, such as caching flags and updating their states
- `Filter`
	- A rule for evaluating the state of a feature flag
	- A user group, device or browser type, a geographic location, and a time window are examples of what filters can represent

An effective feature manager consists of *at least* two components working in concert:
- An application that makes use of feature flags
- A repository that stores flags and their states

## Feature Flag Usage in Code
The basic pattern is quite simple.
It's essentially a `boolean` variable wrapped in a `conditional` statement:
```cs
if (featureFlag) 
{
	// run some code
}
```
Can set the value of `featureFlag` statically, or evaluate based on some rules:
```cs
bool featureFlag = IsBetaUser();
```
A more complex feature flag may use an alternative condition as well:
```cs
if (featureFlag) 
{
	// Run some code
}
else 
{
	// Run some other code
}
```

## Feature Flag Declaration
Each feature flag has two parts:
1. A name
2. A *list* of one or more filters used to evaluate state of the feature

When a flag has ==multiple filters==, list is traversed in order until one filter determines feature *should* be enabled.
Any remaining filters after that enabling filter are skipped.
If no features are enabling, then feature is determined to be disabled.

The *feature manager* supports `appsettings.json` as a config source for feature flags.
Below is an example of how the flags may look in a JSON file:
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
To use flags effectively, you should *externalise* all flags within an app.
This approach allows you to change flags without modifying and redeploying the app itself.

*Azure App Configuration* is designed to be a centralised repository for flags.
Can use it to define different kinds of feature flags and manipulate their states quickly and confidently.
Can use *App Configuration* libraries for various frameworks to easily access flags from application.