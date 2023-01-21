### Kafka Producer

```
import org.apache.kafka.clients.producer.KafkaProducer;
import org.apache.kafka.clients.producer.ProducerConfig;
import org.apache.kafka.clients.producer.ProducerRecord;
import org.apache.kafka.common.serialization.StringSerializer;

import java.util.Properties;

public class KafkaProducerExample {
    public static void main(String[] args) {
        Properties properties = new Properties();
        properties.setProperty(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG, "localhost:9092");
        properties.setProperty(ProducerConfig.KEY_SERIALIZER_CLASS_CONFIG, StringSerializer.class.getName());
        properties.setProperty(ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG, StringSerializer.class.getName());

        KafkaProducer<String, String> producer = new KafkaProducer<>(properties);

        ProducerRecord<String, String> record = new ProducerRecord<>("test", "hello world");
        producer.send(record);

        producer.flush();
        producer.close();
    }
}

```

### Kafka Consumer

```
import org.apache.kafka.clients.consumer.ConsumerConfig;
import org.apache.kafka.clients.consumer.ConsumerRecord;
import org.apache.kafka.clients.consumer.ConsumerRecords;
import org.apache.kafka.clients.consumer.KafkaConsumer;
import org.apache.kafka.common.serialization.StringDeserializer;

import java.time.Duration;
import java.util.Collections;
import java.util.Properties;

public class KafkaConsumerExample {
    public static void main(String[] args) {
        Properties properties = new Properties();
        properties.setProperty(ConsumerConfig.BOOTSTRAP_SERVERS_CONFIG, "localhost:9092");
        properties.setProperty(ConsumerConfig.GROUP_ID_CONFIG, "group1");
        properties.setProperty(ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class.getName());
        properties.setProperty(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class.getName());

        KafkaConsumer<String, String> consumer = new KafkaConsumer<>(properties);
        consumer.subscribe(Collections.singleton("test"));

        while (true) {
            ConsumerRecords<String, String> records = consumer.poll(Duration.ofMillis(100));
            for (ConsumerRecord<String, String> record : records) {
                System.out.println(record.value());
            }
        }
    }
}

```
---

### Partitioning stream of data in Kafka into Substreams
</br>
In Kafka, streams of data are represented as topics, and you can split a stream of data into substreams by using the concept of a "topic partition."

> A partition is a unit of parallelism in Kafka, and each partition can be consumed independently by a separate consumer. When you produce a message to a topic, it gets assigned to a partition based on the partitioning strategy. By default, messages are round-robin assigned to partitions.

You can create multiple partitions for a topic by using the kafka-topics command-line tool. For example, the following command creates a topic named "test" with 3 partitions:

```
kafka-topics --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 3 --topic test
```

Once the topic is created, you can produce messages to it as usual, and each message will be assigned to one of the partitions.

On the consumer side, you can use the Kafka Consumer API to read data from specific partitions. In the consumer application, you can use the subscribe method to subscribe to the topic and specify the partitions you want to consume.

You can also use the Kafka Streams API to split a stream of data into substreams. The Streams API provides a high-level abstraction for working with streams of data, and it allows you to create a topology of stream processors that can be used to filter, transform, and aggregate data.

> It's also worth noting that topic partitioning also allows you to scale out the consumption of data, by allowing multiple consumers to read from a topic in parallel. Each consumer group can read from a specific set of partitions, making it possible to process data in parallel and scale out the number of consumers as needed.

---

### Merging multiple data stream into single stream in Kafka
</br>
In Kafka, you can merge multiple streams of data into a single stream by using a technique called "topic merging."

One way to merge multiple streams is to use the Kafka Connect API to create a "sink connector" that reads data from multiple sources and writes it to a single destination topic. A sink connector can be configured to read data from multiple topics and write it to a single topic.

Another way to merge multiple streams is to use the Kafka Streams API. The Streams API provides a high-level abstraction for working with streams of data and it allows you to create a topology of stream processors that can be used to filter, transform, and aggregate data.

You can use the KStream#merge method to combine multiple KStreams into a single KStream. The merge method accepts a variable number of KStreams and returns a new KStream that contains all the records from the input streams.

Here's an example:
```
KStream<String, String> stream1 = ...;
KStream<String, String> stream2 = ...;
KStream<String, String> mergedStream = stream1.merge(stream2);
```

This will create a new stream, mergedStream, that contains all the records from both stream1 and stream2.

Alternatively, you can use the KStream#through method to write the output of one stream to another stream.

```
KStream<String, String> inputStream = ...;
KStream<String, String> outputStream = ...;
inputStream.through("output-topic");
```

This will write the output of inputStream to outputStream

> It's also worth noting that merging streams can be an intensive process, and it can introduce additional complexity to your data pipeline. It's important to understand the requirements of your use case, and to carefully consider the trade-offs between merging streams and maintaining separate streams.
