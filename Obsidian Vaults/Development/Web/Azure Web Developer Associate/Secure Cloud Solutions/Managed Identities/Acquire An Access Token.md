#azure #az-204 #csharp #json 

## Overview
Client apps can request an app-only access token for accessing a given resource for a managed identity.
Token is based on managed identities for Azure resources service principal.
- No need for client to register itself to obtain access token
Token suitable for use as a bearer token in service-to-service calls requiring client credentials

## Acquire Token Using REST
Fundamental interface for acquiring access token is based on REST.
Accessible to any client app running on VM that can make HTTP REST calls.
Need to use the `GET` HTTP verb.
A fixed token endpoint for use from within VMs (see request below).
The `api-version` parameter indicating API version for IMDS endpoint.
- Use `2018-02-01` or greater.
The `resource` parameter indicates App ID URI of target resource
- Also appears in `aud` (audience) claim of the issued token
- Example below requests token for accessing Azure Resource Manager
The `metadata` parameter is required and must be set to `true`
- It's a mitigation against Server Side Request Forgery (SSRF) attacks.

An example access token request may look like this:
```http
GET 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https://management.azure.com/' HTTP/1.1 Metadata: true
```

Which will return a JSON response which looks like this:
```json
{
	"access_token": "eyJ0XAi...",
	"refresh_token": "",
	"expires_in": "3599",
	"expires_on": "1506484173",
	"not_before": "1506480273",
	"resource": "https://management.azure.com/",
	"token_type": "Bearer"
}
```

## Get A Token Using C\#
Code sample below builds request to acquire a token, calls the endpoint, and extracts token from the response:
```csharp
using System;
using System.Collection.Generic;
using System.IO;
using System.Net;
using System.Web.Script.Serialization;

// Build request to acquire managed identities for token
const string endpoint = "http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https://management.azure.com/";
HttpWebRequest request = (HttpWebRequest)WebRequest.Create(endpoint)
request.Headers["Metadata"] = "true";
request.Method = "GET";

try
{
	// Call token endpoint
	HttpWebResponse response = (HttpWebResponse)request.GetResponse();

	// Use stream reader to extract access token
	StreamReader reader = new StreamnReader(response.GetResponseStream());
	string stringResponse = reader.ReadToEnd();
	
	JavaScriptSerializer serializer = new();
	var result = serializer.Deserialize(stringResponse, 
		typeof(Dictionary<string, string>)) as (Dictionary<string, string>);

	return result["access_token"];
}
catch (Exception ex)
{
	string errorText = string.Format("{0} \n\n{1}", ex.Message,
		ex.InnerException != null
			? ex.InnerException.Message
			: "Acquire Token Failed");
}
```

## Token Caching
Managed identities for Azure resources subsystem does cache tokens.
It's still recommended to implement caching in own code.
Should prepare for scenarios where resource indicates token has expired.

## Retry Guidance
Recommended to try if you get a 404, 429, or 5xx code.
Throttling limits apply to number of calls made to IMDS endpoint.
- When exceeded, IMDS endpoint limits further requests while throttle is in effect
- During this period, status code of 429 is returned.