## 3.1 Kafka连接器

### 3.1.1 Kafka连接器的版本介绍

Flink官方提供三种：  
- org.apache.flink:flink-connector-kafka_2.11:版本号，又名为universal

    ```xml
    <dependency>
        <groupId>org.apache.flink</groupId>
        <artifactId>flink-connector-kafka_2.11</artifactId>
        <version>1.11.2</version>
    </dependency>
    ```

- org.apache.flink:flink-connector-kafka-011_2.11:版本号，又名为0.11

    ```xml
    <dependency>
        <groupId>org.apache.flink</groupId>
        <artifactId>flink-connector-kafka-011_2.11</artifactId>
        <version>1.11.2</version>
    </dependency>
    ```

- org.apache.flink:flink-connector-kafka-010_2.11:版本号，又名为0.10

    ```xml
    <dependency>
        <groupId>org.apache.flink</groupId>
        <artifactId>flink-connector-kafka-010_2.11</artifactId>
        <version>1.11.2</version>
    </dependency>
    ```

    > 不支持exactly-once语义

Kafka的客户端高版本能兼容低版本，所以universal能兼容版本大于等于0.10.0的Kafka broker。但是对于版本为 0.11.x 和 0.10.x 的Kafka，更推荐使用 0.11 和 0.10 版本的Kafka连接器。

### 3.1.2 从Kafka读取数据



### 3.1.2 向Kafka写入数据

FlinkKafkaProducer构造器有多个重载，但最基础的构造器如下：  
```
private FlinkKafkaProducer(
			String defaultTopic,
			KeyedSerializationSchema<IN> keyedSchema,
			FlinkKafkaPartitioner<IN> customPartitioner,
			KafkaSerializationSchema<IN> kafkaSchema,
			Properties producerConfig,
			FlinkKafkaProducer.Semantic semantic,
			int kafkaProducersPoolSize)
```
- defaultTopic：指定数据即将写入的Topic
- keyedSchema：指定带Key类型消息的序列化方式
- customPartitioner：为消息指定发送的分区
- kafkaSchema：指定无Key类型消息的序列化方式
- producerConfig：传递给Kafka生产者的参数，只有`bootstrap.servers`参数是必须的（TODO:是否直接传递给Kafka生产者？是否经过转换？）
- semantic：写入数据时支持的语义，共包含三种语义：
    - EXACTLY_ONCE：保证数据不丢失不重复，需要和Checkpoint联合使用；
    - AT_LEAST_ONCE： 保证数据能发送到Broker，不会丢失
    - NONE： 消息可能会丢失，也可能会重复。
- kafkaProducersPoolSize：指定Kafka线程池的大小（TODO：如何实现？有何意义？）

> (TODO)该类经过大量的重构，需要看看最新Producer类如何使用。