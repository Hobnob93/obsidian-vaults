#azure #az-204 

These perform comparisons against a number of rows.
There are a lot of tabular operators, but below are the common/main ones.

`count` - return s the count of rows in the table:
```Q
StormEvents | count
```

`take` - returns up to the specified number of rows of data:
```Q
StormEvents | take 5
```

`project` - returns a specific set of columns:
```Q
StormEvents
| take 5
| project StartTime, EndTime, State, EventType
```

`where` - filters a table to the subset of rows satisfying a predicate:
```Q
StormEvents
| where EventType == 'Flood' and State == 'WASHINGTON'
| take 5
| project StartTime, EndTime, State, EventType
```

`sort` - sorts the rows by one or more columns:
```Q
StormEvents
| where EventType = 'Flood'
| sort by DamageProperty desc
| take 5
| project StartTime, EndTime, State, EventType
```

`top` - returns the first N records sorted by the specified column(s) (so basically a `sort` and `take` rolled into one):
```Q
StormEvents
| where EventType == 'Flood'
| top 5 by DamageProperty desc
| project StartTime, EndTime, State, EventType
```

`extend` - creates a new column by computing a value:
```Q
StormEvents
| where EventType == 'Flood'
| top 5 by DamageProperty desc
| extend Duration = EndTime - StartTime
| project StartTime, EndTime, Duration
```

`summarize` - aggregates groups of rows, like a "group by":
```Q
StormEvents
| summarize event_count = count() by State
```

`render` - renders results as a graphical output:
```Q
StormEvents
| summarize event_count = count() by bin(StartTime, 1d)
| render timechart
```