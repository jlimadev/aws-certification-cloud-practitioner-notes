# 🚦 Cloud Integration

When we start deploying multiple applications, they will inevitably need to communicate with one another. There are two patterns of application communication:
**Synchronous Communications**: An application communicating directly to another application. (Synchronous between applications can be problematic if there are sudden spikes of traffic)

**Asynchronous Communications** It is event driven and an application puts events or notifications in queues/streams and the other systems communicates with the queues if there is anything in there. The applications keeps decoupled from each other. In AWS we use the following services to Cloud Integrations with Asynchronous Communications:

- [Simple Queue Service](#simple-queue-service)
- [Simple Notification Service](#simple-notification-service)
- [AWS Kinesis](#aws-kinesis)
- [Amazon MQ](#amazon-mq)
- [Summary](#summary)

## Simple Queue Service

First we need to understand how does a queue work: We have producers that generates message and stores it in a queue. Once this message is stored in a queue it can be read by consumers, who will be polling the message and process it, and after finish the processing it will delete the message from the queue.

Simple Queue Service (SQS) is one of the most old AWS Services and it is used to decouple between application tiers.

- Fully Managed and Serverless services + Auto scalable
- By default it keeps the message from 4 to 14 days and there is no limit of messages into the queue.
- Messages are delete after read by consumers
- Consumers share the work to to read messages & scale horizontally.

## Simple Notification Service

## AWS Kinesis

## Amazon MQ

## Summary

- SQS:
  - Queue service in AWS
  - Multiple Producers, messages are kept up to 14 days
  - Multiple Consumers share the read and delete messages when done
  - Used to decouple applications in AWS
- SNS:
  - Notification service in AWS (Pub/Sub)
  - Subscribers: Email, Lambda, SQS, HTTP, Mobile…
  - Multiple Subscribers, send all messages to all of them
  - No message retention
- Kinesis: real-time data streaming, persistence and analysis
- Amazon MQ: managed Apache MQ in the cloud (MQTT, AMQP.. protocols)

All these services can scale independently from our application!
