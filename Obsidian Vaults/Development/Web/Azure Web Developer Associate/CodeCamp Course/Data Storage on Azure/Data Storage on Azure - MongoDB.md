#azure #az-204 

**MongoDB** is an open-source document database which stores JSON-like documents.
The primary data structure for MongoDB is called BSON.

BSON is essentially binary JSON, and they are very similar:
- BSON is a subset of JSON and so its data structure is very similar
- BSON is designed to be efficient in both storage and scan speed when compared to JSON
- BSON has more data types that it can support, such as:
	- Datetime
	- Byte arrays
	- RegEx
	- MD5 binary data
	- JavaScript code

Example BSON file:
```BSON
\x16\x00\x00\x00            // total document size
\x02                        // 0x02 = type String
hello\x00                   // field name
\x06\x00\x00\x00world\x00   // field value (size, value, null terminator)
\x00                        // 0x00 = type E00 ('end of object')
```

MongoDB supports searches against:
- Fields
- Ranged queries
- Regular Expressions

MongoDB supports **primary** and **secondary** indexes.
High availability can be obtained via replica sets.
- Replica to offload reads, or acts as a stand-by in case of failure
Scales horizontally using *sharding*.
Can run over multiple servers via load balancing.
Can be used as a file system, called **GridFS**.
- With load balancing and data replication features over multiple machines for storing files
Supports fixed-size collections called **capped collections**.
Claims to support multi-document ACID transactions.

Provides 3 ways to perform aggregation (grouping data during a query)
- Aggregation pipeline
- Map-reduce
- Single-purpose aggregation