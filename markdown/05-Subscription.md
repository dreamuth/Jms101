## Subscription Types


#### Subscription Types
## Non-Durable Subscription
    MessageConsumer consumer = session.createConsumer("TopicName")
Note: Nondurable subscribers receive messages only when they are actively listening on that topic. Otherwise, the message is gone


#### Subscription Types
## Durable Subscription
    MessageConsumer consumer = session.createDurableConsumer(
        "TopicName",
        "SubscriptionName")
Note: Durable subscribers, on the other hand, will receive all messages sent to that topic, regardless of whether that subscriber is active or not


#### Subscription Types (JMS 2.0)
## Shared Subscriptions
Note: If you want to share the work load.


#### Subscription Types (JMS 2.0)
## Shared Non-Durable Subscriptions
    MessageConsumer consumer = createSharedConsumer(
        "TopicName",
        "SharedSubscriptionName")


#### Subscription Types (JMS 2.0)
## Shared Durable Subscriptions
    MessageConsumer consumer = createSharedDurableConsumer(
        "TopicName",
        "SharedSubscriptionName")
