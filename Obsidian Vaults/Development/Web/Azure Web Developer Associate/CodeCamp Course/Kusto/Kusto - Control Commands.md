#azure #az-204 

Control commands can modify data and metadata.
It has its own syntax different from KQL.
It's essentially a tool for managing the database.

The following control command creates a new Kusto table with two columns:
```Q
.create table Logs (Level:string, Text:string)
```

A very common control command is `.show`.
For example, this will count all tables
```Q
.show tables
| count
```