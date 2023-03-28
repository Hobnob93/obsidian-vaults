#azure #az-204 

Topics can be used to send and receive messages
- Queue is often used for point-to-point (one-to-one) communication
- Topics are used in pub/sub (one-to-many) communication
	- NOT available in the Basic pricing tier!
	- Requires Standard or Premium

Multiple, independent subs can be attached to a topic.
They will work in the same way as with queues, as far as the receivers are concerned.
A sub to a topic can receive a copy of each message sent to that topic.
Subscriptions are named entities.

You can define rules on a subscription.
- A rule has a filter specifying condition for a message to be copied to a sub
- May contain optional extra action that modifies message metadata