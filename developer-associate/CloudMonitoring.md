CloudWatch, X-ray, CloudTrail
=============================


# 1. CloudWatch

> can monitoring service in aws 

- Metrics: Collect and track key metrics
- Logs: Collect, monitor, analyze and store log files
- Events: Send notifications when certain events happen in your aws
- Alarms: React in real-time to metrics/events

## Example

1. EC2 인스턴스의 CPU 점유율을 보고싶다.

> EC2 : Namespace
> CPU : metric
> type of instance 별로 확인 : Dimension

## 1. Metrics(지표)

- CPU utilization / networking

## Metrics filter

> 지표 필터를 사용하여 더 심화된 작업 가능

- specific IP, Error Count... then alarms

## Alarms

- State
    - OK
    - INSUFFICIENT_DATA
    - ALARM
- Period
    - Length of time in seconds to evaluate the metric

- Alarms target

    - Ec2
    - AutoScaling
    - SNS

## Logs

- Log Groups
- Log stream 

- log repository

    - S3
    - Kinesis Data Streams

## Events

- Pattern : Intercept events from AWS Service
- Schedule or Cron




# 2. AWS X-Ray

> Trouble Shooting application performance and errors

> Distributed tracing of microservices

> Trace and debug application in producion environment

> Quick

## how to enable it in X-ray

1. your code(Java, Python, Go, Node, .NET) must import the aws X-ray SDK

- very little code modification needed
- calls to AWS Services / HTTP, HTTPS requests / database calls / queue calls
- Install the x-ray daemon or enable x-ray AWs Integration

## Trouble shooting

1. EC2 

- IAM role 
- X-ray daemon

2. Lambda

- IAM Role
- check X-ray code is imported 

# 3. CloudTrail

> Internal monitoring of API Calls being made

> Audit changes to AWS Resources by your users

> visible service in aws account



# CloudTrail vs CloudWatch vs X-Ray

* CloudTrail
> Audit Api calls by users/ services/ AWS console
> Useful to detact unauthorized calls or root cause of changes

* CloudWatch
> metrics overtime for monitoring
> Logs for storing application log
> alarms to send notifications in case of unexpected metrics

* X-Ray
> Automated Trace Alalysis & Central Service Map visualization
> Latency, Errors and Fault Analysis
> Request tracking across distributed systems
