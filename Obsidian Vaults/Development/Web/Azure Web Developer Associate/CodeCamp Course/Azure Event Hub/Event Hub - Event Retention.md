#azure #azure 

Published events are removed from an Event Hub based on a configurable, time-based retention policy.
- Default and shortest possible retention period is 1 day
- For *Standard*, the maximum is 7 days
- For *Premium* and *Dedicated*, maximum is 90 days
- Changing retention period applies to all messages already in the Event Hub
- You cannot explicitly delete events

Retention period exists to prevent large volumes of historic consumer data getting trapped in a deep store that is only indexed by a timestamp, and only allows sequential access.

If you need to archive events beyond the allowed retention period, you can have them automatically stored in Azure Storage or Azure Data Lake by turning on the [[Event Hub - Entities#Capture|Capture]] feature.

if you need to search or analyse such deep archives, you can easily import them into Azure Synapse, or other similar stores and analytics platforms.