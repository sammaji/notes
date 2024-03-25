To start a rabbitmq server locally, one way is to run the following command:
```bash
sudo docker run -it --rm --name rabbitmq -p 5672:5672 -p 15672:1
5672 rabbitmq:latest
```

## terminology
Some important terms related to rabbitmq:
### message broker
facilitates communication between different parts of a system. rabbitmq 
is a message broker.
### producer
component responsible for sending information.
### consumer
receives messages.
### messaging queue
place where messages are stored, until received by the consumer.
### exchange
Routing mechanism that determines how messages are delivered to queues. Producers send messages to exchanges, and exchanges route messages to one or more queues based on specific routing rules and criteria. Types -> direct, topic, headers, fanout.

## Work Queues

## Publish Subscribe
Publishers don't directly publish to any queue. Instead, they send it to an exchange, which sends it to a queue. The exchange can send it to one or more queues.

For a pub sub system, we would need to create a `fanout` exchange. It sends the messages to all the queues.

```python
channel.exchange_declare(exchange='logs', exchange_type='fanout')
```

Now we can use it the exchange while publishing. Messages will be sent to all the queues with the same `routing_key`

```python
channel.basic_publish(exchange='logs', routing_key='hello', body=message)
```

