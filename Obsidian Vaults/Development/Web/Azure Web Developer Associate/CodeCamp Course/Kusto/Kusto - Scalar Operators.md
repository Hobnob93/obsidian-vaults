#azure #az-204 

These perform comparisons against scalar data types.

Bitwise operators:
- `binary_and`
- `binary_not`
- `binary_or`
- `binary_shift_right`
- `binary_shift_left`
- `binary_xor`

Logical operators:
- `=`
- `!=`
- `and`
- `or`

Datetime / timespan arithmetic:
- add or subtract two date times
- add, subtract, divide, or multiple two timespans

Numerical operators (for `int`, `long`, and `real`):
- `+`, `-`, `*`, and `/`
- `%`
- `<`, `>`, `==`, `>=`, `<=`, `!=`
- Equals one of the elements: `in`
- Doesn't equal any of the elements: `!in`

String operators:
- `==`, `!=`, `=~`, `!~`
- `has`, `hasprefix`, `hassuffix`, `contains`, `starswith`, `endswith`, `matches`, `in`, `has_any` (and more)

Between operator:
- Matches the input that is inside the inclusive range
- `Table1 | where Num1 between (1 .. 10)`
- `Table1 | where Time1 between (datetime(2017-01-01) .. datetime(2020-01-01))`