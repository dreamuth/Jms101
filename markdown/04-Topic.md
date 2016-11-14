#### Topic
## Publish/Subscribe Messaging (Pub-Sub)
Note: A distribution mechanism for publishing messages that are delivered to multiple subscribers.
In the simplest sense, publish-and-subscribe is intended for a one-to-many broadcast of messages


#### Topic
## Delivered to multiple consumer (Subscribers)


#### Topic
## Each subscriber will have its own copy of the message


#### Topic
## Synchronous or Asynchronous


#### Topic
## Topic will not hold messages
(If there is no waiting durable subscribers)



## How to send and receive messages


#### How to send a message
    try (
        final Connection connection = createConnection();
        final Session session = createSession();
        final Producer producer = createProducer())
    ) {
        createAndSendMessage();
    }
    catch (JMSException e)
    {
        // ... handle exception
    }


#### How to create connection
## JNDI
#### Java Naming and Directory Interface
    final Connection connection =
        context.getConnectionFactory().createConnection();

Note: JNDI is a standard Java extension that provides a uniform API for accessing a variety of directory and naming services


#### How to send a message (example)
    try (
        final Connection connection =
            context.getConnectionFactory().createConnection();
        final Session session =
            connection.createSession(false, Session.AUTO_ACKNOWLEDGE);
        final Producer producer =
            session.createProducer(context.lookupQueue("requestQueue"))
    ) {
        Message requestMessage = session.createTextMessage("Test Message");
        producer.send(requestMessage);
    }
    catch (JMSException e)
    {
        // ... handle exception
    }


#### How to receive a message synchronously
    try (
        final Connection connection = createConnection();
        final Session session = createSession();
        final Consumer consumer = createConsumer())
    ) {
        receiveMessage();
    }
    catch (JMSException e)
    {
        // ... handle exception
    }


#### How to receive a message synchronously (example)
    try (
        final Connection connection =
            context.getConnectionFactory().createConnection();
        final Session session =
            connection.createSession(false, Session.AUTO_ACKNOWLEDGE);
        final Producer consumer =
            session.createConsumer(context.lookupQueue("requestQueue"))
    ) {
        TextMessage message = (TextMessage) consumer.receive();
        System.out.println(message.getText());
    }
    catch (JMSException e)
    {
        // ... handle exception
    }


#### How to receive a message asynchronously
    @Override public void run()
    {
        try (
            final Connection connection = createConnection();
            final Session session = createSession();
            final Consumer consumer = createConsumer())
        ) {
            setMessageListener();
        }
    }
    @Override public void onMessage(Message message)
    {
        // Read message
    }


#### How to receive a message asynchronously (example)
    try (
        final Connection connection =
            context.getConnectionFactory().createConnection();
        final Session session =
            connection.createSession(false, Session.AUTO_ACKNOWLEDGE);
        final Producer consumer =
            session.createConsumer(context.lookupQueue("requestQueue"))
    ) {
        consumer.setMessageListener(this);
    }
    @Override public void onMessage(Message message)
    {
        System.out.println((TextMessage) message.getText());
    }
