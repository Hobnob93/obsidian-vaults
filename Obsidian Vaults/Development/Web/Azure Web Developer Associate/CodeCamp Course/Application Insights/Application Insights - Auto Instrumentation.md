#azure #az-204 

Auto-instrumentation allows you to enable application monitoring with Application Insights without modifying the codebase.
However, if you want to monitor specific things you are able to implement instrumentation manually using the SDK.

| Env                            | .NET           | .NET Core      | Java           | Node.js        | Python    |
| ------------------------------ | -------------- | -------------- | -------------- | -------------- | --------- |
| Azure App Service Windows      | GA, OnBD*      | GA, opt-in     | Public preview | Public preview | N/A       |
| Azure App Service Linux        |                | Public preview | GA             | GA             | N/A       |
| Azure Functions - Basic        | GA, OnBD*      | GA, OnBD*      | GA, OnBD*      | GA, OnBD*      | GA, OnBD* |
| Azure Functions - Dependencies | N/A            | N/A            | Public preview | N/A            | Extension |
| Azure Spring Cloud             | N/A            | N/A            | GA             | N/A            | N/A       |
| Azure Kubernetes Service       |                | N/A            | Agent          | N/A            | N/A       |
| Azure VMs Windows              | Public preview | Public preview | Agent          | N/A            | N/A       |
| On-premise VMs Windows         | GA, opt-in     | Public preview | Agent          | N/A            | N/A       |
| Standalone agent - any env     | N/A            | N/A            | GA             | N/A            | N/A       |

