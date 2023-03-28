# Install Kafka with Zookeeper on Linux
## 1) Install Java JDK version 11

      wget -O- https://apt.corretto.aws/corretto.key | sudo apt-key add - 
      sudo add-apt-repository 'deb https://apt.corretto.aws stable main'
      sudo apt-get update; sudo apt-get install -y java-11-amazon-corretto-jdk


Upon completion, you should get a similar output when doing  `java -version`:


    openjdk version "11.0.18" 2023-01-17 LTS
    OpenJDK Runtime Environment Corretto-11.0.18.10.1 (build 11.0.18+10-LTS)
    OpenJDK 64-Bit Server VM Corretto-11.0.18.10.1 (build 11.0.18+10-LTS, mixed mode)


## 2) Install Apache Kafka

    cd /opt/
    
    sudo wget https://archive.apache.org/dist/kafka/3.0.0/kafka_2.13-3.0.0.tgz
    
    sudo tar xzf kafka_2.13-3.0.0.tgz
    
    cd kafka_2.13-3.0.0/
    
    vim ~/.bashrc
    
    PATH="$PATH:/opt/kafka_2.13-3.0.0/bin"

## 3) start zookeeper

    sudo /opt/kafka_2.13-3.0.0/bin/zookeeper-server-start.sh /opt/kafka_2.13-3.0.0/config/zookeeper.properties
    
    ss -tuna | grep 2181
   
## 4) start kafka

    sudo /opt/kafka_2.13-3.0.0/bin/kafka-server-start.sh /opt/kafka_2.13-3.0.0/config/server.properties
    
    ss -tuna | grep 9092

## 5) Changing the Kafka and Zookeeper data storage directory

For Zookeeper edit the zookeeper.properties file

    sudo vim /opt/kafka_2.13-3.0.0/config/zookeeper.properties 
    
    >>> dataDir=/opt/kafka_2.13-3.0.0/data/zookeeper
    
For kafka edit the server.properties file

    sudo vim /opt/kafka_2.13-3.0.0/config/server.properties
    
    >>> log.dirs=/opt/kafka_2.13-3.0.0/data/kafka

## 6) Create first topic

    kafka-topics.sh --bootstrap-server localhost:9092 --topic first_topic --create --partitions 3 --replication-factor 1

    kafka-topics.sh --bootstrap-server localhost:9092 --list

    kafka-topics.sh --bootstrap-server localhost:9092 --describe --topic first_topic
    
## 7) Producer & Consumer

    kafka-console-producer.sh --bootstrap-server localhost:9092 --topic first_topic

    kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic first_topic --from-beginning
    
