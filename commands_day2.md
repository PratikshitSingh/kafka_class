KAFKA 101:

https://kiddcorp.signin.aws.amazon.com/console
User7
THEHART1234!


# Start zookeeper server
bin/zookeeper-server-start.sh config/zookeeper.properties &
 
# Start Kafka broker server
bin/kafka-server-start.sh config/server.properties &

# List all running java processes
jps -lm
  
user4:~/environment/kafka_2.12-3.8.0 $ jps -lm
2547 org.apache.zookeeper.server.quorum.QuorumPeerMain config/zookeeper.properties
4246 jdk.jcmd/sun.tools.jps.Jps -lm
3630 kafka.Kafka config/server.properties
 
# Create topic on the running broker
bin/kafka-topics.sh --create --topic quickstart-events --bootstrap-server localhost:9092

# List topics on the broker
bin/kafka-topics.sh --list --bootstrap-server localhost:9092

# Describe the topic
bin/kafka-topics.sh --describe --topic quickstart-events --bootstrap-server localhost:9092

# Start producer
bin/kafka-console-producer.sh --topic quickstart-events --bootstrap-server localhost:9092

# Start consumer and consume
bin/kafka-console-consumer.sh --topic quickstart-events --from-beginning --bootstrap-server localhost:9092

# Kafkacat
sudo apt install kafkacat

# See Kafka-cluster info
kafkacat -b localhost:9091 -L

# State a consumer in a consumer group
kafkacat -b localhost:9092 -C -G cg1 t1

# Describe all consumers in a CG
bin/kafka-consumer-groups.sh --bootstrap-server localhost:9091 --group cg1 --describe --members

# To find offset
bin/kafka-consumer-groups.sh --bootstrap-server localhost:9091 --group cg1 --describe

![image](https://github.com/user-attachments/assets/ae91ab13-60d9-47c2-9445-09ff11641887)


## File Source and Sink - Connector


# Connect test - To work with connectors
bin/kafka-topics.sh --create --bootstrap-server :9092 --topic connect-test

# Add following to connect-standalone.properties
plugin.path=/home/ubuntu/environment/kafka_2.12-3.8.0/libs/connect-file-3.8.0.jar

echo -e "foo\nbar" > test.txt
kafkacat -b localhost:9092 -C -G ct1 connect-test
bin/connect-standalone.sh config/connect-standalone.properties config/connect-file-source.properties config/connect-file-sink.properties
￼




# Running with Java class
mvn exec:java -Dexec.mainClass="com.kiddcorp.ProducerDemoWithCallback"

# Running a Java consumer java class
mvn exec:java -Dexec.mainClass="com.kiddcorp.ConsumerDemo"

