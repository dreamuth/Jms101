### Java Message Service (JMS) 101
###### Uttran Ishtalingam


## What is JMS
> JMS is a specification that provides a common way for Java programs to create, send, receive and read an enterprise messaging system’s messages
Note: JMS is used for Interprocess, host even inter data center communication 


### What is Enterprise messaging
> Enterprise messaging is that messages are delivered **asynchronously** from one system to others over a network

Note:
sender is not required to wait for the message to be received
each message is self-contained and carries all of the data and state needed


### Advantages of Messaging (JMS)


#### Advantages of Messaging (JMS)
## Heterogeneous integration


#### Advantages of Messaging (JMS)
## Loosely coupled communication


#### Advantages of Messaging (JMS)
## Asynchronous messaging


#### Advantages of Messaging (JMS)
## Reliable delivery


#### Advantages of Messaging (JMS)
## Centralized architecture
Note: invoke services from applications and systems that are implemented in completely different platforms.  JMS to non-Java or even non-JMS messaging
decouples sender & receiver. Clients see only the messaging server, not other clients,
Increase the clients dynamically
(A message is guaranteed to be delivered once and only once)


## JMS Version History
* JMS 1.0.2b (June 26, 2001)
* JMS 1.1 (April 12, 2002)
* JMS 2.0 (May 21, 2013)
Note: You can see that JMS 1.1 is used more than a decade and doesn't required any update. As part of Java EE 7 JMS 2.0 API was introduced and this new API is also called Simplified API. Because it require less code to be written for sending and receiving messages by introducing new Interfaces. Shared subscription is added on topic for scallability, Delayed delivery are some of them