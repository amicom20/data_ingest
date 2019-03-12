Creating a Kafka Topic
```
login as: training
training@192.168.115.134's password:
[training@localhost ~]$ kafka-topics --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic weblogs
Created topic "weblogs".
```

Kafka Topic list
```
[training@localhost ~]$ kafka-topics --list --zookeeper localhost:2181
weblogs
```

describe weblogs topic.
```
[training@localhost ~]$ kafka-topics --describe weblogs --zookeeper localhost:2181
Topic:weblogs   PartitionCount:1        ReplicationFactor:1     Configs:
        Topic: weblogs  Partition: 0    Leader: 0       Replicas: 0     Isr: 0
[training@localhost ~]$ kafka-topics --describe weblogs --zookeeper localhost:2181
Topic:weblogs   PartitionCount:1        ReplicationFactor:1     Configs:
        Topic: weblogs  Partition: 0    Leader: 0       Replicas: 0     Isr: 0
[training@localhost ~]$
```

Kafka producer (Start up and producing data)
```
login as: training
training@192.168.115.134's password:
[training@localhost ~]$
[training@localhost ~]$
[training@localhost ~]$ kafka-console-producer --broker-list localhost:9092 --topic weblogs
test weblog entry 1
test weblog entry 2
test weblog entry 3
test weblog entry 4
test weblog entry 5
test weblog entry 6
test weblog entry 7
```

Kafka consumer (start up and receving data)
```
login as: training
training@192.168.115.134's password:
[training@localhost ~]$ kafka-console-consumer --zookeeper localhost:2181 --topic weblogs --from-beginning
test weblog entry 1
test weblog entry 2
test weblog entry 3
test weblog entry 4
^CProcessed a total of 4 messages
[training@localhost ~]$ kafka-console-consumer --zookeeper localhost:2181 --topic weblogs
test weblog entry 7
```
