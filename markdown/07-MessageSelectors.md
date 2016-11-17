## Filtering Messages


#### Filtering Messages
## Message Selectors
Based on a subset of the SQL92 conditional expression syntax.
Note:
You can receive messages only which you are interested in by using message selectors. Only messages whose header or property values match your filter will be delivered to you. But message selectors cannot reference message body values (payload). When message selectors are used, the consumer will receive only messages that apply to the specified filter
When a JMS consumer declares a message selector for a particular destination, the selector is applied only to messages delivered to that consumer. Every JMS client can have a different selector specified for each of its consumers.


![](image/Filter1.png)


#### Filtering Messages
### Ask Coke Price (Producer X)
```java
// Send request to get coke price
Message requestMessage = session.createTextMessage("COKE");
requestMessage.setStringProperty("Region", "INDIA")
producer.send(requestMessage);

// Receive response
```


![](image/Filter1.png)


#### Filtering Messages
### Receive request for India (Consumer 3)
```java
// Create Consumer for Region India
MessageConsumer consumer = session.createConsumer(
    context.lookupQueue("req Q"),
    "Region = 'INDIA'");

// Receive the request
```


![](image/Filter2.png)


#### Filtering Messages
### Send coke price (Producer 3)
```java
// Send the response
Message responseMessage = session.createTextMessage("40 INR");
responseMessage.setJMSCorrelationID(requestMessage.getJMSMessageID());
producer.send(responseMessage);
```


![](image/Filter3.png)


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
final String selector1 = "NumberOfOrders > 1";

final String selector2 = "age >= 15 AND age <= 19";

final String selector3 = "JMSType = 'car' AND color = 'blue' AND weight > 2500";

final String selector3 = "releaseYear BETWEEN 1980 AND 1989"
```


## Message Delivery Mode


![](image/NonPersistence.png)


![](image/Persistence.png)
Note: DB or file system, its a property of a message, broker restart, slow
