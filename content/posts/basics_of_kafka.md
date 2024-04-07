---
title: "Basics of Kafka"
date: 2024-04-07T12:38:19+05:30
draft: false
tags:
  - tech
  - kafka
  - event-driven-systems
---

Kafka is a distributed event logging system. It's widely used in event event driven system as framework of choice.


### Events

- We learned about these the last time in [Event Driven Systems](/posts/event_driven_systems).
- In kafka an event is represented by a key-value pair.
- A key can be null as well.


### Topics

- A topic is an **ordered log**
- A new event is appended to end of a topic.
- A topic is not a queue it's a proper Log.


### Partitioning

- Topics are log files which are stored on the file system
- Kafka gives to you the ability to store the topic across multiple servers.
- Each server now act as a partition of the topic. A part of the topic is stored on the server.
- The order in which the event is stored in each partition is dependent upon the key of the event. In case of null the the logs are stored in a round robin fashion.


### Brokers

- Independent machines running the Kafka broker process.
- Managers partions
- Write the messages to topics
- Read messages from topics.
- Minimum computation is done on these so they are easy to replicate.


### Replication

- Each partition is replicated over brokers.
- There is lead broker and rest are follower brokers.
- While writing and reading we communicate with the lead broker.
- The replication is handled by Kafka internally.

### Zookeeper

- Centralised service used to maintain naming and configuration data.
- It selects the lead broker in case the current one goes down.
- Stores a list of topics that exist in Kafka
- Keeps a list of all the functioning brokers in the Kafka cluster.

### Consumer Groups

- Group of consumer that are assigned a subset of partitions from a topic(s).
- Parallelization of processing of those events.
