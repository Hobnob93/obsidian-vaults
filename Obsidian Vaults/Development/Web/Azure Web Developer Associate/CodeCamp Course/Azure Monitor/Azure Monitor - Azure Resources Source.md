#azure #az-204 

Resource logs provide insights into the internal operation of an Azure resource.
Resource logs are created automatically.
You must create a diagnostic setting to specify a destination for them to be collected for each resource.

Platform metrics will write to the Azure Monitor metrics database with no configuration.
Access platform metrics from [[Azure Monitor - Metrics Explorer|Metrics Explorer]].
Trending and other analysis using Log Analytics.
Copy platform metrics to logs.
Send resource logs to Azure Storage for archiving.
Stream metrics to other locations using [[CodeCamp - Azure Event Hub|Azure Event Hub]].

![[Azure Monitor - Azure Resources Source Diagram.png]]