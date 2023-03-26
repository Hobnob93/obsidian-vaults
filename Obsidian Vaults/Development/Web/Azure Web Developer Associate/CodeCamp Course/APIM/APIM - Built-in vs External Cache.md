#azure #az-204 

APIs and operations in APIM can be configured with response caching.
Response caching can significantly reduce latency for API callers and backend load for API providers.

#### Built-in Cache
Built-in cache is volatile and is shared by all units in the same region in the same APIM service.
See [[APIM - Caching Policies#Store to Cache|outbound caching policy]].

#### External Cache
You can utilise a Redis cache externally instead of using the built-in cache.
You simply need to provide a connection string to your Redis cache.

Using an external cache allows you to overcome a few limitations of the built-in cache:
- Avoid having your cache periodically cleared during APIM updates
- Have more control over cache config
- Cache more data that APIM tier allows
- Use caching with the Consumption tier of APIM
- Enable caching in the APIM of self-hosted gateways