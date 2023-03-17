#azure #az-204 

Cosmos DB provides five different consistency levels to maintain data availability and querying performance depending on your requirements.
You set default consistency at the Cosmos DB account-level under the Default Consistency blade.
Settings are in a range from:
- 1: 
	- higher latency
	- lower availability
	- worst read scalability
- to 5:
	- lower latency
	- higher availability
	- better read scalability

The five levels are:
1. **Strong**
	- Read operations ensure most recent data is returned
	- Reads cost the same as **Boundless Staleness** but more than **Session** and **Eventual**
	- Write operations can only be read after data has been replicated by most replicas
2. **Bounded Staleness**
	- Reads lag behind writes by at most `k` prefixes or `t` interval
	- Reads cost the same as **Strong** but more than **Session** and **Eventual**
	- Has highest level of consistency
	- Recommended for globally distributed applications, with high availability and low latency
3. **Session**
	- Read operations ensure written data is consistent with the same session
	- Consistency scoped to a user session
	- Other users may encounter "dirty" data if another session has just written some data
	- Default consistency for newly created databases
	- Reading costs lower than above, but more expensive than below
1. **Consistent Prefix**
	- Read operations ensure most recent data replicated among replicas is returned
	- Does not guarantee that the data is the most recent
	- "Dirty" data occurs when one replica changes the data state, but this data has not yet been replicated
	- Stronger consistency than eventual, but less than the others above
1. Eventual
	- Out of order reads
	- Read operations does not guarantee any consistency level