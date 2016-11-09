### Java Message Service (JMS) 101
###### Uttran Ishtalingam


### What is JMS
> This specification describes the objectives and functionality of the Java Message Service (JMS).


### What is JMS
> JMS provides a common way for Java programs to create, send, receive and read an enterprise messaging system’s messages


### What is JMS
> Enterprise messaging is that messages are delivered **asynchronously** from one system to others over a network

Note:
sender is not required to wait for the message to be received
each message is self-contained and carries all of the data and state needed



### Advantages of Messaging (JMS)
* Heterogeneous integration
* Centralized architecture
* Loosely coupled communication
* Asynchronous messaging
* Reliable delivery (A message is guaranteed to be delivered once and only once)

Note:
Heterogeneous - Using messaging you can invoke services from applications and systems that are implemented in completely different platforms. Depending on the vendor, it is possible to use JMS to communicate to non-Java or even non-JMS messaging clients

Enterprise messaging systems that use a centralized architecture rely on a message server (broker), is responsible for delivering messages from one messaging client to other messaging clients. The message server decouples a sending client from other receiving clients. Clients see only the messaging server, not other clients, which allows clients to be added and removed without affecting the system as a whole

Scalability - Increase the clients dynamically



### JMS Version History
* JMS 1.0.2b (June 26, 2001)
* JMS 1.1 (April 12, 2002)
* JMS 2.0 (May 21, 2013)


### JMS Elements
* JMS Provider
* JMS Client
* JMS producer/publisher
* JMS consumer/subscriber
* JMS Message
* JMS Queue
* JMS Topic
* JMS Message Models


## JMS Provider
A JMS provider is a messaging system that implements the JMS interfaces and provides administrative and control features.


## Provides (some of them)
* Amazon SQS with Java Messaging Library
* Azure Service Bus
* Apache ActiveMQ
* Apache Artemis
* Apache Apollo
* Apache Qpid
* OpenJMS
* RabbitMQ
* SonicMQ
* SwiftMQ

Note: Show all logos



### JMS Client
JMS clients are the programs or components, written in the Java programming language, that produce and consume messages.

* JMS producer/publisher
* JMS consumer/subscriber

Note: A JMS client can be both a message producer and a message consumer


### JMS Message
Messages are the objects that communicate information between JMS clients


### JMS Destination
A JMS destination is an object (a JMS queue or a JMS topic) that represents the target of messages that the client produces and the source of messages that the client consumes. In **point-to-point messaging**, destinations represent **queues**; in **publish/subscribe messaging**, destinations represent **topics**.


## Queue
A staging area that contains messages that have been sent and are waiting to be read (by only one consumer). A JMS queue only guarantees that each message is processed only once.

Note:  


## Topic
A distribution mechanism for publishing messages that are delivered to multiple subscribers.

Note: todo


## JMS Message Models
* Point To Point Messaging (p2p)
* Publish and Subscribe (pub/sub)

Note:  In the simplest sense, publish-and-subscribe is intended for a one-to-many broadcast of messages, while point-to-point is intended for one-to-one delivery of messages


## Point To Point Messaging
A queue is a destination to which producers send messages and a source from which receivers consume messages

Each message is delivered to only one receiver. Multiple receivers may listen on a queue, but each message in the queue may only be consumed by one of the queue’s receivers.

Messages are ordered. A queue delivers messages to consumers in the order they were placed in the queue by the message server. As messages are consumed, they are removed from the head of the queue (unless message priority is used).

There is no coupling of the producers to the consumers. Receivers and senders can be added dynamically at runtime, allowing the system to grow or shrink in complexity over time. (This is a characteristic of messaging systems in general.)

 Any number of producers can send messages to the queue, each message is guaranteed to be delivered, and consumed by one consumer

 Queues retain all messages sent to them until the messages are consumed or until the messages expire

With the p2p messaging model, the p2p receiver can either push or pull messages, depending on whether it uses the asynchronous onMessage() callback or a synchronous receive() method.



#### Point To Point Messaging
## async fire-and-forget
![](https://www.safaribooksonline.com/library/view/java-message-service/9780596802264/httpatomoreillycomsourceoreillyimages296952.png)


### async request/reply
![](https://www.safaribooksonline.com/library/view/java-message-service/9780596802264/httpatomoreillycomsourceoreillyimages296954.png)


## Publish and Subscribe
Zero or more consumers will receive the message.
The subscriber has to remain continuously active to receive messages, unless it has established a durable subscription. In that case, messages published while the subscriber is not connected will be redistributed whenever it reconnects.

Durable subscribers, on the other hand, will receive a copy of every message published, even if they are “offline” when the message is published.


Messages are exchanged through a virtual channel called a topic.

Each message is delivered to multiple message consumers, called subscribers. There are many types of subscribers, including durable, nondurable, and dynamic. These subscriber types are described later in this chapter.

The publisher generally does not know and is not aware of which subscribers are receiving the topic messages.

Messages are pushed to consumers, which means that consumers are delivered messages without having to request them. Messages are exchanged through a virtual channel called a topic. A topic is a destination where producers can publish, and subscribers can consume, messages. Messages delivered to a topic are automatically pushed to all qualified consumers.

As in enterprise messaging in general, there is no coupling of the producers to the consumers. Subscribers and publishers can be added dynamically at runtime, which allows the system to grow or shrink in complexity over time.

Every client that subscribes to a topic receives its own copy of messages published to that topic. A single message produced by one publisher may be copied and distributed to hundreds or even thousands of subscribers.



## What is durable subscriber?



## Connection
* JNDI Support
JNDI is a standard Java extension that provides a uniform API for accessing a variety of directory and naming services


## Message types
* Message
* TextMessage
* ObjectMessage
* BytesMessage
* StreamMessage
* MapMessage

Note:
* Message:
    This type has no payload. It is useful for simple event notification.
* TextMessage:
    This type carries a java.lang.String as its payload. It is useful for exchanging simple text messages and also for more complex character data, such as XML documents.
* ObjectMessage:
    This type carries a serializable Java object as its payload. It’s useful for exchanging Java objects.
* BytesMessage:
    This type carries an array of primitive bytes as its payload. It’s useful for exchanging data in an application’s native format, which may not be compatible with other existing Message types. It is also useful where JMS is used purely as a transport between two systems, and the message payload is opaque to the JMS client.
* StreamMessage:
    This type carries a stream of primitive Java types (int, double, char, etc.) as its payload. It provides a set of convenience methods for mapping a formatted stream of bytes to Java primitives. It’s an easy programming model when exchanging primitive application data in a fixed order.
* MapMessage:
    This type carries a set of name-value pairs as its payload. The payload is similar to a java.util.Properties object, except the values must be Java primitives or their wrappers. The MapMessage is useful for delivering keyed data.


## Anatomy of a JMS Message
### Headers
* JMSDestination
* JMSDeliveryMode
* JMSMessageID
* JMSTimestamp
* JMSExpiration
* JMSRedelivered
* JMSPriority
* JMSReplyTo
* JMSCorrelationID
* JMSType

Note: The message headers provide metadata about the message describing who or what created the message, when it was created, how long the data is valid, etc. The headers also contain routing information that describes the destination of the message (topic or queue), how a message should be acknowledged, and a lot more

### Properties
Properties act like additional headers that can be assigned to a message. They allow the developer to add additional opaque information about the message. They are also used to expose data used for message selectors when doing message filtering

messages can carry properties that can be defined and set by the JMS client. JMS consumers can choose to receive messages based on the values of certain headers and properties, using a special filtering mechanism called message selectors.

### Payload
Object, Bytes, Streams

## Message persistence
 The messages may be stored centrally (as is the case with centralized architectures) or locally, with each sending or receiving client (the solution used by decentralized architectures). While some vendors may still use a flat-file storage mechanism, most vendors use a database. Some may also use an intelligent combination of both. The forwarding mechanism is responsible for retrieving messages from storage and subsequently routing and delivering them.


## Message Filtering
### Message Selectors
When message selectors are used, the consumer will receive only messages that apply to the specified filter

When a JMS consumer declares a message selector for a particular destination, the selector is applied only to messages delivered to that consumer. Every JMS client can have a different selector specified for each of its consumers.



## Message Acknowledgments


## Transacted Messages


## Lost Connections and Retry


## Clustering


## JMX Support


## Load balancing


## References
* https://en.wikipedia.org/wiki/Java_Message_Service
* Java Message Service, 2nd Edition by David A Chappell, Richard Monson-Haefel, Mark Richards
