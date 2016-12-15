#### Filtering Messages
### Receive request for India (Consumer 3)
```java
// Create Consumer for Region India
MessageConsumer consumer = session.createConsumer(
    context.lookupQueue("req Q"),
    "Region = 'INDIA'");

// Receive the request
```
