#### Filtering Messages
### Receive coke price
```java
// Create Consumer for request message id
MessageConsumer consumer = session.createConsumer(
    context.lookupQueue("res Q"),
    "JMSCorrelationID = '" + requestMessage.getJMSMessageID() + "'")

// Receive response
```



#### Message Selectors
### More Examples
```java
String selector1 = "NumberOfOrders > 1";

String selector2 = "age >= 15 AND age <= 19";

String selector3 = "JMSType = 'car' AND color = 'blue' AND weight > 2500";

String selector3 = "releaseYear BETWEEN 1980 AND 1989"
```
