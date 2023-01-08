
## Create a separate network

docker network create kafkanet

## Running a container with ZooKeeper
docker run -d --network=kafkanet --name=zookeeper -e ZOOKEEPER_CLIENT_PORT=2181 -e ZOOKEEPER_TICK_TIME=2000 -p 2181:2181 confluentinc/cp-zookeeper

## Running a container with Kafka
docker run -d --network=kafkanet --name=kafka -e KAFKA_ZOOKEEPER_CONNECT=zookeeper:2181 -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://localhost:9092 -e KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR=1 -p 9092:9092 confluentinc/cp-kafka

## Optional (Working with kafka via console):

## Connect to Kafka container
docker exec -it kafka bash

## Create demo-topic
/bin/kafka-topics --create --topic demo-topic --bootstrap-server kafka:9092

## List all topics
/bin/kafka-topics --list --bootstrap-server kafka:9092

## Display a description of the created topic
/bin/kafka-topics --describe --topic demo-topic --bootstrap-server kafka:9092

## Generate messages
/bin/kafka-console-producer --topic demo-topic --bootstrap-server kafka:9092

## Read messages
/bin/kafka-console-consumer --topic demo-topic --from-beginning --bootstrap-server kafka:9092







