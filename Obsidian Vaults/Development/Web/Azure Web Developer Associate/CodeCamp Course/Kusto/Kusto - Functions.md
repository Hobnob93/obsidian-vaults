#azure #az-204 

Functions are reusable queries or query parts.
Kusto supports several kinds of functions:
- **Stored Functions**
	- User-defined functions
	- Stored and managed
	- Belongs to one of two categories:
		- Scalar functions (input scalar, output scalar)
		- Tabular functions (input tabular data, output tabular data)
			- Tabular = multiple rows in a table
- **Query-Defined Functions**
	- User-defined functions
	- Defined and used within the scope of a single query
- **Built-In Functions**
	- Hard-coded, so cannot be modified by users
	- Defined by Kusto

**Special Functions** are one type of built-in function.
They are used for selecting Kusto entities, such as `cluster()`:
```Q
cluster('help').database('Sample').SomeTable
```

**Aggregation Functions** perform a calculation on a set of values, and returns a single value, such as `count()`:
```Q
StormEvents
| where State startswith "W"
| summarize Count=count() by State
```

**Windows Functions** operate on multiple rows (records) at a time e.g. `row_number()`:
```Q
range x from 1 to 10 step 1
| sort by x desc
| extend rn=row_number()
```