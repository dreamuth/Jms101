### Java Message Service (JMS) 101
###### Uttran Ishtalingam


## What is JMS
Note: JMS is a specification that provides a common way for Java programs to create, send, receive and read an enterprise messaging system’s messages
Enterprise messaging is that messages are delivered **asynchronously** from one system to others over a network
JMS is used for Inter-process, host, inter data center communication
each message is self-contained and carries all of the data and state needed


### Advantages of Messaging (JMS)


#### Advantages of Messaging (JMS)
## Heterogeneous integration
Note: invoke services from applications and systems that are implemented in completely different platforms.  JMS to non-Java


#### Advantages of Messaging (JMS)
## Loosely coupled communication
Note: Clients see only the messaging server, not other clients, decouples sender & receiver.
Increase the clients dynamically,


#### Advantages of Messaging (JMS)
## Asynchronous messaging
Note: Clients don't need to request for message


#### Advantages of Messaging (JMS)
## Reliable delivery
Note: (A message is guaranteed to be delivered once and only once)


## JMS Version History
* JMS 1.0.2b (June 26, 2001)
* JMS 1.1 (April 12, 2002)
* JMS 2.0 (May 21, 2013)
Note: You can see that JMS 1.1 is used more than a decade and doesn't required any update. As part of Java EE 7 JMS 2.0 API was introduced and this new API is also called Simplified API. Because it require less code to be written for sending and receiving messages by introducing new Interfaces. Shared subscription and Delayed delivery are some of them
