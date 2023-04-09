Serverless
=============

> virtual Functions - no server! Don't need to provision server!

> Limited by time - short executions

> Run on-demand / 

> Scaling is automated

## service using Lambda

- API Gateway
- Kinesis
- DynamoDB
- S3
- CloudFront
- CloudWatch Events EventBridge
- CloudWatch Logs
- SNS
- SQS
- Cognito


## Lambda - Synchronous Invocations

> CLI, SDK, API Gateway, Application Load Balancer
> Result is returned right away
> Error handling must happen client side(retries, Exponential backoff)

### Sysnchronous Invocations - services

1. User Invoked:
- Elastic Load Balancing
- Amazon Api Gateway
- Amazon CloudFront(Lambda@Edge)
- Amazon S3 Batch

2. Service Invoked
- Amazon Cognito
- AWS Step Functions

3. other Services
- Amazon Lex
- Amazon Alexa
- Amazon Kinesis Data Firehose

# Lambda Integration with ALB



## Asysnchronous Invocations

> S3, SNS, CloudWatch Events...

## CloudWatch Events / EventBridge

> Cron or Rate EventBridge rule -> trigger on time -> Aws Lambda Function perform a task

> CodePipeline EventBridge rule -> trigger on state changes -> AWS Lambda Function Perform a task

## Event Source Mapping

- Kinesis Data Streams 
- SNS & SQS FIFO queue
- DynamoDB Streams

* Lambda Event 소스 매핑 중요!

# VPC

> In VPC, can deploy Lambda

> lambda create ENI(Elastic Network Interface) in subnet

> AWSLambdaVPCAccessExecutionRole

> also, using Internet Gateway, Net 

> CPU-bound, then increase RAM

# lambda 속도 향상

> cpu-bound -> increase RAM

> cold start -> db.connection, sdk, etc, 함수를 실행하는 영역 바깥에 db 연결 등의 세팅을 종료할 경우 속도가 향상 됨(추후에 호출시 기억하고 있음)


# concurrency and Throttling

> reserved concurrency at the function level (== limit)

* 동기식 호출 

> throttling이 일어나 429 error 반환

* 비동기식 호출

> 재시도 후 DLQ로 이동 / 이후 지원 티켓을 열어 자원 추가

# Cold start & Provisioned Concurrency

+ cold Start

> New instance -> code is loaded and code outsice the handler run(init)

* Provisioned Concurrency

> in advance, Concurrency is allocated before the function is invoked 



# Lambda and CloudFormation

- Inline

> Use the Code.zipFile

> Cannot incloud function dependency

- S3

> Lambda zip in s3

> S3 bucket, s3key, s3objectVersion(versioned bucket)

# Lambda Layer

> Externalize Dependencies to re-use them




