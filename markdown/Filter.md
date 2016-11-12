## Message Filtering
* Message Selectors

Note: When message selectors are used, the consumer will receive only messages that apply to the specified filter
When a JMS consumer declares a message selector for a particular destination, the selector is applied only to messages delivered to that consumer. Every JMS client can have a different selector specified for each of its consumers.


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

Note: Add source code


## Message Acknowledgments


#### Message Acknowledgments
## AUTO_ACKNOWLEDGE


#### Message Acknowledgments
## DUPS_OK_ACKNOWLEDGE


#### Message Acknowledgments
## CLIENT_ACKNOWLEDGE


## Group Messages



## JNDI
#### Java Naming and Directory Interface
Note: JNDI is a standard Java extension that provides a uniform API for accessing a variety of directory and naming services



## Popular Design Patterns



#### Popular Design Patterns
### async fire-and-forget
![](image/fireNforget.png)


#### Popular Design Patterns
### async request/reply
![](image/ReqResponse.png)



## References
* https://en.wikipedia.org/wiki/Java_Message_Service
* Java Message Service, 2nd Edition by David A Chappell, Richard Monson-Haefel, Mark Richards
