You can choose the most appropriate migration method based on your actual business scenarios to migrate your business data to the cloud by following the steps below. This guide is mainly for data migration from CVM to CKafka, which can be done over the private network. If access to data stream over the public network is required, you need to activate the public IP access for your CKafka instance first.

## Migrating Data to CKafka with Message Ordering Guarantees

The prerequisite for guaranteeing message ordering is to strictly limit data consumption to only one consumer. Therefore, timing of the migration is vital. The migration steps are as follows:

![Alt text](https://main.qcloudimg.com/raw/85c0ee0a869df5fbf294bdfc972f2084.png)

Detailed steps:

1. Create a CKafka instance and create a corresponding topic:
![Alt text](https://main.qcloudimg.com/raw/feb55a130b2e14b3942b34e41f4f8a17.png)

2. Switch the production flow so that the producer produces data to the CKafka instance.
 Change the IP in the broker-list to the VIP of the CKafka instance and topicName to the topic name in the CKafka instance:
```
 ./kafka-console-producer.sh --broker-list xxx.xxx.xxx.xxx:9092 --topic topicName
```

3. Original consumer does not need to be configured and can continue to consume the data in your self-built Kafka cluster. When the consumption is completed, make new consumers consume data in the CKafka cluster through the following configurations (let only one consumer consume the data to guarantee message ordering).

 To add a new consumer, configure the IP in --bootstrap-server to the VIP of the CKafka instance:
```
./kafka-console-consumer.sh --bootstrap-server xxx.xxx.xxx.xxx:9092 --from-beginning --new-consumer --topic topicName --consumer.config ../config/consumer.properties
```

4. New consumer continues to consume data in the CKafka cluster and the migration is completed (if the original consumer is a CVM instance, it can continue to consume the data).

>**Note:**
> The above commands are test commands. In actual business operations, just modify the broker address configured for the corresponding application and then restart the application.

## Migrating Data to CKafka Without Message Ordering Guarantees

If the requirement for message ordering is not high, it is possible to migrate the data while it is consumed by multiple consumers in parallel. The migration steps are as follows:

![Alt text](https://main.qcloudimg.com/raw/02342dc426a1ec0f5378071721923c7a.png)

Detailed steps:

1. Create a CKafka instance and create a corresponding topic:
![Alt text](https://main.qcloudimg.com/raw/feb55a130b2e14b3942b34e41f4f8a17.png)

2. Switch the production flow so that the producer produces data to the CKafka instance.

 Change the IP in the broker-list to the VIP of the CKafka instance and topicName to the topic name in the CKafka instance:
```
 ./kafka-console-producer.sh --broker-list xxx.xxx.xxx.xxx:9092 --topic topicName
```

3. Original consumer does not need to be configured and can continue to consume the data in your self-built Kafka cluster. Meanwhile, new consumers can be added to consume data in the CKafka cluster. After the data in the original self-built cluster is all consumed, the migration is completed (suitable for scenarios that do not require message ordering).

 Configure the IP in --bootstrap-server to the VIP of the CKafka instance:
```
./kafka-console-consumer.sh --bootstrap-server xxx.xxx.xxx.xxx:9092 --from-beginning --new-consumer --topic topicName --consumer.config ../config/consumer.properties
```

>**Note:**
> The above commands are test commands. In actual business operations, just modify the broker address configured for the corresponding application and then restart the application.
