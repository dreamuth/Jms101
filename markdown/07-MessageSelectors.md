## Message Selectors
Based on a subset of the SQL92 conditional expression syntax.
Note: You can receive messages only which you are interested in by using message selectors. Only messages whose header or property values match your filter will be delivered to you. But message selectors cannot reference message body values (payload) 


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

Note: When message selectors are used, the consumer will receive only messages that apply to the specified filter
When a JMS consumer declares a message selector for a particular destination, the selector is applied only to messages delivered to that consumer. Every JMS client can have a different selector specified for each of its consumers.


#### Message Selectors
### Examples
    final String selector1 = "NumberOfOrders > 1";

    final String selector2 = "age >= 15 AND age <= 19";

    final String selector3 = "JMSType = 'car' AND color = 'blue' AND weight > 2500";

    final String selector3 = "releaseYear BETWEEN 1980 AND 1989"


## Message Acknowledgments


#### Message Acknowledgments
## Auto Acknowledge


#### Message Acknowledgments
## Dups OK Acknowledge


#### Message Acknowledgments
## Client Acknowledge


#### Message Acknowledgments
## Client Acknowledge
    public void onMessage(Message message)
    {
        try
        {
            // Process the message
            ...  
            message.acknowledge();
        }
        catch (JMSException e)
        {
            throw new IllegalStateException("Failed to process the message", e);
        }
    }


#### Message Acknowledgments
## Transacted Messages


#### Message Acknowledgments
## Transacted Messages
    public void onMessage(Message message)
    {
        try
        {
            // Process the message
            ...  
            session.commit();
        }
        catch (JMSException e)
        {
            session.rollback();
            throw new IllegalStateException("Failed to process the message", e);
        }
    }



## Group Messages


#### Group Messages
    ...
    // send an empty payload message starting the group
    BytesMessage msgStart = session.createBytesMessage();
    msgStart.setStringProperty("SequenceMarker", "START_SEQUENCE");
    sender.send(msgStart);

    // now send the messages
    TextMessage msg1 = session.createTextMessage(messagePayload);
    sender.send(msg1);
    TextMessage msg2 = session.createTextMessage(messagePayload);
    sender.send(msg2);
    ...

    // send an empty payload message ending the group
    BytesMessage msgEnd = session.createBytesMessage();
    msgEnd.setStringProperty("SequenceMarker", "END_SEQUENCE");
    sender.send(msgEnd);



## Message Delivery Mode


![](image/NonPersistence.png)


![](image/Persistence.png)
Note: DB or file system, its a property of a message, broker restart, slow


## JNDI
#### Java Naming and Directory Interface
Note: JNDI is a standard Java extension that provides a uniform API for accessing a variety of directory and naming services
