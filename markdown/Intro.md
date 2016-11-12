### Java Message Service (JMS) 101
###### Uttran Ishtalingam


## What is JMS
> JMS is a specification that provides a common way for Java programs to create, send, receive and read an enterprise messaging system’s messages


### What is Enterprise messaging
> Enterprise messaging is that messages are delivered **asynchronously** from one system to others over a network

Note:
sender is not required to wait for the message to be received
each message is self-contained and carries all of the data and state needed


### Advantages of Messaging (JMS)


#### Advantages of Messaging (JMS)
## Heterogeneous integration


#### Advantages of Messaging (JMS)
## Centralized architecture


#### Advantages of Messaging (JMS)
## Loosely coupled communication


#### Advantages of Messaging (JMS)
## Asynchronous messaging


#### Advantages of Messaging (JMS)
## Reliable delivery

Note: invoke services from applications and systems that are implemented in completely different platforms.  JMS to non-Java or even non-JMS messaging
decouples sender & receiver. Clients see only the messaging server, not other clients,
Increase the clients dynamically
(A message is guaranteed to be delivered once and only once)



## JMS Version History
* JMS 1.0.2b (June 26, 2001)
* JMS 1.1 (April 12, 2002)
* JMS 2.0 (May 21, 2013)


#### JMS Concepts
## Broker (Provider)
Note: A JMS provider is a messaging system that implements the JMS interfaces and provides administrative and control features.


## JMS Brokers
#### (some of them)
* Azure Service Bus
* Amazon SQS with Java Messaging Library
* Apache ActiveMQ
* Apache Artemis
* Apache Apollo
* Apache Qpid
* OpenJMS
* RabbitMQ
* SonicMQ
* SwiftMQ
* ...
Note: Show all logos


#### JMS Concepts
## Client


#### JMS Concepts
## Producer/Publisher


#### JMS Concepts
## Consumer/Subscriber


#### JMS Concepts
## Message


#### JMS Concepts
## Queue


#### JMS Concepts
## Topic



## JMS Client
JMS clients are the programs or components, written in the Java programming language, that produce and consume messages.

* JMS producer/publisher
* JMS consumer/subscriber

Note: A JMS client can be both a message producer and a message consumer


### JMS Client
![](image/Slide1.png)


### JMS Client
![](image/Slide2.png)


## JMS Message
Messages are the objects that communicate information between JMS clients
