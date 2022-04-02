# accountability-solution
This repository includes a Docker-based accountability solution based on Sysdig, Librdkafka producer, Kafka and MongoDB. This approach aims to identify the causes that have triggered a set of specific events, thanks to the use of the syscalls run by the monitored system. Features such as being completely decoupled from the monitored system, real-time analysis and optimized querying make this solution an optimal choice when it comes to understanding the root causes of a system's behaviour. Different assessment scenarios have been developed to define the best strategy to reduce the impact of the audit process and logging tasks.

# Software artifacts
Sysdig (version 0.28.0)

Librdkafka (version 1.7.0)

Zookeeper (version 7.0.1)

Kafka (version 7.0.1)

Kafka-connect (version 7.0.1)

MongoDB (version 5.0.5)

MongoDB Atlas (version 5.0.6 Enterprise)

Docker-compose (version 1.26.0)

# Installation
Dependencies can be installed with [setup.sh](https://github.com/inflfb00/accountability-docker-solution/blob/main/setup.sh).
The kernel headers must be installed in the host operating system, before running sysdig.

# Configuration and usage
Host IP must be set in the Docker environment variable BROKER_KAFKA_ADVERTISED_HOST_NAME, defined in [.env](https://github.com/inflfb00/accountability-docker-solution/blob/main/.env#L13)
## Scenario i. ROS logging engine

## Scenario ii. Zookeeper, Kafka broker, Kafka connect, Librdkafka producer with Sysdig and MongoDB (local)

## Scenario iii. Zookeeper, Kafka broker, Kafka connect, Librdkafka producer with Sysdig and Atlas MongoDB

## Scenario iv. Zookeeper, Kafka broker, Kafka connect, Librdkafka producer with Sysdig and MongoDB (local) with TLSv1.3
MongoDB connection URI value must be assigned to the connection.uri property in [MongoSinkConnector.properties](https://github.com/inflfb00/accountability-docker-solution/blob/main/mongodb-kafka-connect/etc/MongoSinkConnector.properties) from Kafka connect, and in [sink-connect.sh](https://github.com/inflfb00/accountability-docker-solution/blob/main/kafka/scripts/sink-connect.sh) for the Kafka-MongoDB connector creation. For this scenario, this value should be equal to
```
mongodb://root:admin@mongo:27017/admin?ssl=true
```
The scenario can be deployed by running
```
docker-compose -f docker-compose-tls.yml up -d
```
ROS Docker image and workspace folder must be created by running [init_ros.sh](https://github.com/inflfb00/accountability-docker-solution/blob/main/ros/init_ros.sh).
Calls to loginfo() method should be commented in [talker.py](https://github.com/inflfb00/accountability-docker-solution/tree/main/ros/src/talker.py#L50) and in [listener.py](https://github.com/inflfb00/accountability-docker-solution/tree/main/ros/src/listener.py#L54).
ROS execution can be started from [ROS folder](https://github.com/inflfb00/accountability-docker-solution/tree/main/ros) by running. 
```
docker-compose up
```

## Scenario v. Zookeeper, Kafka broker, Kafka connect, Librdkafka producer with Sysdig and Atlas MongoDB with TLSv1.3
MongoDB connection URI value must be assigned to the connection.uri property in [MongoSinkConnector.properties](https://github.com/inflfb00/accountability-docker-solution/blob/main/mongodb-kafka-connect/etc/MongoSinkConnector.properties) from Kafka connect, and in [sink-connect.sh](https://github.com/inflfb00/accountability-docker-solution/blob/main/kafka/scripts/sink-connect.sh) for the Kafka-MongoDB connector creation. For this scenario, this value should be equal to
```
connection.uri=mongodb+srv://root:admin@cluster0.ecipx.mongodb.net/admin?ssl=true
```
The scenario can be deployed by running
```
docker-compose -f docker-compose-tls-atlas.yml up -d
```
ROS Docker image and workspace folder must be created by running [init_ros.sh](https://github.com/inflfb00/accountability-docker-solution/blob/main/ros/init_ros.sh).
Calls to loginfo() method should be commented in [talker.py](https://github.com/inflfb00/accountability-docker-solution/tree/main/ros/src/talker.py#L50) and in [listener.py](https://github.com/inflfb00/accountability-docker-solution/tree/main/ros/src/listener.py#L54).
ROS execution can be started from [ROS folder](https://github.com/inflfb00/accountability-docker-solution/tree/main/ros) by running. 
```
docker-compose up
```


