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

          sender.  ------> queue.  -----> Receiver
          
# Publish-Subscribe Messaging System
- messages are persisted in a topic. 
- Unlike point-to-point system, consumers can subscribe to one or more topic and consume all the messages in that topic. 
- In the Publish-Subscribe system, message producers are called publishers and message consumers are called subscribers. 

        sender.    ------> Message Queue.  ------> Receiver1
                                           \
                                            -> Receiver 2 ..n
                                            
# What is Kafka?
- Apache Kafka is a distributed publish-subscribe messaging system and a robust queue that can handle a high volume of data and enables you to pass messages from one end-point to another. 
- Kafka is suitable for both offline and online message consumption. 
- Kafka messages are persisted on the disk and replicated within the cluster to prevent data loss. 
- Kafka is built on top of the ZooKeeper synchronization service. 
- It integrates very well with Apache Storm and Spark for real-time streaming data analysis.

- Reliability − Kafka is distributed, partitioned, replicated and fault tolerance.
- Scalability − Kafka messaging system scales easily without down time..
- Durability − Kafka uses Distributed commit log which means messages persists on disk as fast as possible, hence it is durable..
- Performance − Kafka has high throughput for both publishing and subscribing messages. It maintains stable performance even many TB of messages are stored.

# Use Cases
Kafka can be used in many Use Cases. Some of them are listed below −

- Metrics −> Kafka is often used for operational monitoring data. This involves aggregating statistics from distributed applications to produce centralized feeds of operational data.
- Log Aggregation Solution −> Kafka can be used across an organization to collect logs from multiple services and make them available in a standard format to multiple con-sumers.
- Stream Processing −> Popular frameworks such as Storm and Spark Streaming read data from a topic, processes it, and write processed data to a new topic where it becomes available for users and applications. Kafka’s strong durability is also very useful in the context of stream processing.

# 

                                           
                                            
