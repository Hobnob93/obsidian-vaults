#azure  #azure-wda #csharp 

# Initialise Client Applications
With *MSAL.NET 3.x*, recommended way to instantiate app is using app builders.
They are `PublicClientApplicationBuilder` and `ConfidentialClientApplicationBuilder`.
They're a powerful mechanism to configure app from code or config file - or both!

Before initialising app, you need to register it so app can be integrated with [[About Microsoft identity Platform|Microsoft identity platform]].
You may need the following information (can be found in *Azure Portal*):
- Client ID (GUID)
- Identity provider of URL and sign-in audience of app (collectively the ==authority==)
- Tenant ID if writing business app solely for your org
- Application secret or certificate if it's a confidential client app
- Web apps, and often public client apps, need to set `redirectUri` where identity provider will contact your app back with security tokens

## Initialising Public & Confidential Client Apps From Code
The following instantiates a public client app, singing-in users in *Azure* public cloud, with their work and school accounts, or personal MS accounts.
```cs
var app = PublicClientApplicationBuilder.Create(clientId).Build();
```

Can do the same for a confidential application, handling tokens from users in *Azure* public cloud, work and school accounts, or personal MS accounts.
App is identified with identity provider by sharing a client secret:
```cs
var redirectUri = "https://myapp.azurewebsites.net";
var app = ConfidentialClientApplicationBuilder.Create(clientId)
	.WithClientSecret(clientSecret)
	.WithRedirectUri(redirectUri)
	.Build();
```

## Builder Modifiers
