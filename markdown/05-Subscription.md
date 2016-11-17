## Connection


#### How to create a connection
## Providers connection factory
```java
final Connection connection =
    new ActiveMQConnectionFactory("tcp://localhost:61616").createConnection();
```


#### How to create a connection
### JNDI
(Java Naming and Directory Interface)
```java
    final Connection connection =
        context.getConnectionFactory().createConnection();
```
Note: JNDI is a standard Java extension that provides a uniform API for accessing a variety of directory and naming services



## Session


#### Message Acknowledgments
## Auto Acknowledge
```java
    final Session session =
        connection.createSession(false, Session.AUTO_ACKNOWLEDGE);
```
Note: With this acknowledgment mode, the session automatically acknowledges a client's receipt of a message either when the session has successfully returned from a call to receive or when the message listener the session has called to process the message successfully returns.


#### Message Acknowledgments
### Auto Acknowledge using blocking wait
```java
public void receiveMessage()
{
    // Create Connection, Session, Consumer
    ...  
    TextMessage message = (TextMessage) consumer.receive(); // Acknowledged
    // Process the message
    ...  
}
```


#### Message Acknowledgments
### Auto Acknowledge using callback
```java
public void onMessage(Message message)
{
    // Process the message
    ...
    ...
    ...
} // Acknowledged
```


#### Message Acknowledgments
## Dups OK Acknowledge
```java
    final Session session =
        connection.createSession(false, Session.DUPS_OK_ACKNOWLEDGE);
```
Note: This acknowledgment mode instructs the session to lazily acknowledge the delivery of messages. This is likely to result in the delivery of some duplicate messages if the JMS provider fails, so it should only be used by consumers that can tolerate duplicate messages. Use of this mode can reduce session overhead by minimizing the work the session does to prevent duplicates.


#### Message Acknowledgments
## Client Acknowledge
```java
    final Session session =
        connection.createSession(false, Session.CLIENT_ACKNOWLEDGE);
```
Note: With this acknowledgment mode, the client acknowledges a consumed message by calling the message's acknowledge method. 


#### Message Acknowledgments
## Client Acknowledge
```java
public void onMessage(Message message)
{
    // Process the message
    ...  
    message.acknowledge();
    ...
}
```


#### Message Acknowledgments
## Transacted Messages
```java
final Session session = connection.createSession(true , ???);
```


#### Message Acknowledgments
## Transacted Messages
```java
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
```


#### Session Summary
Session  | Delivery
------------ | -----
Auto | Only once
Dups OK | At least once
Client | Redelivery controls
Transacted | Rollback and Redelivery controls



## Subscription Types


#### Subscription Types
## Non-Durable Subscription
```java
    MessageConsumer consumer = session.createConsumer("TopicName");
```
Note: Nondurable subscribers receive messages only when they are actively listening on that topic. Otherwise, the message is gone


#### Subscription Types
## Durable Subscription
```java
    MessageConsumer consumer = session.createDurableConsumer(
        "TopicName",
        "SubscriptionName");
```
Note: Durable subscribers, on the other hand, will receive all messages sent to that topic, regardless of whether that subscriber is active or not


#### Subscription Types (JMS 2.0)
## Shared Subscriptions
Note: If you want to share the work load.


#### Subscription Types (JMS 2.0)
## Shared Non-Durable Subscriptions
```java
    MessageConsumer consumer = createSharedConsumer(
        "TopicName",
        "SharedSubscriptionName");
```


#### Subscription Types (JMS 2.0)
## Shared Durable Subscriptions
```java
    MessageConsumer consumer = createSharedDurableConsumer(
        "TopicName",
        "SharedSubscriptionName");
```


#### Subscription Summary
Subscription  | Behavior
------------ | -----
Non-Durable | Active only, No work distribution
Durable | Guaranty, No work distribution
Shared-Non-Durable (JMS 2.0) | Active only, Work distribution
Shared-Durable (JMS 2.0)| Guaranty, Work distribution
