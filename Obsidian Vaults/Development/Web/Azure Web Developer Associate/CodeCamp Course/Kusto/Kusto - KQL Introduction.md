#azure #az-204 

Azure Monitor Logs is based on Azure Data Explorer.
Log queries are written using the Kusto Query Language (KQL or KSL).

Kusto is based on relational database management systems.
It supports [[Kusto - Entities|entities]] such as databases, clusters, tables, columns, and [[Kusto - Functions|functions]].

KQL can be used in:
- Log Analytics
- Log alert rules
- Workbooks
- Azure Dashboards
- Logic Apps
- PowerShell
- Azure Monitor Logs API

Some query operators include:
- calculated columns
- searching and filtering on rows
- group by-aggregates
- join functions

An example of a KQL query:
```Q
StormEvents
| where EventType == 'Flood' and State == 'WASHINGTON'
| sort by DamageProperty desc
| take 5
| project StartTime, EndTime, State, EventType, DamageProperty, EpisodeNarrative
```