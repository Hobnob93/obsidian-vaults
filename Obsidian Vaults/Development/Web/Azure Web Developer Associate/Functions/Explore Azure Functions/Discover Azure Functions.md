#azure #azure-wda 

# Discover Azure Functions
A solution for processing data; integrating systems; working with IoT; simples APIs; and microservices.
E.g. image processing; file maintenance; scheduled tasks.
Comes with templates to help get started.

Supports ==triggers==; ways to begin executing code.
Supports ==bindings==; ways to simplify data input and output.
Additional integration and automation services exist to help solve various problems.
They can all define ==input==, ==actions==, ==conditions==, and ==output==.

## Compare Azure Functions & Logic Apps
They *both* enable ==serverless workloads==.
*Functions* is a serverless compute service.
*Logic Apps* provides serverless workflows.
Both can create complex ==orchestrations==; a collection of functions or steps to accomplish a task.

### Orchestration
For *Azure Functions*, orchestrations done via *Durable Functions* extension.
For *Azure Logic Apps*, orchestrations done via GUI or editing config files.
Can mix and match services when orchestrating.

### Key Differences Between Functions & Logic Apps
See the table below for a concise difference between the two.

|              | Azure Functions          | Logic Apps                    |
| ------------ | ------------------------ | ----------------------------- |
| Development  | Code-first (imperative)  | Designer-first (declarative)  |
| Connectivity | Custom/built-in bindings | Connectors/custom connectors  |
| Actions      | Activity is a function   | Ready-made actions collection |
| Monitoring   | Azure App Insights       | Portal / Azure Monitor Logs   |
| Management   | REST API / Visual Studio | Portal / REST / PowSh / VS    |
| Exec Context | Locally or in cloud      | Run-anywhere scenarios        |

## Compare Functions & WebJobs
They are both code-first integration (WebJobs uses SDK).
Both designed for developers.
Both built on *Azure App Service* and supports features that come with that.

*Azure Functions* is built on the *WebJobs SDK*, so shares many of the same triggers and connections to other *Azure* services.
Some factors to consider when choosing between the two in the table below.

|                             | Functions | WebJobs with SDK |
| --------------------------- | --------- | ---------------- |
| Serverless with Autoscaling | Yes       | No               |
| Develop & test in browser   | Yes       | No               |
| Pay-per-use pricing         | Yes       | No               |
| Integration with Logic Apps | Yes       | No               |

They also differ with trigger events, as table below shows.

| Trigger Event                 | Functions | WebJobs with SDK |
| ----------------------------- | --------- | ---------------- |
| Timer                         | Yes       | Yes              |
| Storage Queues and Blobs      | Yes       | Yes              |
| Service Bus queues and topics | Yes       | Yes              |
| Cosmos DB                     | Yes       | Yes              |
| Event Hubs                    | Yes       | Yes              |
| HTTP/Webhook                  | Yes       | No               |
| Event Grid                    | Yes       | No               |
| File System                   | No        | Yes              | 

*Azure Functions* offers more dev productivity than *WebJobs* does.
Offers more options for languages; dev environments; *Azure* service integration; and pricing.
It is the best choice for **most** scnearios.