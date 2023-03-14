#azure #az-204 

When comparing Account Storage Azure Table vs Cosmos DB Table API.

| Feature             | Azure Table Storage                                                  | Cosmos DB Table API                                                                 |
| ------------------- | -------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| Latency             | Fast w/ no upper bounds                                              | <10ms for reads and writes                                                          |
| Throughput          | Limit of 20,000 operations/s                                         | Backed by SLAs - no upper limit                                                     |
| Global Distribution | Single region with one optional readable secondary read region       | 30+ regions                                                                         |
| Indexing            | Only primary index on PartitionKey and RowKey - no secondary indexes | Automatic and complete indexing on all properties, no index management              |
| Query               | Query execution uses index for primary key, and scans otherwise      | Queries can take advantage of automatic indexing on properties for fast query times |
| Consistency         | String within primary region - eventual within secondary             | Five well-defined consistency levels                                                |
| Pricing             | Consumption-based                                                    | Consumption-based or provisioned capacity                                           |
| SLAs                | 99.99% availability                                                  | 99.99% availability SLA (most conditions)                                                                                    |
