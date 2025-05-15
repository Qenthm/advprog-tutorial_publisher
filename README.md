# Reflection

## a. How much data will the publisher program send to the message broker in one run?

The publisher program sends 5 messages to the message broker in one run. Each message contains a `user_id` and a `user_name` as strings, serialized using the Borsh format. The total data sent is the sum of the sizes of these 5 serialized `UserCreatedEventMessage` structs, which depends on the length of the strings and serialization overhead.

## b. The url of: “amqp://guest:guest@localhost:5672” is the same as in the subscriber program, what does it mean?

This means both the publisher and subscriber are connecting to the same AMQP message broker instance (such as RabbitMQ) running locally on your computer, using the same credentials and port. This allows them to communicate through the same broker and exchange messages.

## Running RabbitMQ as message broker

Below is the screenshot of RabbitMQ running in Docker and accessed via the management UI:

![RabbitMQ Management UI](rabbitmq.jpg)

## Monitoring chart based on publisher

Below is the screenshot of the charts when running both publisher and subscriber:

![Monitoring chart](chart.jpg)

The spike visible in the monitoring chart corresponds to the moment when the publisher program sends its batch of 5 messages to the RabbitMQ broker. When the publisher runs, it quickly sends all messages in a short burst, causing a sudden increase (spike) in the message rate and throughput metrics shown in the chart. This spike directly reflects the activity of the publisher, as the broker receives and processes the incoming messages before they are consumed by the subscriber.
