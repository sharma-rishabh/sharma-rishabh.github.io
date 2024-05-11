---
title: "Kafka With Spring"
date: 2024-05-11T11:32:20+05:30
draft: false
tags:
  - tech
  - kafka
  - event-driven-systems
---

In the last blog we learned how to implement kafka consumer-publisher using plain kotlin.
In this blog we'll walk through some code to implement the same using Spring.

Spring makes the implementation rather simple. We need to create a configuration class and then we can add all our code there.

### Setting up the configuration class

We need two annotations for this `Configuration` and `EnableKafka`. We can also take some time to pick the value for bootstrapAddress and topic name from `application.yaml`

```kotlin
@Configuration
@EnableKafka
class ConsumerPublisherConfig(
    @Value("\${kafka.bootstrapAddress}")
    private val bootstrapAddress: String,
    @Value("\${kafka.topic.name}")
    private val topicName: String
)
```

### Creating a topic

We'll need an AdminClient to create a new topic for our cluster, and then we can create a bean for each topic that we want to create like shown below.

```kotlin
private val adminConfig = mapOf(
	AdminClientConfig.BOOTSTRAP_SERVERS_CONFIG to bootstrapAddress
)

@Bean
fun admin(): KafkaAdmin {
	return KafkaAdmin(adminConfig)
}

@Bean
fun createTopic() = NewTopic(topicName, 1, 1.toShort())
```

### Creating a producer bean.

With Spring we need to setup a `ProducerFactory` so that it can take advantage of the multithreaded architecture and produce multiple events at once. We use `KafkaTemplate` which will internally use the producer factory to produce events. We'll see the usage later on for now let's set it up.

```kotlin
val producerProps = mapOf(
	ProducerConfig.BOOTSTRAP_SERVERS_CONFIG to bootstrapAddress,
	ProducerConfig.KEY_SERIALIZER_CLASS_CONFIG to StringSerializer::class.java,
	ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG to StringSerializer::class.java,
)

@Bean
fun producerFactory() = DefaultKafkaProducerFactory<String, String>(producerProps)

@Bean
fun kafkaTemplate(producerFactory: ProducerFactory<String, String>) = KafkaTemplate(producerFactory)
```

### Creating a consumer bean

Creating a Consumer is similar to creating a producer. We need to create a `ConsumerFactory` which then will be used by `ConcurrentKafkaListenerContainerFactory` to listen to events concurrently. let's set this up.

```kotlin
val consumerProps = mapOf(
	ConsumerConfig.BOOTSTRAP_SERVERS_CONFIG to bootstrapAddress,
	ConsumerConfig.GROUP_ID_CONFIG to "local-group",
	ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG to StringDeserializer::class.java,
	ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG to StringDeserializer::class.java,
	ConsumerConfig.AUTO_OFFSET_RESET_CONFIG to "earliest"
)

@Bean
fun consumerFactory() : DefaultKafkaConsumerFactory<String, String>{
	return DefaultKafkaConsumerFactory<String, String>(consumerProps)
}
@Bean
fun kafkaListenerContainerFactory(consumerFactory: ConsumerFactory<String, String>) = ConcurrentKafkaListenerContainerFactory<String, String>().also { it.consumerFactory = consumerFactory }

```

The code we have written till now will in the configuration class. Now let's see how we would use these beans to actually produce and consume events.

### Main Application

```kotlin
@SpringBootApplication
class KafkaConsumerPublisherApplication{
	@KafkaListener(id = "consumer", topics = ["AUTO_PRICES"])
	fun listen(message: String) {
		println(">>> MESSAGE $message")
	}

	@Bean
	fun runner(kafkaTemplate: KafkaTemplate<String, String>) =
		ApplicationRunner {
			kafkaTemplate.send("AUTO_PRICES", "ALTO", "100000")
		}
	companion object {
		@JvmStatic
		fun main(args: Array<String>) {
			runApplication<KafkaConsumerPublisherApplication>(*args)
		}
	}
}
```

Here the `KafkaListener` is using `ConcurrentKafkaListenerContainerFactory` in the background to consume the events and passes the message to the annotated function.

Hope this helped you to understand how to set up Kafka with Spring. If you have any doubts you can go through the code in this [repository](https://github.com/sharma-rishabh/kafka-consumer-publisher-).
