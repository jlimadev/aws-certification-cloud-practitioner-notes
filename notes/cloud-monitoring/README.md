# 🕐 Cloud Monitoring

- [CloudWatch Metrics](#cloudwatch-metrics)
- [CloudWatch alarms](#cloudwatch-alarms)
- [CloudWatch logs](#cloudwatch-logs)
- [CloudWatch Events - EventBridge](#cloudwatch-events)
- [CloudTrail](#cloudtrail)
- [X-Ray](#x---ray)
- [Service Health Dashboard](#service-health-dashboard)
- [Personal Health Dashboard](#personal-health-dashboard)
- [Summary](#summary)

## CloudWatch Metrics

CloudWatch provides metrics for every services in AWS. A Metric is a variable to monitor (CPU Utilization, NetworkIn…)

- Metrics have timestamps
- Can create CloudWatch dashboards of metrics
- Important Metrics:
  - EC2 instances: CPU Utilization (understanding the need of scale), Status Checks, Network (not RAM)
  - Default metrics every 5 minutes
  - Option for Detailed Monitoring ($$$): metrics every 1 minute
  - EBS volumes: Disk Read/Writes
  - S3 buckets: BucketSizeBytes, NumberOfObjects, AllRequests
  - Billing:Total Estimated Charge (only in us-east-1)
  - Service Limits: how much you’ve been using a service API
  - Custom metrics: we can create our own metrics

## CloudWatch Alarms

Alarms are use to trigger notifications for any metric. The alarms are customizable and we have multiple options (min, max, average, etc.). With CloudWatch Alarms we can:

- Auto Scaling: Scale In/Up or Scale Out/Down EC2 instances to a desired count
- EC2 Actions: stop, terminate, reboot or recover an EC2 instance
- SNS Notifications: send notifications into SNS topics
- Billing Alarms
- Choose a schedule to check metrics and evaluate alarms.
