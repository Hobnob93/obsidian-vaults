#azure #azure-wda #exercise #shell #csharp 

# Exercise - Implement Interactive Authentication Using MSAL.NET
## Prerequisites
- *Azure* account with active subscription
- VSCode (or another IDE)

## Register New Application
1. Sign in to *Azure Portal*
2. Search for *Azure Active Directory*
3. Under ==Manage== select `App registrations` => `New registration`
4. When register app appears, enter app's information:
| Field                   | Value                                                  |
| ----------------------- | ------------------------------------------------------ |
| Name                    | az204appreg                                            |
| Supported account types | Select **Accounts in this org directory only**         |
| Redirect URI (optional) | Select **Public client/native** using **http://localhost** |
5. Select `Register`

*AAD* assigns unique application (client) ID to app.

## Create & Build Console Application
Use the following commands to create a console app and open in VSCode:
```shell
md az204-auth
cd az204-auth

dotnet new console

code . -r
```

### Add Packages
1. Add `Microsoft.Identity.Client` package to project
```shell
dotnet add package Microsoft.Identity.Client
```
2. Open `Program.cs`, and add the following `using` statements, as well as making `Main` async:
```cs
using System.Threading.Tasks;
using Microsoft.Identity.Client;

public static async Task Main(string[] args)
```

### Add Interactive Authentication
1. Need static variables with the `Program` class to hold Client and Tenant IDs (can get those values from the portal)
```cs
private const string _clientId = "APP_CLIENT_ID";
private const string _tenantId = "DIRECTORY_TENANT_ID";
```
2. Use the `PublicClientApplicationBuilder` to build auth context:
```cs
var app = PublicClientApplicationBuilder
	.Create(_clientId)
	.WithAuthority(AzureCloudInstance.AzurePublic, _tenantId)
	.WithRedirectUri("http://localhost")
	.Build();
```

### Acquire a Token
When registered the *az204appreg* app, it automatically generated an API permission `user.read` for MS Graph.
Use this permission to acquire a token.

1. Set permission scope for the token request
```cs
var scopes = { "user.read" };
```
2. Request token and write result to console
```cs
var result = await app.AcquireTokenInteractive(scopes)
	.ExecuteAsync();

Console.WriteLine($"Token:\t{result.AccessToken}");
```

## Run Application
Can use `dotnet build` and `dotnet run` commands to do this.
Open will open default browser prompting for account selection and to log in.
You may receive permissions requested notification if first time doing this.