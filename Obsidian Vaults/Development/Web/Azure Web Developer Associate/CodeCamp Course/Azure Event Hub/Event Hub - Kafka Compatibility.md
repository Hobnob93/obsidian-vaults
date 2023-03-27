#azure #az-204 

Apache Kafka is an open source streaming platform to create high performance data pipelines, streaming analytics, data integration, and mission critical apps.
Kafka was originally developed by LinkedIn, and open-sourced in 2011.
It was written in Scala and Java, so to use it you need to write Java code.

Kafka is very similar to Event Hubs.
In Kafka, data is stored in partitions on a Kafka Cluster, which can span multiple machines.
Producers publish messages in a key-value format using Kafka Producer API.
Consumers listen for messages and consume them using Kafka Consumer API.

Messages are organised into Topics.
Producers will push messages to topics, and consumers will listen to topics.
A topic can contain multiple partitions.

Event Hubs provides an endpoint compatible with the Apache Kafka producer and consumer APIs for version 1 and above.
Event Hub Kafka Compatibility is an alternative to running your own Apache Kafka Cluster.

Terminology:
| Kafka          | Event Hub      |
| -------------- | -------------- |
| Cluster        | Namespace      |
| Topic          | Event Hub      |
| Partition      | Partition      |
| Consumer Group | Consumer Group |
| Offset         | Offset         | 
