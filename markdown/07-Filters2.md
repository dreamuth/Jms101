#### Filtering Messages
### Ask Coke Price (Producer X)
```java
// Send request to get coke price
Message requestMessage = session.createTextMessage("COKE");
requestMessage.setStringProperty("Region", "INDIA")
producer.send(requestMessage);

// Receive response
```
