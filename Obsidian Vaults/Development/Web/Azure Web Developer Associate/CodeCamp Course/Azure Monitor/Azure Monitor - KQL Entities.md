#azure #az-204 

Kusto is generally composed of the following entities:
- Clusters
	- Contain databases
	- A solution can have multiple clusters
- Databases
	- Named entities that hold tables and stored functions
- Tables
	- Named entities that hold data
	- Has an ordered set of columns
	- Zero or more rows of data
- Columns
	- Named entities that have a scalar data type
	- Columns are referenced in the query relative to the tabular data that is in the context of the specific operator referencing them
- Stored Functions
	- Named entities that allow reuse of Kusto queries or query parts
- External Tables
	- Entities that reference data stored outside a Kusto database
	- Used for exporting data from Kusto to external storage
	- Or for querying external data without ingesting it into Kusto