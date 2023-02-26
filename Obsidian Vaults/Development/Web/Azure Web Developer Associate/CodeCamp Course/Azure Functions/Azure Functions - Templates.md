#azure #az-204 

Templates are optional, but can save you time for common scenarios.
You choose your template within VSCode, and *not* in the portal.

| Template           | Trigger                            | Misc                               |
| ------------------ | ---------------------------------- | ---------------------------------- |
| HTTP               | HTTP request                       | Returns HTTP result                |
| Timer              | Schedule                           |                                    |
| Blob Storage       | On file upload/update              |                                    |
| Cosmos DB          | On new/modified documents          |                                    |
| Queue Storage      | Azure Storage queue messages       |                                    |
| Event Grid         | Event from Event Grid              | Many Azure Services use Event Grid |
| Event Hub          | Event from Event Hub               | Event streaming                    |
| Service Bus Queue  | Message in a Bus Queue             |                                    |
| Service Bus Topics | Event from a Bus Topic             | pub/sub model                      |
| SendGrid           | Email event in third-party service |                                    |

