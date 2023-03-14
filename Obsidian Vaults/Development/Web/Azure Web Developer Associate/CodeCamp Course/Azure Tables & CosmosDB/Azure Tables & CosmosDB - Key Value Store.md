#azure #az-204 

Key value stores are **DUMB** but very **FAST**.
They generally lack features such as:
- Relationships
- Indexes
- Aggregation

A key value store uses a unique key to store associated data.
The stored data is schema-less, so it can take the format of anything - bit it objects or simple data.
A key value store can resemble tabular data, it does not have to have the consistent columns per row (hence schema-less).

Due to their simple design they can scale well beyond a relational database.