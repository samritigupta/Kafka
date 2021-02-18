# Kafka
- Kafka is written in Scala and Java. 
- Apache Kafka is publish-subscribe based fault tolerant messaging system. 
- It is fast, scalable and distributed by design.
- Challenge: how to collect large volume of data and the second challenge is to analyze the collected data. To overcome those challenges, you must need a messaging system.
- In comparison to other messaging systems, Kafka has better throughput, built-in partitioning, replication and inherent fault-tolerance, which makes it a good fit for large-scale message processing applications.

# What is a Messaging System?
- Messaging System is responsible for transferring data from one application to another, so the applications can focus on data, but not worry about how to share it. - Distributed messaging is based on the concept of reliable message queuing. Messages are queued asynchronously between client applications and messaging system. - - Two types of messaging patterns are available:
  - one is point to point 
  - publish-subscribe (pub-sub) messaging system

# Point to Point Messaging System
- messages are persisted in a queue. 
- One or more consumers can consume the messages in the queue, but a particular message can be consumed by a maximum of one consumer only. 
- Once a consumer reads a message in the queue, it disappears from that queue. 
- The typical example of this system is an Order Processing System, where each order will be processed by one Order Processor, but Multiple Order Processors can work as well at the same time. 



