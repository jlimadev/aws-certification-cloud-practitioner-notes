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
