# Kafka
- Apache Kafka is a powerful, scalable, fault-tolerant distributed streaming platform.
- Apache Kafka is an event streaming platform used to collect, process, store, and integrate data at scale. It has numerous use cases including distributed logging, stream processing, data integration, and pub/sub messaging.
- Kafka is written in Scala and Java. 
- Apache Kafka is publish-subscribe based fault tolerant messaging system. 
- It is fast, scalable and distributed by design.
- Challenge: how to collect large volume of data and the second challenge is to analyze the collected data. To overcome those challenges, you must need a messaging system.
- In comparison to other messaging systems, Kafka has better throughput, built-in partitioning, replication and inherent fault-tolerance, which makes it a good fit for large-scale message processing applications.

# What is a Messaging System?
- Messaging System is responsible for transferring data from one application to another, so the applications can focus on data, but not worry about how to share it. - Distributed messaging is based on the concept of reliable message queuing. Messages are queued asynchronously between client applications and messaging system. 
- Two types of messaging patterns are available:
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

# Events
- An event is any type of action, incident, or change that's identified or recorded by software or applications. For example, a payment, a website click, or a temperature reading, along with a description of what happened.

- In other words, an event is a combination of notification—the element of when-ness that can be used to trigger some other activity—and state. That state is usually fairly small, say less than a megabyte or so, and is normally represented in some structured format, say in JSON or an object serialized with Apache Avro™ or Protocol Buffers.

# Kafka and Events - Key/Value Pairs
Kafka is based on the abstraction of a distributed commit log. By splitting a lot into partitions, Kafka is able to scale-out systems. As such, Kafka models events as key/value pairs. Internally, keys and values are just sequences of bytes, but externally in your programming language of choice, they are often structured objects represented in your language’s type system. Kafka famously calls the translation between language types and internal bytes serialization and deserialization. The serialized format is usually JSON, JSON Schema, Avro, or Protobuf.

Values are typically the serialized representation of an application domain object or some form of raw message input, like the output of a sensor.

Keys can also be complex domain objects but are often primitive types like strings or integers. The key part of a Kafka event is not necessarily a unique identifier for the event, like the primary key of a row in a relational database would be. It is more likely the identifier of some entity in the system, like a user, order, or a particular connected device.

# Kafka Architecture - Fundamental Concepts
Kafka Topics
----------
- Events have a tendency to proliferate—just think of the events that happened to you this morning—so we’ll need a system for organizing them. Kafka’s most fundamental unit of organization is the topic, which is something like a table in a relational database. As a developer using Kafka, the topic is the abstraction you probably think the most about. You create different topics to hold different kinds of events and different topics to hold filtered and transformed versions of the same kind of event.

- A topic is a log of events. Logs are easy to understand, because they are simple data structures with well-known semantics. First, they are append only: When you write a new message into a log, it always goes on the end. Second, they can only be read by seeking an arbitrary offset in the log, then by scanning sequential log entries. Third, events in the log are immutable—once something has happened, it is exceedingly difficult to make it un-happen. The simple semantics of a log make it feasible for Kafka to deliver high levels of sustained throughput in and out of topics, and also make it easier to reason about the replication of topics, which we’ll cover more later.

- Logs are also fundamentally durable things. Traditional enterprise messaging systems have topics and queues, which store messages temporarily to buffer them between source and destination.

- Since Kafka topics are logs, there is nothing inherently temporary about the data in them. Every topic can be configured to expire data after it has reached a certain age (or the topic overall has reached a certain size), from as short as seconds to as long as years or even to retain messages indefinitely. The logs that underlie Kafka topics are files stored on disk. When you write an event to a topic, it is as durable as it would be if you had written it to any database you ever trusted.

- The simplicity of the log and the immutability of the contents in it are key to Kafka’s success as a critical component in modern data infrastructure—but they are only the beginning.                                           
  
  
Kafka Partitioning
-------------------
If a topic were constrained to live entirely on one machine, that would place a pretty radical limit on the ability of Kafka to scale. It could manage many topics across many machines—Kafka is a distributed system, after all—but no one topic could ever get too big or aspire to accommodate too many reads and writes. Fortunately, Kafka does not leave us without options here: It gives us the ability to partition topics.

Partitioning takes the single topic log and breaks it into multiple logs, each of which can live on a separate node in the Kafka cluster. This way, the work of storing messages, writing new messages, and processing existing messages can be split among many nodes in the cluster.


How Partitioning Works
------------------
Having broken a topic up into partitions, we need a way of deciding which messages to write to which partitions. Typically, if a message has no key, subsequent messages will be distributed round-robin among all the topic’s partitions. In this case, all partitions get an even share of the data, but we don’t preserve any kind of ordering of the input messages. If the message does have a key, then the destination partition will be computed from a hash of the key. This allows Kafka to guarantee that messages having the same key always land in the same partition, and therefore are always in order.

For example, if you are producing events that are all associated with the same customer, using the customer ID as the key guarantees that all of the events from a given customer will always arrive in order. This creates the possibility that a very active key will create a larger and more active partition, but this risk is small in practice and is manageable when it presents itself. It is often worth it in order to preserve the ordering of keys.

Kafka Broker
----------
From a physical infrastructure standpoint, Kafka is composed of a network of machines called brokers. In a contemporary deployment, these may not be separate physical servers but containers running on pods running on virtualized servers running on actual processors in a physical datacenter somewhere. However they are deployed, they are independent machines each running the Kafka broker process. Each broker hosts some set of partitions and handles incoming requests to write new events to those partitions or read events from them. Brokers also handle replication of partitions between each other.

Replication
----------
It would not do if we stored each partition on only one broker. Whether brokers are bare metal servers or managed containers, they and their underlying storage are susceptible to failure, so we need to copy partition data to several other brokers to keep it safe. Those copies are called follower replicas, whereas the main partition is called the leader replica. When you produce data to the leader—in general, reading and writing are done to the leader—the leader and the followers work together to replicate those new writes to the followers.

Client Applications
-----------------
Now let’s get outside of the Kafka cluster itself to the applications that use Kafka: the producers and consumers. These are client applications that contain your code, putting messages into topics and reading messages from topics. Every component of the Kafka platform that is not a Kafka broker is, at bottom, either a producer or a consumer or both. Producing and consuming are how you interface with a cluster.

Kafka Producers
---------------
The API surface of the producer library is fairly lightweight: In Java, there is a class called KafkaProducer that you use to connect to the cluster. You give this class a map of configuration parameters, including the address of some brokers in the cluster, any appropriate security configuration, and other settings that determine the network behavior of the producer. There is another class called ProducerRecord that you use to hold the key-value pair you want to send to the cluster.

To a first-order approximation, this is all the API surface area there is to producing messages. Under the covers, the library is managing connection pools, network buffering, waiting for brokers to acknowledge messages, retransmitting messages when necessary, and a host of other details no application programmer need concern herself with

      (KafkaProducerString,<Payment> producer = new KafkaProducer<String, Payment>(props)) {

            for (long i = 0; i < 10; i++) {
                final String orderId = "id" + Long.toString(i);
                final Payment payment = new Payment(orderId, 1000.00d);
                final ProducerRecord<String, Payment> record = 
                   new ProducerRecord<String, Payment>("transactions", 
                                                payment.getId().toString(), 
                                                payment);
                producer.send(record);
           }
        } catch (final InterruptedException e) {
              e.printStackTrace();
         }
        
Kafka Consumers
------------------
Using the consumer API is similar in principle to the producer. You use a class called KafkaConsumer to connect to the cluster (passing a configuration map to specify the address of the cluster, security, and other parameters). Then you use that connection to subscribe to one or more topics. When messages are available on those topics, they come back in a collection called ConsumerRecords, which contains individual instances of messages in the form of ConsumerRecord objects. A ConsumerRecord object represents the key/value pair of a single Kafka message.

      try (final KafkaConsumer<String, Payment> consumer = new KafkaConsumer<>(props)) {
      consumer.subscribe(Collections.singletonList(TOPIC));

      while (true) {
          ConsumerRecords<String, Payment> records = consumer.poll(100);
          for (ConsumerRecord<String, Payment> record : records) {
              String key = record.key();
              Payment value = record.value();
              System.out.printf("key = %s, value = %s%n", key, value);
          }
        }
      }

What is Schema Registry?
------------------------
Schema Registry is a standalone server process that runs on a machine external to the Kafka brokers. Its job is to maintain a database of all of the schemas that have been written into topics in the cluster for which it is responsible. That “database” is persisted in an internal Kafka topic and cached in the Schema Registry for low-latency access. Schema Registry can be run in a redundant, high-availability configuration, so it remains up if one instance fails.

Schema Registry is also an API that allows producers and consumers to predict whether the message they are about to produce or consume is compatible with previous versions. When a producer is configured to use the Schema Registry, it calls an API at the Schema Registry REST endpoint and presents the schema of the new message. If it is the same as the last message produced, then the produce may succeed. If it is different from the last message but matches the compatibility rules defined for the topic, the produce may still succeed. But if it is different in a way that violates the compatibility rules, the produce will fail in a way that the application code can detect.

Likewise on the consume side, if a consumer reads a message that has an incompatible schema from the version the consumer code expects, Schema Registry will tell it not to consume the message. Schema Registry doesn’t fully automate the problem of schema evolution—that is a challenge in any system regardless of the tooling—but it does make a difficult problem much easier by keeping runtime failures from happening when possible.

Looking at what we’ve covered so far, we’ve got a system for storing events durably, the ability to write and read those events, a data integration framework, and even a tool for managing evolving schemas. What remains is the purely computational side of stream processing.

Link: https://docs.confluent.io/platform/current/schema-registry/index.html

