#azure #az-204 #xml 

## Overview
Can be used to provide Transport Layer Security (TLS) mutual authentication between client and API gateway.
Can configure API Management gateway to only allow requests with certificates with specific thumbprint.
The authorisation at the gateway level is handled through inbound policies.

## Transport Layer Security Client Authentication
API Management can inspect certificate contained within the client request and check properties like:
- __Certificate Authority (CA)__
	- Only allow certificates signed by a particular CA
- __Thumbprint__
	- Allow certificates containing a specific thumbprint
- __Subject__
	- Allow certificates with a certain subject
- __Expiration Date__
	- Allow certificates that have *not* expired

The properties are not mutually exclusive.
Can be mixed together to form your own policy requirements.

Client certificates are signed to ensure they are not tampered with.
When a partner sends you a certificate, verify it comes from them and not an imposter.
There are two common ways to verify a certificate:
- Check who issued the certificate
	- If issuer was a trusted authority, you can use it
	- You can configure trusted authorities in Azure portal to automate this
- If issued by the partner verify it came from them
	- If they deliver the certificate in person, you can be sure of its authenticity
	- These are known as self-signed certificates

## Accepting Client Certificates in the Consumption Tier
Consumption tier in API Management is designed to work with serverless design principals.
This tier is a good fit if your API is built from serverless technologies, like [[Azure Functions]].
In Consumption tier, you must explicitly enable use of client certificates, which you can do on the `Custom domains` page.
This step is not necessary in other tiers.
![[Enable Use Of Client Certificates in Portal.png]]

## Certificate Authorisation Policies
Create these policies in the inbound policy file within the API Management gateway:
![[Certificate Authorisation Inbound Policies.png]]

## Check Thumbprint of a Client Certificate
Every client includes a thumbprint, which is a hash, calculated from certificate properties.
Thumbprint ensures values in the certificate have not been altered since certificate was issued by certificate authority.
You can check the thumbprint in your [[Create Advanced Policies#Control Flow|Control Flow policy]]:
```xml
<choose>
	<when condition="@(context.Request.Certificate == null || context.Request.Certificate.Thumbprint != <desired-thumbprint>)">
		<return-response>
			<set-status code="403" reason="invalid client certificate" />
		</return-response>
	</when>
</choose>
```

## Check Thumbprint Against Certificate Uploaded to API Management
Usually, each customer or partner company would pass a different certificate with a different thumbprint.
To support this scenario, obtain certificates from partners and use the `Client certificates` page in portal to upload them to API Management resource.
Then you can add this to your [[Create Advanced Policies#Control Flow|Control Flow policy]]:
```xml
<choose>
	<when conditition="@(context.Request.Certificate == null || !context.Request.Certicate.Verify() || !context.Deployment.Certificates.Any(c => c.Value.Thumbprint == context.Request.Certificate.Thumbprint))">
		<return-response>
			<set-status code="403" reason="invalid client certificate" />
		</return-response>
	</when>
</choose>
```

## Check Issuer and Subject of a Client Certificate
This [[Create Advanced Policies#Control Flow|Control Flow policy]] checks issuer and subject of certificate passed to request:
```xml
<choose>
	<when condition="@(context.Request.Certificate == null || context.Request.Certificate.Issuer != trusted issuer || context.Request.Certificate.SubjectName.Name != expected name)">
		<return-response>
			<set-status code="403" reason="invalid client certificate" />
		</return-response>
	</when>
</choose>
```