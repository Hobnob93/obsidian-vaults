#azure #az-204 

In Kusto, data types are used for various things:
- Columns can have a defined type
- Function parameters expect specific data types

A data type defines how a piece of data is interpreted.
Scalars are quantities that are fully described by a magnitude (or numerical value) alone.
Data types in Kusto include:
- `bool`, `boolean`
	- represents a `true` or `false` value
- `datetime`, `date`:
	- represents a date and/or time
	- always in UTC time zone
- `decimal`
	- represents 128-bit decimal number
- `int`
	- represents a signed 32-bit integer
- `long`
	- represents a signed 64-bit integer
- `guid`, `uuid`, `uniqueid`
	- represents a 128-bit globally unique value
- `real`
	- represents 64-bit double-precision floating-point number
- `string`
	- represents a Unicode string
	- Kusto strings are encoded in UTF-8
	- are limited to 1MB in length by default
- `timespan`
	- represents a time interval
	- `2d` = 2 days, `30m` = 30 minutes, `1tick` = 100 ns
- `dynamic`
	- can accept primitive scalar types listed above
	- can be an array of data types
	- can be a "property bag", which is similar in format to JSON
- `null`
	- represents a missing value
	- all data types above are nullable