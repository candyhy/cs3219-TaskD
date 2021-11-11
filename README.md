# cs3219-TaskD
## Instructions:
1.  Build docker file:
```
docker compose up -d
```

5. Run a bash shell in the Kafka server container by:
```
docker exec -it cs3219-taskd_kafka-server1_1 bash
```

6. Create kafka topic named testTopic to produce and consume messages from
```
kafka-topics --create --topic testTopic --bootstrap-server kafka-server1:9092 --replication-factor 2 --partitions 3
```

7. Start Console producer clients:
```
kafka-console-producer --broker-list localhost:9092 localhost:9093 localhost: 9094 --topic testTopic
```

8. Start another bash shell in the Kafka server contatiner by: 
```
docker exec -it cs3219-taskd_kafka-server1_1 bash
```

9. Start console consumer clients:
```
kafka-console-consumer --bootstrap-server localhost:9092 --topic testTopic --from-beginning
```

Now the console consumer client will listen and receive messages sent by the producer client

10. On a new terminal tab, start another bash shell in the Kafka server container:
```
docker exec -it cs3219-taskd_kafka-server1_1 bash
```

11. View the description of topic testTopic which contains Leader information:
```
kafka-topics --describe --topic testTopic --bootstrap-server localhost:9092
```

We can observe that testTopic has 3 Leaders 1, 2, 3

12. Now kill node 1 for another node to take over as master node:
```
docker restart cs3219-taskd_kafka-server1_1 
```

13. Run a new bash file by:
```
docker exec -it cs3219-taskd_kafka-server1_1 bash 
```

14. View the description of testTopic again:
```
kafka-topics --describe --topic testTopic --bootstrap-server localhost:9092
```

We can now see that there are only 2 distinct leaders and another node has taken over node 1
