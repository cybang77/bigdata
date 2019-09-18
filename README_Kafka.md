# 1. Zookeeper
Apache ZooKeeper is an effort to develop and maintain an open-source server which enables highly reliable distributed coordination.

```
sudo apt-get install zookeeperd
```

# 2. Kafka
Apache Kafka is a community distributed streaming platform capable of handling trillions of events a day.

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
