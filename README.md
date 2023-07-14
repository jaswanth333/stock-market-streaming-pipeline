# Real-Time Stock Market Data Streaming and Analysis

## Introduction 
This project simulates the processing of streaming data with Kafka using Python, Amazon Web Services (AWS), Apache Kafka, Glue, Athena, and SQL.

## Architecture 
<img src="Architecture.jpg">

## Installation

Kafka Download
```
wget https://downloads.apache.org/kafka/3.5.0/kafka_2.12-3.5.0.tgz (check website and replace URL)

tar -xvf kafka_2.12-3.5.0.tgz
```
Java Download
```
sudo yum install java-1.8.0-openjdk
java -version
```
It is pointing to a private server, change server.properties so that it can run on public IP 

To do this, you can follow any of the 2 approaches shared below --
Do a "sudo nano config/server.properties" - change ADVERTISED_LISTENERS to public IP of the EC2 instance
```
sudo nano config/server.properties
change ADVERTISED_LISTENERS to public IP of the EC2 instance
```

Start Zookeeper:
```
cd kafka_2.12-3.5.0
bin/zookeeper-server-start.sh config/zookeeper.properties
```

Open another window to start Kafka
But first, ssh to your ec2 machine as done above

Start Kafka-server:
----------------------------------------
Duplicate the session & enter in a new console –
```
export KAFKA_HEAP_OPTS="-Xmx256M -Xms128M"
cd kafka_2.12-3.5.0
bin/kafka-server-start.sh config/server.properties
```
Create the topic:
-----------------------------
Duplicate the session & enter following in  new console 
```
cd kafka_2.12-3.5.0
bin/kafka-topics.sh --create --topic test1 --bootstrap-server Ec2publicIP:9092 --replication-factor 1 --partitions 1
```
Start Producer:
--------------------------
```
bin/kafka-console-producer.sh --topic test1 --bootstrap-server Ec2publicIP:9092
```
Start Consumer:
-------------------------
Duplicate the session & enter in a new console --
```
cd kafka_2.12-3.5.0
bin/kafka-console-consumer.sh --topic test1 --bootstrap-server Ec2publicIP:9092
```
