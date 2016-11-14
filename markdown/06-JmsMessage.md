## Message
* Anatomy of a JMS Message
* Message types


#### Message
## Anatomy of a JMS Message
* Headers
* Properties
* Payload
Note: Header - All messages support the same set of header fields. Header fields contain values used by both clients and providers to identify and route messages. Properties - Each message contains a built-in facility for supporting application-defined property values. Properties provide an efficient mechanism for supporting application-defined message filtering. Body - The JMS API defines several types of message body, which cover the majority of messaging styles currently in use.


## Message types


#### Message types
## Message
Note: The Message interface is the root interface of all JMS messages. A Message object holds all the standard message header information. It can be sent when a message containing only header information is sufficient.


#### Message types
## TextMessage
Note: A TextMessage object's message body contains a java.lang.String object. This message type can be used to transport plain-text messages, and XML messages.


#### Message types
## ObjectMessage
Note: An ObjectMessage object's message body contains a Serializable Java object.


#### Message types
## BytesMessage
Note: A BytesMessage object's message body contains a stream of uninterpreted bytes. This message type is for literally encoding a body to match an existing message format. In many cases, it is possible to use one of the other body types, which are easier to use. Although the JMS API allows the use of message properties with byte messages, they are typically not used, since the inclusion of properties may affect the format.


#### Message types
## StreamMessage
Note: A StreamMessage object's message body contains a stream of primitive values in the Java programming language ("Java primitives"). It is filled and read sequentially.


#### Message types
## MapMessage
Note: A MapMessage object's message body contains a set of name-value pairs, where names are String objects, and values are Java primitives. The entries can be accessed sequentially or randomly by name. The order of the entries is undefined



#### Anatomy of a JMS Message
#### Headers
## JMSDestination
Note: Where the message will get delivered


#### Anatomy of a JMS Message
#### Headers
## JMSDeliveryMode
Note: Persistent or Non-Persistent


#### Anatomy of a JMS Message
#### Headers
## JMSMessageID
Note: The unique identifier of the message


#### Anatomy of a JMS Message
#### Headers
## JMSTimestamp
Note: The JMSTimestamp is set automatically by the message producer when the send operation is invoked.
The approximate time that the send operation was invoked


#### Anatomy of a JMS Message
#### Headers
## JMSExpiration
Note: A Message object can have an expiration date. The expiration date is useful for messages that are only relevant for a fixed amount of time. The expiration time for messages is set in milliseconds by the producer using the setTimeToLive() method


#### Anatomy of a JMS Message
#### Headers
## JMSRedelivered
Note: The JMSRedelivered header indicates if the message was redelivered to the consumer. The JMSRedelivered header is true if the message has been redelivered, and false if has not. A message may be marked as redelivered if a consumer failed to acknowledge delivery, or if the JMS provider is otherwise uncertain whether the consumer received the message.


#### Anatomy of a JMS Message
#### Headers
## JMSPriority
Note: Messages may be assigned a priority by the message producer when they are delivered. The message servers may use message’s priority to order delivery of messages to consumers; messages with a higher priority are delivered ahead of lower priority messages. If not specified, the message priority is set to a default value of 4


#### Anatomy of a JMS Message
#### Headers
## JMSReplyTo
Note: In some cases, a message producer may want the consumers to reply to a message. The JMSReplyTo header indicates which destination, if any, a JMS consumer should reply to. The JMSReplyTo header is set explicitly by the JMS client; its contents will be a javax.jms.Destination object (either Topic or Queue).


#### Anatomy of a JMS Message
#### Headers
## JMSCorrelationID
Note: The JMSCorrelationID provides a header for associating the current message with some previous message or application-specific ID. In most cases, the JMSCorrelationID will be used to tag a message as a reply to a previous message


#### Anatomy of a JMS Message
## Properties
Note: Message properties are additional headers that can be assigned to a message. They provide the application developer or JMS vendor with the ability to attach more information to a message.


#### Anatomy of a JMS Message
## Payload
Note: Actual message payload, Stream, bytes, object, text and map
