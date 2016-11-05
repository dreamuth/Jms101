## Java Message Service (JMS) 101
#### Uttran Ishtalingam


### What is JMS
This specification describes the objectives and functionality of the Java Message Service (JMS).

JMS provides a common way for Java programs to create, send, receive and read an enterprise messaging system’s messages

Enterprise messaging is that messages are delivered **asynchronously** from one system to others over a network

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


### JMS producer/publisher
Note:


### JMS consumer/subscriber


### JMS Message
Messages are the objects that communicate information between JMS clients

## Queue
* Point to Point
* good
Note:  



## Topic
#### What is Topic
* One to many
Note: todo


## JMS Message Models
* Point To Point Messaging
* Publish and Subscribe


## Point To Point Messaging


## Publish and Subscribe



## Connection
* JNDI Support


## Message types
* Message
* TextMessage
* ObjectMessage
* BytesMessage
* StreamMessage
* MapMessage


## Anatomy of a JMS Message
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


## Message Filtering


## Message Acknowledgments


## Transacted Messages


## Lost Connections and Retry


## Clustering


## JMX Support


## Load balancing


## References
* https://en.wikipedia.org/wiki/Java_Message_Service
* Java Message Service, 2nd Edition by David A Chappell, Richard Monson-Haefel, Mark Richards
