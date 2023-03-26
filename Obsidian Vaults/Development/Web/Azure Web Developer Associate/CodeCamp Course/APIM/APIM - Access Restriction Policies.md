#azure #az-204 #xml 

#### Check HTTP Header
Enforces existence and/or value of an HTTP header

#### Limit Call Rate
Prevents API usage spikes by limiting call rate.
On a per-subscription basis.
On a per-key basis.

#### Restrict Caller IPs
Filters (allow/disallow) calls from specific IP addresses and/or address ranges.
```xml
<ip-filter action="allow">
	<address>13.66.201.169</address>
	<address-range from="13.66.140.128" to="13.66.140.143" />
</ip-filter>
```

#### Set Usage Quota
Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota.
On a per-subscription basis.
On a per-key basis.

#### Validate JWT
Enforces existences of a valid JWT.
Extracted from specified HTTP header.
Or extracted from specified query string parameter.
```xml
<validate-jwt header-name="Authorization" require-scheme="Bearer">
	<issuer-signing-keys>
		<key>{{jwt-signing-key}}</key>
	</issuer-signing-keys>
	<audiences>
		<audience>@(context.Request.OriginalUrl.Host)</audience>
	</audiences>
	<issuers>
		<issuer>https://contoso.com</issuer>
	</issuers>
</validate-jwt>
```

#### Validate Client Certificate
Enforces a certificate presented by client to an APIM instance matches specified validation rules and claims.