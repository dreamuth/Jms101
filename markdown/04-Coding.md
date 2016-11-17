## How to send and receive messages


#### How to send a message (skeleton)
```java
// Step 1: Create Connection

// Step 2: Create Session

// Step 3: Create Producer

// Step 4: Create Message

// Step 5: Send Message
```


#### How to send a message (example)
```java
// Step 1: Create Connection
Connection connection = context.getConnectionFactory().createConnection();

// Step 2: Create Session
Session session = connection.createSession(false, Session.AUTO_ACKNOWLEDGE);

// Step 3: Create Producer
MessageProducer producer = session.createProducer(context.lookupQueue("Q1"))

// Step 4: Create Message
Message requestMessage = session.createTextMessage("Test Message");

// Step 5: Send Message
producer.send(requestMessage);
```


## How to receive a message
* Synchronously using blocking wait
* Asynchronously by registering Callback


#### How to receive a message
#### Synchronously using blocking wait (skeleton)
```java
// Step 1: Create Connection

// Step 2: Create Session

// Step 3: Create Consumer

// Step 4: Receive Message
```


#### How to receive a message
#### Synchronously using blocking wait (example)
```java
// Step 1: Create Connection
// Step 2: Create Session
// Step 3: Create Consumer
MessageConsumer consumer =
    session.createConsumer(context.lookupQueue("requestQueue"))

// Step 4: Receive Message
TextMessage message = (TextMessage) consumer.receive();
System.out.println(message.getText());
```


#### How to receive a message
### Blocking wait with timeout
```java
consumer.receive(TimeUnit.MINUTES.toMillis(10));
```


#### How to receive a message
#### Asynchronously by registering Callback (skeleton)
```java
// Step 1: Create Connection

// Step 2: Create Session

// Step 3: Create Consumer

// Step 4: Register Message Handler
```


#### How to receive a message
#### Asynchronously by registering Callback (example)
```java
// Step 1: Create Connection
// Step 2: Create Session
// Step 3: Create Consumer
// Step 4: Register Message Handler
consumer.setMessageListener(this);

@Override public void onMessage(Message message)
{
    System.out.println((TextMessage) message.getText());
}
```
