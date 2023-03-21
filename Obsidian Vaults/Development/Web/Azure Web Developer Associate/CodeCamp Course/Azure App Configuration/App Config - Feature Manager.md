#azure #az-204 #csharp 

Azure App Configuration Feature Manager allows you to add **feature flags**.
A feature flag provides an alternative to maintaining multiple feature branches in source code.
A condition within the code enables or disables a feature during runtime.
This makes it easier to rollback or do A/B testing for new functionality.

Feature flags can be accessed via code:
```cs
using Microsoft.FeatureManagement;

public class Startup
{
	public void ConfigureServices(IServiceCollection services)
	{
		// ...
		services.AddFeatureMangagement(
			Configuration.GetSection("FeatureFlags"));
		// ...
	}
}
```

**Feature Filters** allows advanced filtering of features.
A filter consistently evaluates the state of a feature flag.
A feature flag supports three built-in types of filters, with the option to create a custom one:
- Targeting
- Time Window
- Percentage