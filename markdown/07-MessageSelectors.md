## Message Selectors
Based on a subset of the SQL92 conditional expression syntax.
Note:
You can receive messages only which you are interested in by using message selectors. Only messages whose header or property values match your filter will be delivered to you. But message selectors cannot reference message body values (payload). When message selectors are used, the consumer will receive only messages that apply to the specified filter
When a JMS consumer declares a message selector for a particular destination, the selector is applied only to messages delivered to that consumer. Every JMS client can have a different selector specified for each of its consumers.


#### Message Selectors
    // Send request to get stock price
    Message requestMessage = session.createObjectMessage("PRO");
    producer.send(requestMessage);

    // Wait for response for this specific request
    try (final DistributedConsumer consumer = new DistributedConsumer(
        session,
        connection.lookupQueue("responseQueue"),
        "JMSCorrelationID = '" + jmsRequestMessage.getJMSMessageID() + "'"))
    {
        final Message responseMessage = consumer.receive();
        logger.info("Stock price = " + responseMessage.getObject().toString());
    }


#### Message Selectors
### Examples
    final String selector1 = "NumberOfOrders > 1";

    final String selector2 = "age >= 15 AND age <= 19";

    final String selector3 = "JMSType = 'car' AND color = 'blue' AND weight > 2500";

    final String selector3 = "releaseYear BETWEEN 1980 AND 1989"



## Message Delivery Mode


![](image/NonPersistence.png)


![](image/Persistence.png)
Note: DB or file system, its a property of a message, broker restart, slow
