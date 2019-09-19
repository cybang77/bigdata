# 1. Zookeeper
Apache ZooKeeper is an effort to develop and maintain an open-source server which enables highly reliable distributed coordination.

```
sudo apt-get install zookeeperd
```

# 2. Kafka
Apache Kafka is a community distributed streaming platform capable of handling trillions of events a day.

## 2.1 Settings

```
cd /usr/local/
wget http://www-eu.apache.org/dist/kafka/2.3.0/kafka_2.11-2.3.0.tgz
tar zxf .tgz

```

Edit Zookeeper properties into `/usr/local/kafka_2.11-2.3.0/config/` by typing:

```bash
# /usr/local/kafka_2.11-2.3.0/config/zookeeper.properties

dataDir=/tmp/zookeeper
clientPort=2181
maxClientCnxns=0
initLimit=10
syncLimit=5

broker1=192.168.0.37:2888:3888
broker2=192.168.0.38:2888:3888
broker3=192.168.0.39:2888:3888
```
Edit Kafka properties into `/usr/local/kafka_2.11-2.3.0/config/` by typing:

```bash
# /usr/local/kafka_2.11-2.3.0/config/server.properties

broker.id=broker1

listeners=PLAINTEXT://:9092
advertised.listeners=PLAINTEXT://192.168.0.37:9092
advertised.host.name=192.168.0.37
advertised.host.name=9092

zookeeper.connect=192.168.0.37:2181, 192.168.0.38:2181, 192.168.0.39:2181

zookeeper.connection.timeout.ms=6000
```
## 2.2 Run

To run Zookeeper

```bash
# /usr/local/kafka_2.11-2.3.0/
$ bin/zookeeper-server-start.sh config/zookeeper.properties
```

To run Kafka

```bash
# /usr/local/kafka_2.11-2.3.0/
$ bin/kafka-server-start.sh config/server.properties
```

To generate topic

```bash
# /usr/local/kafka_2.11-2.3.0/
/bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic bsnc
```

To check generated topic
```bash
# /usr/local/kafka_2.11-2.3.0/
bin/kafka-topics.sh --list --zookeeper localhost:2181
```

## 2.3 Test

Run Producer
```bash
# /usr/local/kafka_2.11-2.3.0/
bin/kafka-console-producer.sh --broker-list localhost:9092 --topic bsnc
```

Run Consumer
```bash
# /usr/local/kafka_2.11-2.3.0/
bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic bsnc --from-beginning
```