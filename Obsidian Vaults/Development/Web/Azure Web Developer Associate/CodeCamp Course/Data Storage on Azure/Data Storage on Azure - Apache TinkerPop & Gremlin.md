#azure #az-204 

Apache TinkerPop is a graph computing framework for both graph databases (OLTP) and graph analytic systems (OLAP).

TinkerPop enables developers to use a vendor-agnostic distrusted framework to traverse (query) many different graph systems, such as:
- Amazon Neptune
- CosmosDB
- Hadoop (Spark)
- Neo4j
- OrientDB
- Titan

TinkerPop includes a graph traversal language called **Gremlin**, which can be used in many supported graph systems.
It is designed towards "Write once, run anywhere" (WORA).
Gremlin traversal can be evaluated as:
- real-time database query (OLTP)
- or as a batch analytics query (OLAP)

Gremlin Host Language Embedding means you can use your favourite programming language to write Gremlin.
```js
g.V().has("name","gremlin").as("a")
	.out("created").in("created")
		.where(neq("a"))
	.groupCount().by("title")
```