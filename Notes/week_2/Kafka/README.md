# Apache Kafka Notes

### **Module: Event Driven Architecture**

### **Event-Driven Architecture (EDA)**

Event-Driven Architecture (EDA) is a software design pattern where the flow of the application is determined by events. These events are significant occurrences within a system that trigger responses or actions. It is commonly used in systems requiring scalability, flexibility, and real-time processing.

---

### **Core Concepts**

1. **Events**:
    - Represent a significant action or change in the system (e.g., a user clicks a button, an item is added to a cart).
    - Events are immutable and usually have a payload that describes the occurrence.
2. **Producers**:
    - Components that generate events.
    - Example: A payment service generating a "Payment Successful" event.
3. **Consumers**:
    - Components that react to events.
    - Example: An email service sending a confirmation email when a "Payment Successful" event is received.
4. **Event Brokers**:
    - Middleware that facilitates communication between producers and consumers.
    - Example: Kafka, RabbitMQ, AWS SNS/SQS.
5. **Event Handlers**:
    - Logic that executes in response to an event.
    - Example: Updating a database when an event is received.

---

### **How EDA Works**

1. **Event Production**: A producer detects a change or action and generates an event.
2. **Event Propagation**: The event is transmitted to an event broker.
3. **Event Consumption**: Consumers subscribe to relevant events and react accordingly.

---

### **Benefits of EDA**

1. **Scalability**:
    - Independent components can be scaled based on load.
2. **Loosely Coupled Systems**:
    - Producers and consumers operate independently, reducing dependencies.
3. **Real-Time Processing**:
    - Events are processed as they occur, enabling near-instantaneous responses.
4. **Flexibility**:
    - Adding new features or consumers doesn't require significant changes to existing components.
5. **Resilience**:
    - Systems can continue operating even if some components fail.

---

### **EDA vs. Traditional Request-Driven Architecture**

| Feature | Event-Driven Architecture | Request-Driven Architecture |
| --- | --- | --- |
| Communication | Asynchronous | Synchronous |
| Coupling | Loose | Tight |
| Scalability | High | Limited |
| Response Time | Event-based, near real-time | Request-based, depends on server load |
| Use Case | Real-time systems, high flexibility | Transactional systems, predictable flows |

---

### **Types of EDA Patterns**

1. **Simple Event Processing**:
    - Events trigger specific actions in near real-time.
    - Example: A motion sensor turning on lights.
2. **Event Stream Processing**:
    - Events are continuously analyzed in a stream.
    - Example: Real-time fraud detection in banking.
3. **Complex Event Processing (CEP)**:
    - Multiple events are analyzed and correlated to identify patterns.
    - Example: Monitoring stock trading for unusual patterns.

---

### **Common Use Cases**

1. **Real-Time Applications**:
    - Chat applications, live dashboards, and notifications.
2. **IoT Systems**:
    - Sensors generating events for devices to act upon.
3. **Microservices Communication**:
    - Services communicating asynchronously to achieve scalability.
4. **E-commerce**:
    - Order processing workflows with events like "Order Placed" or "Item Shipped."
5. **Event Sourcing**:
    - Capturing the state changes as a sequence of events for reconstructing state.

---

### **Key Technologies**

- **Event Brokers/Message Queues**:
    - Kafka, RabbitMQ, Apache Pulsar, Amazon SNS/SQS, Azure Event Grid.
- **Streaming Frameworks**:
    - Apache Flink, Apache Storm, Spark Streaming.
- **Serverless Solutions**:
    - AWS Lambda, Azure Functions, Google Cloud Functions.

---

### **Challenges in EDA**

1. **Event Duplication**:
    - Handling duplicate events due to retries or distributed systems.
    - Solution: Use idempotent consumers.
2. **Debugging**:
    - Asynchronous nature can make debugging challenging.
    - Solution: Implement logging and monitoring.
3. **Complexity**:
    - Designing and maintaining loosely coupled systems can be difficult.
    - Solution: Proper documentation and use of standards.
4. **Data Consistency**:
    - Ensuring eventual consistency across components.
    - Solution: Adopt patterns like Saga for distributed transactions.

---

### **Events, Producer/Consumer, Event Bus/Broker**

In an Event-Driven Architecture (EDA), events are used to communicate between different components, decoupling the producers and consumers. This section explores the core components of EDA: **Events**, **Producers/Consumers**, and **Event Bus/Broker**.

---

### **1. Events**

An **event** represents a significant change or action that has occurred within the system. It is a piece of information that other components of the system may need to know about.

### **Event Characteristics**

- **Immutability**: Once an event is created, it cannot be changed. This guarantees that the system¿s history is preserved.
- **Self-contained**: The event should carry all necessary information to describe the occurrence (such as event type and event data).
- **Asynchronous**: Events are typically processed asynchronously. The producer does not need to wait for the consumer to act upon the event.

### **Example of an Event**

```json
{
  "eventType": "OrderPlaced",
  "orderId": 1234,
  "userId": 5678,
  "orderAmount": 299.99,
  "timestamp": "2024-12-03T10:00:00Z"
}

```

This `OrderPlaced` event includes the order ID, user ID, amount, and timestamp. Consumers may need to react to this event, such as by sending a confirmation or processing payment.

---

### **2. Producers and Consumers**

- **Producer**: The component that generates and sends events.
    - It detects a change or an action that needs to be communicated and creates an event.
    - Producers are often user-facing components or services that trigger actions based on business logic.
    - Example: A **User Service** producing an `AccountCreated` event when a new user registers.
- **Consumer**: The component that listens for events and processes them.
    - Consumers subscribe to events and take appropriate actions when an event they are interested in occurs.
    - A consumer may act by updating databases, invoking business logic, or notifying other services.
    - Example: An **Email Service** might consume the `AccountCreated` event and send a welcome email to the new user.

### **Example of Producer/Consumer in Practice**

- **Producer**: `OrderService` generates an event like `OrderPlaced`.
- **Consumer**: `PaymentService` listens for `OrderPlaced` events to initiate payment processing.

---

### **3. Event Bus/Broker**

The **Event Bus** or **Event Broker** is the system component responsible for transmitting events between producers and consumers. It decouples the event generation from event handling by ensuring that producers do not directly interact with consumers. The event bus enables the asynchronous, reliable delivery of events.

### **Roles of an Event Bus/Broker**

- **Event Dispatching**: It ensures events are sent from the producer to the appropriate consumer.
- **Message Queuing**: It can temporarily store events, allowing consumers to process events at their own pace. This ensures reliable delivery even if consumers are temporarily unavailable.
- **Routing**: It determines which consumers should receive specific events (e.g., filtering by event type or topic).
- **Persistence**: Some event brokers can persist events, enabling replay and auditing.

### **Types of Event Brokers**

1. **Message Queues (MQ)**:
    - Used in cases where events are consumed by a single consumer or where order matters.
    - Examples: **RabbitMQ**, **Amazon SQS**, **ActiveMQ**.
2. **Publish-Subscribe Systems (Pub/Sub)**:
    - Events are broadcasted to multiple consumers who subscribe to specific event types.
    - Examples: **Apache Kafka**, **Google Cloud Pub/Sub**, **AWS SNS**.
3. **Event Streams**:
    - Systems that allow for continuous streams of events, often for real-time processing.
    - Examples: **Apache Kafka**, **Apache Pulsar**, **Redpanda**.

### **Event Broker Example: Apache Kafka**

- **Kafka** is an example of a distributed event broker that supports high-throughput, fault tolerance, and scalability.
- Producers push events (e.g., order placed, payment completed) to Kafka topics.
- Consumers subscribe to these topics and process events asynchronously.

---

### **Event Flow: A Simple Example**

Consider an e-commerce platform:

1. **Producer**: The `OrderService` generates an event when a user places an order:
    
    ```json
    {
      "eventType": "OrderPlaced",
      "orderId": 1234,
      "userId": 5678,
      "totalAmount": 299.99
    }
    
    ```
    
2. **Event Bus/Broker**: The event is sent to the Event Broker (e.g., Kafka). The broker is responsible for delivering this event to the interested consumers.
3. **Consumers**:
    - **PaymentService**: Subscribes to `OrderPlaced` events to initiate payment processing.
    - **InventoryService**: Subscribes to `OrderPlaced` events to update stock levels.
    - **NotificationService**: Subscribes to `OrderPlaced` events to send an order confirmation to the user.

The system is decoupled, meaning that the `OrderService` does not need to know which services are consuming the event. It only generates the event and sends it to the Event Broker.

---

### **Apache Kafka**

Apache Kafka is an open-source, distributed event streaming platform used to handle large volumes of real-time data. Originally developed by LinkedIn and later open-sourced, Kafka is now one of the most widely used technologies for building scalable and fault-tolerant event-driven systems, especially in scenarios that require real-time analytics, monitoring, and high-throughput messaging.

Kafka is typically used for managing streams of data, event sourcing, log aggregation, and message brokering. It works by allowing the streaming of data across systems, making it suitable for applications like event-driven architectures, real-time analytics, and integrating data pipelines.

---

### **Core Components of Apache Kafka**

1. **Producer**:
    - A producer is an application or service that sends data to Kafka topics. Producers can send messages in real-time to a Kafka topic or multiple topics.
    - Producers typically write to a topic's partitions, and the Kafka brokers will handle the distribution of the data across nodes.
2. **Consumer**:
    - A consumer is an application or service that subscribes to Kafka topics and processes the data messages.
    - Consumers read data from Kafka topics, and they can either read from a specific partition or all partitions of the topic, depending on configuration.
3. **Broker**:
    - Kafka brokers are the core servers in the Kafka cluster that manage the storage, distribution, and retrieval of event messages.
    - They handle incoming producer messages and serve consumer requests. A Kafka cluster can have multiple brokers for scalability and fault tolerance.
4. **Topic**:
    - A topic is a category or feed name to which messages are sent by producers. Kafka topics are divided into partitions, and each partition is distributed across multiple brokers in the cluster.
    - Topics allow consumers to subscribe to specific categories of messages.
5. **Partition**:
    - Kafka topics are split into partitions for scalability and parallel processing. Each partition is an ordered, immutable sequence of messages.
    - Partitions allow Kafka to scale horizontally by distributing them across different brokers in the Kafka cluster.
6. **ZooKeeper** (deprecated in newer versions, now optional with **KRaft** mode):
    - ZooKeeper was used by Kafka for distributed coordination and management of brokers. It managed the leader election and metadata for topics and partitions. However, with newer versions of Kafka (starting from 2.8.0), Kafka has started replacing ZooKeeper with KRaft (Kafka Raft) for managing internal metadata.
7. **Consumer Groups**:
    - A consumer group is a group of consumers that jointly consume messages from one or more Kafka topics. Each consumer within the group reads data from exclusive partitions.
    - Consumer groups enable Kafka to handle parallel processing, as each consumer in the group can read from different partitions.

---

### **Kafka Architecture**

Kafka operates on a **distributed architecture** that can span multiple servers (brokers) and support massive amounts of event streams.

1. **Cluster**: Kafka is designed to run as a cluster, where multiple brokers work together to handle the ingestion, storage, and processing of messages.
2. **Replication**: Kafka provides fault tolerance through **replication**. Each partition in Kafka can be replicated across different brokers. This ensures that data is not lost even if a broker fails.
3. **Log-based Storage**: Kafka stores messages in a log format, which means messages are written to disk and can be retained for a configurable period (even after consumption), enabling use cases like event sourcing and replaying data.

---

### **Kafka Topics and Partitions**

1. **Topics**:
    - Kafka topics are logical channels to which producers send messages and consumers subscribe.
    - Topics can have multiple consumers and producers, enabling pub/sub messaging patterns.
2. **Partitions**:
    - Kafka divides topics into **partitions** for scalability. Each partition is a sequence of messages and is replicated across brokers for fault tolerance.
    - Partitions allow Kafka to distribute the load across multiple brokers and parallelize data processing.
    - The order of messages is guaranteed within a partition but not across partitions.

---

### **Kafka Producers and Consumers**

### **Kafka Producer**

To create a Kafka producer in Java, you need to include the Kafka client library in your project. Here's an example using **Maven** for dependency management:

### **Maven Dependency**

```xml
<dependency>
    <groupId>org.apache.kafka</groupId>
    <artifactId>kafka-clients</artifactId>
    <version>3.3.1</version>  <!-- Use the appropriate version -->
</dependency>

```

### **Kafka Producer Code**

This example demonstrates how to produce messages to a Kafka topic.

```java
import org.apache.kafka.clients.producer.KafkaProducer;
import org.apache.kafka.clients.producer.ProducerRecord;
import org.apache.kafka.common.serialization.StringSerializer;

import java.util.Properties;

public class KafkaProducerExample {
    public static void main(String[] args) {
        // Configure Kafka Producer
        Properties props = new Properties();
        props.put("bootstrap.servers", "localhost:9092"); // Kafka broker address
        props.put("key.serializer", StringSerializer.class.getName());
        props.put("value.serializer", StringSerializer.class.getName());

        // Create KafkaProducer instance
        KafkaProducer<String, String> producer = new KafkaProducer<>(props);

        try {
            // Produce messages
            for (int i = 0; i < 10; i++) {
                String message = "Message-" + i;
                ProducerRecord<String, String> record = new ProducerRecord<>("my-topic", "key-" + i, message);
                producer.send(record);
                System.out.println("Sent message: " + message);
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            // Close the producer
            producer.close();
        }
    }
}

```

### **Kafka Consumer Code**

The following example demonstrates how to consume messages from a Kafka topic.

```java
import org.apache.kafka.clients.consumer.ConsumerConfig;
import org.apache.kafka.clients.consumer.KafkaConsumer;
import org.apache.kafka.common.serialization.StringDeserializer;

import java.util.Collections;
import java.util.Properties;

public class KafkaConsumerExample {
    public static void main(String[] args) {
        // Configure Kafka Consumer
        Properties props = new Properties();
        props.put("bootstrap.servers", "localhost:9092");  // Kafka broker address
        props.put("group.id", "my-group");  // Consumer group ID
        props.put("key.deserializer", StringDeserializer.class.getName());
        props.put("value.deserializer", StringDeserializer.class.getName());
        props.put("auto.offset.reset", "earliest");  // Start reading from the beginning if no offset

        // Create KafkaConsumer instance
        KafkaConsumer<String, String> consumer = new KafkaConsumer<>(props);

        // Subscribe to the topic
        consumer.subscribe(Collections.singletonList("my-topic"));

        try {
            while (true) {
                // Poll for new messages
                var records = consumer.poll(1000);  // 1000ms timeout
                records.forEach(record -> {
                    System.out.println("Consumed message: " + record.value());
                });
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            // Close the consumer
            consumer.close();
        }
    }
}

```

---

### **Explanation**

1. **Producer Example**:
    - **KafkaProducer** is used to send messages to a Kafka topic.
    - It takes properties that define how to connect to the Kafka broker and what type of serialization to use for keys and values.
    - The **ProducerRecord** class is used to represent a record that gets sent to the Kafka topic.
    - The producer sends messages asynchronously, and `send()` can take a callback to handle the result.
2. **Consumer Example**:
    - **KafkaConsumer** reads messages from a Kafka topic.
    - The consumer subscribes to a topic, then uses `poll()` to fetch messages.
    - The `auto.offset.reset` property determines where the consumer starts reading (e.g., from the latest message, earliest, etc.).
    - The consumer reads in a loop and prints out each consumed message.

---

### **Running Kafka Locally**

1. **Start Kafka Broker**: Before running the producer and consumer code, make sure you have a Kafka broker running. You can download and start Kafka locally by following these steps:
    - Download Kafka from the [official site](https://kafka.apache.org/downloads).
    - Start Zookeeper (which Kafka uses for distributed coordination):
        
        ```bash
        bin/windows/zookeeper-server-start.bat config/zookeeper.properties
        
        ```
        
    - Start Kafka broker:
        
        ```bash
        bin/windows/kafka-server-start.bat config/server.properties
        
        ```
        
2. **Create Topic**: You need to create a Kafka topic to send and receive messages.
    
    ```bash
    bin/windows/kafka-topics.bat --create --topic my-event-topic --bootstrap-server localhost:9092 --partitions 1 --replication-factor 1
    
    ```
    
3. **Start Producer and Consumer**: After setting up the Kafka broker and creating a topic, you can run the producer and consumer code.

### Maven Dependencies

```
<dependencies>
    <dependency>
        <groupId>org.apache.kafka</groupId>
        <artifactId>kafka-clients</artifactId>
        <version>3.9.0</version>
    </dependency>
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-api</artifactId>
        <version>2.0.0-alpha1</version>
    </dependency>
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-simple</artifactId>
        <version>2.0.0-alpha1</version>
    </dependency>
</dependencies>
```

### **Kafka Producer Example (Java)**

This example demonstrates producing events (messages) to a Kafka topic.

```java
import org.apache.kafka.clients.producer.KafkaProducer;
import org.apache.kafka.clients.producer.ProducerRecord;
import org.apache.kafka.common.serialization.StringSerializer;

import java.util.Properties;

public class EventProducer {
    public static void main(String[] args) {
        // Setup Kafka Producer properties
        Properties props = new Properties();
        props.put("bootstrap.servers", "localhost:9092");
        props.put("key.serializer", StringSerializer.class.getName());
        props.put("value.serializer", StringSerializer.class.getName());

        // Create KafkaProducer instance
        KafkaProducer<String, String> producer = new KafkaProducer<>(props);

        try {
            // Produce event
            for (int i = 0; i < 5; i++) {
                String key = "event-key-" + i;
                String value = "Event-Data-" + i;
                ProducerRecord<String, String> record = new ProducerRecord<>("my-event-topic", key, value);
                producer.send(record);
                System.out.println("Produced event: " + value);
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            // Close producer
            producer.close();
        }
    }
}

```

### **Kafka Consumer Example (Java)**

This example demonstrates consuming events (messages) from a Kafka topic.

```java
import org.apache.kafka.clients.consumer.KafkaConsumer;
import org.apache.kafka.common.serialization.StringDeserializer;

import java.util.Collections;
import java.util.Properties;

public class EventConsumer {
    public static void main(String[] args) {
        // Setup Kafka Consumer properties
        Properties props = new Properties();
        props.put("bootstrap.servers", "localhost:9092");
        props.put("group.id", "my-event-consumer-group");
        props.put("key.deserializer", StringDeserializer.class.getName());
        props.put("value.deserializer", StringDeserializer.class.getName());
        props.put("auto.offset.reset", "earliest");

        // Create KafkaConsumer instance
        KafkaConsumer<String, String> consumer = new KafkaConsumer<>(props);

        // Subscribe to the event topic
        consumer.subscribe(Collections.singletonList("my-event-topic"));

        try {
            while (true) {
                // Poll for new events (messages)
                var records = consumer.poll(1000);
                records.forEach(record -> {
                    System.out.println("Consumed event: " + record.value());
                });
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            // Close consumer
            consumer.close();
        }
    }
}

```

---

### **Kafka Use Cases**

1. **Real-Time Event Streaming**:
    - Kafka is widely used for processing real-time data streams, such as clickstream data, sensor data, or logs from distributed systems.
2. **Log Aggregation**:
    - Kafka is used for collecting logs from different systems, applications, and servers, making it easier to monitor, analyze, and process logs centrally.
3. **Data Pipelines**:
    - Kafka serves as the backbone for building robust, scalable data pipelines where data flows from producers to multiple consumers or data storage systems.
4. **Event Sourcing**:
    - Kafka is used for event sourcing, where each change in application state is captured as an immutable event. These events can be replayed to rebuild the state of an application.
5. **Microservices Communication**:
    - Kafka facilitates asynchronous communication between microservices, allowing decoupled systems to communicate and react to events.
6. **Real-Time Analytics**:
    - Kafka is often used in combination with tools like **Apache Flink**, **Apache Spark**, or **Kafka Streams** to perform real-time stream processing and analytics.

---

### **Kafka Advantages**

1. **High Throughput**:
    - Kafka can handle high throughput, supporting millions of messages per second. It is optimized for both writing and reading high volumes of data.
2. **Scalability**:
    - Kafka clusters can scale horizontally by adding more brokers and partitions. It can handle a massive amount of data.
3. **Fault Tolerance**:
    - Kafka's replication mechanism ensures that data is fault-tolerant, even in the case of broker failures. Data remains available due to multiple replicas of partitions.
4. **Distributed**:
    - Kafka is designed to work as a distributed system, with no single point of failure. It can span multiple data centers or cloud regions.
5. **Durability**:
    - Kafka ensures that data is safely stored and can be replayed at any time, making it reliable for storing critical data.

---

### **Kafka Challenges**

1. **Operational Complexity**:
    - Running a Kafka cluster can be complex, requiring knowledge of topics, partitions, replication, and scaling strategies.
2. **Message Duplication**:
    - Due to Kafka¿s distributed nature, message duplication can occur, and consumers need to be designed to handle it.
3. **Event Ordering**:
    - Kafka guarantees ordering of events within a partition, but across partitions, ordering may not be maintained.
4. **Latency**:
    - While Kafka supports low-latency processing, in some use cases (e.g., near real-time data processing), additional optimizations may be necessary to reduce latency.

---

### **Apache Kafka Event Streams**

Apache Kafka is a powerful platform for **event streaming**, enabling real-time data processing and integration of distributed systems. Kafka's **event streaming** capabilities allow it to handle large volumes of data in real-time, making it an ideal solution for use cases like monitoring, analytics, and event-driven architectures. Here¿s a deeper look at how Kafka works with **event streams**, how to use it effectively, and some of its key concepts.

---

### **What is Event Streaming?**

Event streaming refers to the continuous flow of events (data) through a system in real time. Kafka acts as an event streaming platform that allows producers (data sources) to publish events to topics, and consumers (data sinks or processing systems) to consume and process these events in real time.

In Kafka, events are typically messages that are produced and consumed asynchronously. Kafka ensures that the events are processed in the correct order (within partitions) and that the system is scalable, fault-tolerant, and resilient.

---

### **Key Concepts in Kafka Event Streaming**

1. **Producer**:
    - The producer is responsible for producing (or publishing) events to Kafka topics. It sends events to Kafka brokers, which then distribute the events to topic partitions.
    - A producer can send events to one or more partitions, depending on the partitioning strategy.
2. **Consumer**:
    - Consumers subscribe to Kafka topics and consume events from partitions. Consumers can be part of a **consumer group**, where each consumer in the group reads messages from a subset of partitions.
    - Consumer groups allow Kafka to scale horizontally, processing data in parallel.
3. **Topic**:
    - Kafka topics are logical channels to which producers publish events. Topics help organize streams of events, allowing consumers to subscribe to specific streams.
    - Topics can be divided into multiple partitions, which help distribute event data across multiple brokers.
4. **Partition**:
    - A topic can have multiple partitions, and each partition stores a subset of events (messages). Partitions enable Kafka to scale horizontally, with different brokers handling different partitions.
    - Kafka ensures **ordering of events** within a partition, but events across partitions may not be in order.
5. **Consumer Group**:
    - A consumer group is a set of consumers that work together to process events from Kafka topics. Each consumer in the group processes messages from different partitions.
    - Consumer groups enable load balancing and parallel processing of events, ensuring scalability and fault tolerance.
6. **Event Streams**:
    - An **event stream** is a continuous flow of events that are produced and consumed in real time. In Kafka, event streams are represented by topics and partitions. Kafka's ability to store and retrieve events allows for use cases like event sourcing and replaying events.
7. **Replication**:
    - Kafka supports replication of topic partitions to ensure data availability and fault tolerance. Each partition can be replicated across multiple brokers, ensuring that even if one broker fails, data is still available from other brokers.
8. **Kafka Streams**:
    - **Kafka Streams** is a library that allows developers to build real-time stream processing applications directly on top of Kafka. It simplifies the process of consuming, processing, and producing events in Kafka, enabling use cases like event transformation, enrichment, and aggregation.

---

### **Kafka Event Streams Flow**

1. **Producer sends an event** to a Kafka topic.
2. The event is written to a **partition** of the topic.
3. **Consumers** read events from the partitions. Each consumer in a group reads from a specific partition, ensuring parallel processing.
4. Kafka provides **guaranteed message delivery**, with options for handling failures using retries and acknowledging event consumption.
5. Events are stored in **Kafka logs** for a configurable retention period. Consumers can read past events (even those already consumed) for replay or auditing purposes.

---

### **Kafka Use Cases in Event Streaming**

### **1. Real-time Analytics**

Kafka enables real-time event streams that can be processed and analyzed in real time. For example:

- Monitoring application logs and system health.
- Processing metrics and generating real-time insights or dashboards.

### **2. Event Sourcing**

In an event-driven architecture, Kafka can be used for **event sourcing**, where each change to the state of a system is captured as an event.

- These events can be replayed or processed in order to reconstruct system state at any point in time.
- Kafka¿s durability and message retention features make it ideal for storing events for future replay or debugging.

### **3. Real-time Data Integration**

Kafka enables **event-driven microservices architectures**, where different microservices exchange data through Kafka topics.

- For example, a service can listen to a Kafka topic for incoming events (such as orders placed or payments processed) and react to them in real time.
- Kafka facilitates loose coupling between services and enables them to scale independently.

### **4. Log Aggregation**

Kafka can aggregate logs from multiple sources, centralizing logging and making it easier to process and analyze logs in real time.

- Logs from various systems or services are streamed to Kafka topics, and consumers can process them to detect anomalies or generate metrics.

### **5. Stream Processing**

With **Kafka Streams** or other stream processing engines like **Apache Flink**, Kafka can be used for real-time data transformation and enrichment.

- For instance, incoming data could be enriched with additional information (e.g., joining data streams), aggregated, or filtered before being forwarded to other services or systems.

---

### **Implementing Kafka Event Streams in Java**

Here¿s a simple example of how to implement event streams using Kafka in Java:

### **Setup**

1. **Input Topic**: `input-topic` (sentences are produced here).
2. **Output Topic**: `output-topic` (word counts are written here).

### **Maven Dependency**

Add Kafka Streams to your `pom.xml`:

```xml
<dependency>
    <groupId>org.apache.kafka</groupId>
    <artifactId>kafka-streams</artifactId>
    <version>3.5.0</version> <!-- Use the latest version -->
</dependency>

```

---

### **Code: Kafka Streams Word Count Example**

```java
import org.apache.kafka.clients.consumer.ConsumerConfig;
import org.apache.kafka.common.serialization.Serdes;
import org.apache.kafka.streams.KafkaStreams;
import org.apache.kafka.streams.StreamsBuilder;
import org.apache.kafka.streams.StreamsConfig;
import org.apache.kafka.streams.kstream.KStream;
import org.apache.kafka.streams.kstream.Materialized;
import org.apache.kafka.streams.kstream.Produced;

import java.util.Arrays;
import java.util.List;
import java.util.Properties;

public class WordCountStreams {
    public static void main(String[] args) {
        //1 define kafka streams config
        Properties props = new Properties();
        props.put(StreamsConfig.APPLICATION_ID_CONFIG, "word-count-app");
        props.put(StreamsConfig.BOOTSTRAP_SERVERS_CONFIG, "localhost:9092");
        props.put(StreamsConfig.DEFAULT_KEY_SERDE_CLASS_CONFIG, Serdes.String().getClass().getName());
        props.put(ConsumerConfig.AUTO_OFFSET_RESET_CONFIG, "earliest");
        props.put(StreamsConfig.DEFAULT_VALUE_SERDE_CLASS_CONFIG, Serdes.String().getClass().getName());
        props.put("file.encoding", "UTF-8");
//        props.put(StreamsConfig.CACHE_MAX_BYTES_BUFFERING_CONFIG, "0");

        // 2 build the stream processing topology
        StreamsBuilder builder = new StreamsBuilder();

        // 3 read from the input topic
        KStream<String, String> inputStream = builder.stream("sentences");

        // 4 process teh stream (split sentences into words and count them
        inputStream
                .flatMapValues((readOnlyKey, value) -> Arrays.asList(value.toLowerCase().split(" ")))
                .groupBy((key, word) -> word)
                .count(Materialized.with(Serdes.String(), Serdes.Long()))
                .toStream()
                .to("word-count", Produced.with(Serdes.String(), Serdes.Long()));

        // 5 build and start the kafka streams application
        KafkaStreams streams = new KafkaStreams(builder.build(), props);

        streams.start();

        // add shutdown hook for graceful exit
        Runtime.getRuntime().addShutdownHook(new Thread(streams::close));

        System.out.println("Kafka Streams Word Count Application Started!");
    }
}

```

---

### **Steps in the Example**

1. **Input Stream**: Sentences are read from `input-topic`. For example:
    
    ```
    "Hello world"
    "Kafka streams are powerful"
    
    ```
    
2. **Processing**:
    - `flatMapValues`: Splits each sentence into words.
    - `groupBy`: Groups the words for counting.
    - `count`: Counts occurrences of each word.
3. **Output Stream**: Results are written to `output-topic`:
    
    ```
    hello: 1
    world: 1
    kafka: 1
    streams: 1
    are: 1
    powerful: 1
    
    ```
    

---

### **How to Test the Example**

1. **Create Topics**:
    
    ```bash
    bin/windows/kafka-topics.bat --create --topic input-topic --bootstrap-server localhost:9092
    bin/windows/kafka-topics.bat --create --topic output-topic --bootstrap-server localhost:9092
    
    ```
    
2. **Produce Test Data**:
    
    ```bash
    bin/windows/kafka-console-producer.bat --topic input-topic --bootstrap-server localhost:9092
    > Hello Kafka Streams
    > Streams are awesome
    
    ```
    
3. **Consume Output Data**:
    
    ```bash
    bin/windows/kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic word-count --formatter org.apache.kafka.tools.consumer.DefaultMessageFormatter --property print.key=true --property print.value=true --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
    ```
