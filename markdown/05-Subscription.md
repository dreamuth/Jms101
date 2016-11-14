## Message Acknowledgments


#### Message Acknowledgments
## Auto Acknowledge
    final Session session =
        connection.createSession(false, Session.AUTO_ACKNOWLEDGE);

Note: With this acknowledgment mode, the session automatically acknowledges a client's receipt of a message either when the session has successfully returned from a call to receive or when the message listener the session has called to process the message successfully returns.


#### Message Acknowledgments
## Dups OK Acknowledge
    final Session session =
        connection.createSession(false, Session.DUPS_OK_ACKNOWLEDGE);
Note: This acknowledgment mode instructs the session to lazily acknowledge the delivery of messages. This is likely to result in the delivery of some duplicate messages if the JMS provider fails, so it should only be used by consumers that can tolerate duplicate messages. Use of this mode can reduce session overhead by minimizing the work the session does to prevent duplicates.


#### Message Acknowledgments
## Client Acknowledge
    final Session session =
        connection.createSession(false, Session.CLIENT_ACKNOWLEDGE);
Note: With this acknowledgment mode, the client acknowledges a consumed message by calling the message's acknowledge method. Acknowledging a consumed message acknowledges all messages that the session has consumed.


#### Message Acknowledgments
## Client Acknowledge
    public void onMessage(Message message)
    {
        try
        {
            // Process the message
            ...  
            message.acknowledge();
            ...
        }
        catch (JMSException e)
        {
            throw new IllegalStateException("Failed to process the message", e);
        }
    }


#### Message Acknowledgments
## Transacted Messages
    final Session session =
        connection.createSession(true , Session.AUTO_ACKNOWLEDGE);


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



## Subscription Types


#### Subscription Types
## Non-Durable Subscription
    MessageConsumer consumer = session.createConsumer("TopicName")
Note: Nondurable subscribers receive messages only when they are actively listening on that topic. Otherwise, the message is gone


#### Subscription Types
## Durable Subscription
    MessageConsumer consumer = session.createDurableConsumer(
        "TopicName",
        "SubscriptionName")
Note: Durable subscribers, on the other hand, will receive all messages sent to that topic, regardless of whether that subscriber is active or not


#### Subscription Types (JMS 2.0)
## Shared Subscriptions
Note: If you want to share the work load.


#### Subscription Types (JMS 2.0)
## Shared Non-Durable Subscriptions
    MessageConsumer consumer = createSharedConsumer(
        "TopicName",
        "SharedSubscriptionName")


#### Subscription Types (JMS 2.0)
## Shared Durable Subscriptions
    MessageConsumer consumer = createSharedDurableConsumer(
        "TopicName",
        "SharedSubscriptionName")
