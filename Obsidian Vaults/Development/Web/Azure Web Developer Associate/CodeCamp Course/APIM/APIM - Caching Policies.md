#azure #az-204 #xml 

#### Get From Cache
Perform cache lookup and return a valid cached response when available.
```xml
// ... inbound policy
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false"
			  downstream-caching-type="none" must-revalidate="true"
			  caching-type="internal">
	<vary-by-query-parameter>version</vary-by-query-parameter>
</cache-lookup>

// ... outbound policy
<cache-store duration="<seconds>" />
```

#### Store to Cache
See above outbound.
Caches response according to specified cache control configuration.

#### Get Value from Cache
Retrieve a cached item by key.

#### Store Value in Cache
Store an item in the cache by key.
```xml
<cache-store-value key="@('userprofile-' + context.Variables['enduserid'])"
				   duration="10000" />
```