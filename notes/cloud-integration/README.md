# 🚦 Cloud Integration

When we start deploying multiple applications, they will inevitably need to communicate with one another. There are two patterns of application communication:
**Synchronous Communications**: An application communicating directly to another application. (Synchronous between applications can be problematic if there are sudden spikes of traffic)

**Asynchronous Communications** It is event driven and an application puts events or notifications in queues/streams and the other systems communicates with the queues if there is anything in there. The applications keeps decoupled from each other. In AWS we use the following services to Cloud Integrations with Asynchronous Communications:

- [Simple Queue Service](#simple-queue-service)
- [Simple Notification Service](#simple-notification-service)
- [AWS Kinesis](#aws-kinesis)
- [Amazon MQ](#amazon-mq)

## Simple Queue Service

## Simple Notification Service

## AWS Kinesis

## Amazon MQ
