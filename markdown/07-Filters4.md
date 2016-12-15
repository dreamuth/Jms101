#### Filtering Messages
### Send coke price (Producer 3)
```java
// Send the response
Message responseMessage = session.createTextMessage("40 INR");
responseMessage.setJMSCorrelationID(requestMessage.getJMSMessageID());
producer.send(responseMessage);
```
