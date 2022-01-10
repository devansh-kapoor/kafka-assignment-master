## Producer.java

### To produce message as object
Add your message in ProducerRecord
```java
for (int i = 1; i <= 10; i++){
    User user=new User(i,"Devansh",21,"B.Tech");
    kafkaProducer.send(new ProducerRecord("Devansh-topic",String.valueOf(user.getId()),user));
}
```
Here `Devansh-topic` is name of ***topic*** & `user` is object of **User** class

## Consumer.java
### To see consuming messages
Make sure you subscribed to the topic `Devansh-topic`
```java
List topics = new ArrayList();
topics.add("Devansh-topic");
kafkaConsumer.subscribe(topics);
```
### Writing Data into a file when consuming it
```java

while (true) {
        FileWriter fileWriter = new FileWriter("Devansh-json-kafka-data.txt", true);
        ConsumerRecords<String, User> consumerRecords = kafkaConsumer.poll(Duration.ofSeconds(1));
        for (ConsumerRecord<String, User> consumerRecord : consumerRecords) {
            System.out.printf(
                "Topic: %s, Partition: %d, Value: %s%n",
                consumerRecord.topic(),
                consumerRecord.partition(),
                consumerRecord.value().toString());
            fileWriter.write(consumerRecord.value().toString() + "\n");
        }
        fileWriter.flush();
        fileWriter.close();
}
```
### Then
Just run the `Consumer.java` file. A terminal will open and there you can see your all messages from beginning produced by Producer.

### In Devansh-json-kafka-data.txt
> {"id":1, "name":"Devansh", "age":21, "course":"B.Tech"}
> 
> {"id":2, "name":"Devansh", "age":21, "course":"B.Tech"}
> 
> {"id":3, "name":"Devansh", "age":21, "course":"B.Tech"}
> 
> {"id":4, "name":"Devansh", "age":21, "course":"B.Tech"}
> 
> {"id":5, "name":"Devansh", "age":21, "course":"B.Tech"}
> 

