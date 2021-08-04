## Kafka



#### Kafka

Apache Kafka is a distributed publish-subscribe messaging system and a robust queue that can handle a high volume of data and enables you to pass messages from one end-point to another. Kafka is suitable for both offline and online message consumption. Kafka messages are persisted on the disk and replicated within the cluster to prevent data loss. Kafka is built on top of the ZooKeeper synchronization service. It integrates very well with Apache Storm and Spark for real-time streaming data analysis.  Apache Kafka was originally developed by **LinkedIn**, and later it was donated to the Apache Software Foundation. Currently, it is maintained by **Confluent** under Apache Software Foundation. Apache Kafka has resolved the lethargic trouble of data communication between a sender and a receiver.



#### Messaging System

A Messaging System is responsible for transferring data from one application to another, so the applications can focus on data, but not worry about how to share it. Distributed messaging is based on the concept of reliable message queuing. Messages are queued asynchronously between client applications and messaging system. Two types of messaging patterns are available − one is point to point and the other is publish-subscribe (pub-sub) messaging system. Most of the messaging patterns follow **pub-sub**.



1. **Point to point Messaging System**

   In a point-to-point system, messages are persisted in a queue. One or more consumers can consume the messages in the queue, but a particular message can be consumed by a maximum of one consumer only. Once a consumer reads a message in the queue, it disappears from that queue. The typical example of this system is an Order Processing System, where each order will be processed by one Order Processor, but Multiple Order Processors can work as well at the same time.

   

2. **Publish - Subscribe Messaging System**

   In the publish-subscribe system, messages are persisted in a topic. Unlike point-to-point system, consumers can subscribe to one or more topic and consume all the messages in that topic. In the Publish-Subscribe system, message producers are called publishers and message consumers are called subscribers. A real-life example is Dish TV, which publishes different channels like sports, movies, music, etc., and anyone can subscribe to their own set of channels and get them whenever their subscribed channels are available.



#### Streaming Process

A streaming process is the processing of data in parallelly connected systems. This process allows different applications to limit the parallel execution of the data, where one record executes without waiting for the output of the previous record. Therefore, a distributed streaming platform enables the user to simplify the task of the streaming process and parallel execution. Therefore, a streaming platform in Kafka has the following key capabilities:

- As soon as the streams of records occur, it processes it.
- It works similar to an enterprise messaging system where it publishes and subscribes streams of records.
- It stores the streams of records in a fault-tolerant durable way.



#### Terminology in Kafka

1. **Message**

   Messages (records) are stored as serialized bytes; the consumers are responsible for de-serializing the message. Messages can have any format, the most common are string, JSON, and Avro.

   The messages always have a key-value structure; a key or value can be null. If the producer does not indicate where to write the data, the broker uses the key to partition and replicate messages. When the key is null, messages are distributed using the round-robin distribution. The DataStax Connector reads messages using tasks; each task subscribes to a subset of partitions. Therefore, all messages on the same partition are pulled by the same task. 

   Keys are used to write messages into partitions in a more controlled manner. Kafka simply finds the hash of the key and uses it to find the partition number where message has to be written

2. **Batch**

   A batch is just a **collection of messages**, all of which are being produced to the *same topic and partition*.

   Messages move within network in form of batches. This is done for efficiency is network utilization.

3.  **Topics**

   A Topic is a category/feed name to which records are stored and published.

   As said before, all Kafka records are organized into topics. Producer applications write data to topics and consumer applications read from topics. Records published to the cluster stay in the cluster until a configurable retention period has passed by.

   Kafka retains records in the log, making the consumers responsible for tracking the position in the log, known as the “offset”. Typically, a consumer advances the offset in a linear manner as messages are read. However, the position is actually controlled by the consumer, which can consume messages in any order. For example, a consumer can reset to an older offset when reprocessing records.

   Please note that if there is a sequence between all messages, then Kafka only ensures the sequence of messages stored in a single partition. There is no guarantee of sequence for all messages stored in multiple partitions.

4. **Partition**

   Kafka topics are divided into a number of partitions, which contain records in an unchangeable sequence. Each record in a partition is assigned and identified by its unique offset. A topic can also have multiple partition logs. This allows multiple consumers to read from a topic in parallel.

   Partitions allow topics to be parallelized by splitting the data into a particular topic across multiple brokers.

5. **Replicas of partition**

   In Kafka, replication is implemented at the partition level. The redundant unit of a topic partition is called a replica. Each partition usually has one or more replicas meaning that partitions contain messages that are replicated over a few Kafka brokers in the cluster.

   Every partition (replica) has one server acting as a leader and the rest of them as followers. The leader replica handles all read-write requests for the specific partition and the followers replicate the leader. If the lead server fails, one of the follower servers becomes the leader by default. You should strive to have a good balance of leaders so each broker is a leader of an equal amount of partitions to distribute the load.

6.  **Brokers**

   There are one or more servers available in Apache Kafka cluster, basically, these servers (each) are what we call a **broker**. A Kafka cluster consists of one or more servers (Kafka brokers) running Kafka. Producers are processes that push records into Kafka topics within the broker. A consumer pulls records off a Kafka topic.

   Running a single Kafka broker is possible but it doesn’t give all the benefits that Kafka in a cluster can give, Management of the brokers in the cluster is performed by Zookeeper. There may be multiple Zookeepers in a cluster, in fact the recommendation is three to five, keeping an odd number so that there is always a majority and the number as low as possible to conserve overhead resources.

7. **Kafka Cluster**

   Kafka’s having more than one broker are called as Kafka cluster. A Kafka cluster can be expanded without downtime. These clusters are used to manage the persistence and replication of message data.

8. **Producers**

   Producers are the publisher of messages to one or more Kafka topics. Producers send data to Kafka brokers. Every time a producer pub-lishes a message to a broker, the broker simply appends the message to the last segment file. Actually, the message will be appended to a partition. Producer can also send messages to a partition of their choice.

9. **Consumers**

   Consumers read data from brokers. Consumers subscribes to one or more topics and consume published messages by pulling data from the brokers.

   A. Low level consumers

   B. High level consumers

   ​	The high-level consumer (more known as consumer groups) consists of one or more consumers. Here a consumer group is created by adding the property “group.id” to a consumer. Giving the same group id to another consumer means it will join the same group.

   Every time a consumer is added or removed from a group the consumption is rebalanced between the group. All consumers are stopped on every rebalance, so clients that time out or are restarted often will decrease the throughput. Make the consumers stateless since the consumer might get different partitions assigned on a rebalance.

10. **Leaders**

    Leader is the node responsible for all reads and writes for the given partition. Every partition has one server acting as a leader.

11. **Followers**

    Node which follows leader instructions are called as follower. If the leader fails, one of the follower will automatically become the new leader. A follower acts as normal consumer, pulls messages and up-dates its own data store.

    


#### Type of Kafka Clusters

1. Single Node - Single Broker Cluster
2. Single Node - Multiple Broker Cluster
3. Multiple Nodes - Multiple Broker Cluster



#### Download kafka & Zookeeper

https://kafka.apache.org/downloads

https://zookeeper.apache.org/releases.html



**Run Zookeeper**

Rename zoo_sample.cfg to zoo.cfg  and add the following lines to enable some commands. This file is in config folder

`4lw.commands.whitelist=*`

Open command prompt in bin folder then type 

`zkServer.bat and run zookeeper`

**Run Kafka**

Go to config folder of kafka then open server.properties file and find listeners=PLAINTEXT:// and change to listeners=PLAINTEXT://localhost:9092

open command prompt in bin folder and type following command

`kafka-server-start.bat ../../config/server.properties`

**Create topic**

open command prompt in kafka bin folder then type following command

`kafka-topics.bat --create --zookeeper localhost:2181 --replication-factor 1 --partions 1 --topic test`

**Start producer console**

open command prompt in kafka bin folder then type following command

`kafka-console-producer.bat --broker-list localhost:9092 --topic test`

**Start Consumer console**

open command prompt in kafka bin folder then type following command

`kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic test --from-beginning`



Type in producer and enter then see in consumer.



#### Some other commands

1. kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic test --group myGroupName
2. kafka-topics.bat --zookeeper localhost:2181 --list
3. kafka-topics.bat --zookeeper localhost:2181 --describe --topic test
4. kafka-consumer-groups.bat bootstrap-server localhost:9092 --list
5. 
