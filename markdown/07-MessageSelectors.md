## Message Selectors
Based on a subset of the SQL92 conditional expression syntax.
Note:
You can receive messages only which you are interested in by using message selectors. Only messages whose header or property values match your filter will be delivered to you. But message selectors cannot reference message body values (payload). When message selectors are used, the consumer will receive only messages that apply to the specified filter
When a JMS consumer declares a message selector for a particular destination, the selector is applied only to messages delivered to that consumer. Every JMS client can have a different selector specified for each of its consumers.


#### Filtering Messages
## Creating filtered Consumer
```java
String messageSelector = ...
final MessageConsumer consumer = session.createConsumer(
    context.lookupQueue("responseQueue"),
    messageSelector)
```


#### Filtering Messages
## Message Selectors
`ReplyTo = 'Text'`  
`ReplyTo = 'Text'`  
`ReplyTo = 'Text'`  


#### Message Selectors
### Ask Coke Price
```java
// Send request to get coke price
Message requestMessage = session.createTextMessage("COKE");
requestMessage.setStringProperty("Region", "USA")
producer.send(requestMessage);

// Receive response
```


#### Message Selectors
## Send coke price
```java
// Receive the request
final MessageConsumer consumer = session.createConsumer(
    context.lookupQueue("requestQueue"),
    "Region = 'USA'")
final Message requestMessage = consumer.receive();

// Send the response
final MessageProducer producer =
    session.createProducer(context.lookupQueue("responseQueue"))

Message responseMessage = session.createTextMessage("1.5 USD");
responseMessage.setJMSCorrelationID(requestMessage.getJMSMessageID());
producer.send(responseMessage);
```


#### Message Selectors
## Receive coke price
```java
// Send request to get coke price
Message requestMessage = session.createTextMessage("COKE");
requestMessage.setStringProperty("Region", "USA")
producer.send(requestMessage);

// Receive response
final MessageConsumer consumer = session.createConsumer(
    context.lookupQueue("responseQueue"),
    "JMSCorrelationID = '" + requestMessage.getJMSMessageID() + "'")

final Message responseMessage = consumer.receive();
logger.info(
    "Coke price in USA = " + ((TextMessage)responseMessage).getText());
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
