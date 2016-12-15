## Filtering Messages



#### Filtering Messages
## Message Selectors
Based on a subset of the SQL92 conditional expression syntax.
Note:
You can receive messages only which you are interested in by using message selectors. Only messages whose header or property values match your filter will be delivered to you. But message selectors cannot reference message body values (payload). When message selectors are used, the consumer will receive only messages that apply to the specified filter
When a JMS consumer declares a message selector for a particular destination, the selector is applied only to messages delivered to that consumer. Every JMS client can have a different selector specified for each of its consumers.
