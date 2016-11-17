## Group Messages


### Group Messages
```java
    TextMessage msg1 = session.createTextMessage("Message 1");
    msg1.setStringProperty("JMSXGroupID", "Group1");
    sender.send(msg1);

    TextMessage msg2 = session.createTextMessage("Message 2");
    msg2.setStringProperty("JMSXGroupID", "Group1");
    sender.send(msg2);

    // Send more messages
    .
    .
    .

    TextMessage msgn = session.createTextMessage("Message n");
    msgn.setStringProperty("JMSXGroupID", "Group1");
    sender.send(msgn);
```


### How to reset Group
```java
    message.setIntProperty("JMSXGroupSeq", -1);
```
