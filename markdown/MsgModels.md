## JMS Message Models
* Point To Point Messaging (p2p)
* Publish and Subscribe (pub/sub)

Note:  In the simplest sense, publish-and-subscribe is intended for a one-to-many broadcast of messages, while point-to-point is intended for one-to-one delivery of messages



### Publish and Subscribe
* Topic
* Delivered to multiple consumer (Subscribers)
* No coupling
* Each subscriber will have its own copy of the message
* Synchronous or Asynchronous


## Types subscriber
* Non-Durable subscriber
* Durable subscriber
* Dynamic subscriber


## Message types
* Message
* TextMessage
* ObjectMessage
* BytesMessage
* StreamMessage
* MapMessage


#### Anatomy of a JMS Message
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


#### Anatomy of a JMS Message
###  Properties
###  Payload


## Message delivery mode
* Non-Persistent
* Persistent
Note: DB or file system, its a property of a message, broker restart, slow
