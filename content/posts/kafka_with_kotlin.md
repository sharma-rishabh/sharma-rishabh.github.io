---
title: "Kafka With Kotlin"
date: 2024-04-07T13:02:53+05:30
draft: false
tags:
  - tech
  - kafka
  - event-driven-systems
---

In this blog we'll learn how to interact with a kafka broker using plain kotlin.

## Generating a kafka project.

For this we're going to generate a spring project using [spring initializer](https://start.spring.io/). Select the dependency `Spring for Apache Kafka`. We are adding this dependency so later on we can start using spring for our kafka interactions.

## Spinning up kafka and zookeeper.

Once you've generated your project you'll need to spin up an instance of kafka and zookeeper. Create a `docker-compose.yam` file.

```yaml
services:
  zookeeper:
    image: confluentinc/cp-zookeeper:latest
    environment:
      ZOOKEEPER_CLIENT_PORT: 2181
      ZOOKEEPER_TICK_TIME: 2000
    ports:
      - 22181:2181

  kafka:
    image: confluentinc/cp-kafka:latest
    depends_on:
      - zookeeper
    ports:
      - 9092:9092
    environment:
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://kafka:9092,PLAINTEXT_HOST://localhost:9092
      KAFKA_LISTENER_SECURITY_PROTOCOL_MAP: PLAINTEXT:PLAINTEXT,PLAINTEXT_HOST:PLAINTEXT
      KAFKA_INTER_BROKER_LISTENER_NAME: PLAINTEXT
      KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: 1
```

Then run this command from the directory where you've created `docker-compose.yaml` file.

```bash
docker-compose up
```

Now you should have zookeeper and a kafka broker instance running on your machine.

## Kafka with Kotlin

Before starting with anything else we can set up a few global variables for convenience.

```kotlin
val bootstrapServer = "localhost:29092"
val topicName = "PRICES"
```

### Creating a topic

Let's try to create a topic to publish and consume our events. For this we'll need a kafka admin client, and the rest of it is pretty straight-forward.

```kotlin
val adminConfig = mapOf(AdminClientConfig.BOOTSTRAP_SERVERS_CONFIG to bootstrapServer)


val topics = listOf(NewTopic(topicName, 1, 1.toShort()))

val adminClient = AdminClient.create(adminConfig)
adminClient.createTopic(topics)
adminClient.close()
```

### Publishing an event to Kafka

For publishing we need a few things like publisher props, kafka producer, and producerRecord. We don't need to worry about these as they come bundled with the kafka kotlin library.

```kotlin
val producerProps = Properties().apply {
	put(
		ProducerConfig.BOOTSTRAP_SERVERS_CONFIG,
		bootstrapServer
	)
	put(
		ProducerConfig.KEY_SERIALIZER_CLASS_CONFIG,
		StringSerializer::class.java
	)
	put(
		ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG,
		StringSerializer::class.java
	)
}

val producer = KafkaProducer<String, String>(producerProps)

val producerRecord = ProducerRecord(topic, "carPrice", "100000")

producer.send(producerRecord){metadata, error ->
	if (error == null) {
		println("Produced an event for ${metadata.topic()}")
	} else {
		println("Couldn't produce event ${error.message}")
	}
}

producer.flush()
producer.close()
```

### Consuming an event from Kafka

For consuming we need to configure consumer props, create a kafka consumer and subscribe to the topic. Then we can poll in a loop to consume any incoming events on the topics.

```kotlin
val consumerProps = Properties().apply {
	put(
		ConsumerConfig.BOOTSTRAP_SERVERS_CONFIG,
		bootstrapServer
	)
	put(
		ConsumerConfig.GROUP_ID_CONFIG, "local-group"
	)
	put(
		ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG,
		StringDeserializer::class.java
	)
	put(
		ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG,
		StringDeserializer::class.java
	)
	put(
		ConsumerConfig.AUTO_OFFSET_RESET_CONFIG, "earliest"
	)
}

val consumer = KafkaConsumer<String, String>(consumerProps)
consumer.subscribe(listOf(topic))

while (true) {
	val records = consumer.poll(Duration.ofMillis(100))
	for (record in records) {
		println(
		"Received Message on ${record.topic()}, key = ${record.key()}, value = ${record.value()}"
		)
	}
```

Note: If you're planning to use rich objects to represent your events rather than strings, you'll have to create a serilaizer and deserilazer class your self.

If you have any doubts you can go through the code in this [repository](https://github.com/sharma-rishabh/kafka-consumer-publisher-/tree/d38e7a76a560dc4b7df467b3b2d08512c3d44898)
