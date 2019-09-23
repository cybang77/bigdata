# 1. Zookeeper
Apache ZooKeeper is an effort to develop and maintain an open-source server which enables highly reliable distributed coordination.

```
sudo apt-get install zookeeperd
```

# 2. Kafka
Apache Kafka is a community distributed streaming platform capable of handling trillions of events a day.

## 2.1 Settings

1\. Go to [Apache Kafka Download page](https://kafka.apache.org/downloads). Choose the Spark release (2.3.0). Click on the link "Download Kafka" to get the `tgz` package of the 2.3.0 Spark release. We will be using that in the rest of these guidelines but feel free to adapt to your version.

```
wget http://www-eu.apache.org/dist/kafka/2.3.0/kafka_2.11-2.3.0.tgz

```

2\. Uncompress that file into `/usr/local` by typing:

```
sudo tar xvzf kafka_2.11-2.3.0.tgz -C /usr/local/
```

3\. Create a shorter symlink of the directory that was just created using:

```
sudo ln -s /usr/local/kafka_2.11-2.3.0 /usr/local/kafka
```

Edit Zookeeper properties into `/usr/local/kafka_2.11-2.3.0/config/` by typing:

```bash
# /usr/local/kafka_2.11-2.3.0/config/zookeeper.properties

dataDir=/tmp/zookeeper
clientPort=2181
maxClientCnxns=0
initLimit=10
syncLimit=5

broker1=broker1_IP:2888:3888
broker2=broker2_IP:2888:3888
broker3=broker3_IP:2888:3888
```
Edit Kafka properties into `/usr/local/kafka_2.11-2.3.0/config/` by typing:

```bash
# /usr/local/kafka_2.11-2.3.0/config/server.properties

broker.id=broker1

listeners=PLAINTEXT://:9092
advertised.listeners=PLAINTEXT://broker1_IP:9092
advertised.host.name=broker1_IP
advertised.host.name=9092

zookeeper.connect=broker1_IP:2181

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