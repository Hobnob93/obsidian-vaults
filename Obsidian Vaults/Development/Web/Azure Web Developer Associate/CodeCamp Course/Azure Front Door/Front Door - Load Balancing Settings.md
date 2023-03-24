#azure #az-204 

Origin group load balancing settings are set within a group.
Allows you to define what sample set is needed to be used to call the backend "healthy" or "unhealthy".

When applying load balancing settings, you can configure the following:
- Sample size
- Successful samples required
- Latency sensitivity (in milliseconds)

The latency sensitivity with a value of 0 means always send to the fastest available backend.
Otherwise, Front Door will round robin traffic between fastest and next fastest backends within configured latency sensitivity.