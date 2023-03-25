#azure #az-204 

Azure Monitor collects two fundamental types of data from sources:
- Logs
- Metrics

#### Azure Monitor Logs
Collects and organises log and performance data from monitored resources.
Data logs are consolidated from different sources into [[Azure Monitor - Log Analytics Workspaces|workspaces]].
- Platform logs from Azure Services
- Log and performance data from virtual machine agents
- Usage and performance data from applications can be consolidated in a workspace so they can be analysed together using a sophisticated query language capable of analysing millions of records.
Work with log queries and their results interactively using Log Analytics.

#### Azure Monitor Metrics
Collects numeric data from monitored resources into a time series database.
Collected at regular intervals.
They describe some aspect of a system at a particular time.
Lightweight and capable of supporting near real-time scenarios.
Useful for alerting and fast detection of issues.
You can analyse them interactively with Metrics Explorer.