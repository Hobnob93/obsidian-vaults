#azure #az-204 #xml 

An example policy for an endpoint to cache the response may look like the following:
```xml
<policies>
	<inbound>
		<base />
		<cache-lookup vary-by-developer="false" vary-by-developer-groups="false"
		              downstream-caching-type="none">
		    <vary-by-header>Accept</vary-by-header>
		    <vary-by-header>Accept-Charset</vary-by-header>	
		</cache-lookup>
		<rewrite-uri template="/resource" />
	</inbound>
	<backend>
		<base />
	</backend>
	<outbound>
		<base />
		<cache-store duration="3600" />
	</outbound>
	<on-error>
		<base />
	</on-error>
</policies>
```