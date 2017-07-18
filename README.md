# README.md still under development

## Usage
After install vagrant and virtualbox on your desktop, you can clone this repo. After that, just bring up the environment whit ```vagrant up``` command, make sure you are in the right directory and Vagrantfile is on the same path where you type the command to start the provisioning.

Depending on how many hosts you require for your environment, you can change the host variables (zookeeper_boxes and kafka_boxes) on Vagrantfile.

As soon as you have your topology up and running, download the [kafka binaries](https://www.apache.org/dyn/closer.cgi?path=/kafka/0.10.2.1/kafka_2.12-0.10.2.1.tgz) to your desktop, expand the tarball and then test your environment with the commands bellow:

### First Terminal
```console
./kafka-topics.sh --create --topic MyTopic --replication-factor 1 --partitions 1 --zookeeper zookeeper1.local:2181,zookeeper2.local:2181,zookeeper3.local:2181  

./kafka-console-producer.sh --broker-list kafka1.local:9092,kafka2.local:9092,kafka3.local:9092 --topic MyTopic
```
Here, type some "Hello World" messages, then open a second terminal to consume those messages.


### Second Terminal
```console
./kafka-console-consumer.sh --bootstrap-server kafka1.local:9092,kafka2.local:9092,kafka3.local:9092 --topic MyTopic
```

Keep in mind that this is my personal laboratory, you can prepare you're production environment following this steps, but make sure you know what you're doing.
