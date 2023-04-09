DynamoDB
==========

> NoSQL

## Basic

> Made of Tables

> Primary key(must be decided at creation time)

> max 400kb

## primary key

1. Partition key(Hash)

2. Partition key + sort key(Hash + Range)

# Read and Write 

> provisioned model and on-demand model

> every 24 hour, can change mode 

> RCU / WCU

> Burst Capacity : temporary exceed

> WCU capacity units upto 1 KB in size / ceil

> RCU capaticy units upto 4 KB in size / ceil

## Read / Strongly Consistent Read vs Eventually Consistent Read 

> One Strongly Consistent Read per second

> two eventually Consistent Reads per second


## Throttling

> ProvisionedThroughputExceededException

* Reason

1. Hot keys
2. Hot Partitions
3. Very large items

* Solution
> Exponential backoff
> Distribute partition keys
> if RCU issue, we can use DynamoDB Accelerator

# API

## Write

- PutItem
- UpdateItem
- Conditional Writes

## Read

- GetItem
> primary key (Hash , Hash + sort key)

## Scan 
> read entire tables

> filter can be used in client side 

> can use parallel 

## delete

- DeleteItem
- DeleteTable

## Batch

- BatchWriteItem
> upto 25 putItem and/or DeleteItem
> upto 16mb of data written, up to 400kb of data per item
> can't update items(use updateItem)

- BatchGetItem
> return items from one or more tables

# Index

1. Local Secondary Index

> alternative Sort key(Partition key)

> up to 5 Local Secodary Indexes per table

> at creation time

2. Global Secondary Index

> alternative Primary key(Hash or hash + range)

> Must provision RCU and WCU for the index

> can be added/modified after table creation

## Index and Throttling

1. GSI > can makes main table throttled

2. LSI > no special throttling considerations because using main tables's RCU, WCU

## PartiQL

> support Insert, Update, Select, Delete also Batch operations



## Optimistic Locking

> ensure an item hasn't changed before update/delete it

> each item has an attribute that acts as a version number

## DynamoDB Accelerator(DAX)

> inmemory Cache

> solve hot key problem

### DAX vs ElasiCache

- DAX

> Individual objects cache
> query & scan Cache

- Elastic Cache

> store Aggregation Result

# DynamoDB Streams

> Orderd streams of Item-level modifications (create/update/delete) in a table

> sent to kinesis Data Streams

> Read by AWS Lambda

> Read By Kinesis Client Library application

> Data Retention for up to 24 hours

# TTL

> expire time setting

# DynamoDB CLI

1. --projection-expression : one or more attributes to retrieve

2. --filter-expression: filter items before returned to you

3. Pagination

* --page-size : 한번에 가져오는 page size를 지정한 후 여러번 호출하여, 한 번에 모든 item을 가져와 시간초과가 나는 것을 방지
* --max-items : return next token
* --starting-token : specify the last NextToken to retrieve the next set of items


# DynamoDB Transaction

1. Read Mode

> Eventual Consistecy, Strong Consistency, Transactional


2. Write Mode

> standard, Transactional 


> Consume 2x WCUs & RCUs


## operations

1. TransactGetItems
> one or more GetItem operations

2. TransactWriteItems
> one or more PutItem, updateItem and DeleteItem operations

3. use Case:
> financial Transactions, managing orders, multiplayer games...


## Capacity Computations

1. Read

> N transactional writes per second, size M kb : N * (M / 4) * 2(transactional costs) 

2. Write

> N transactional writes per second, size M kb : N * (M / 1) * 2(transactional costs) 


# Session State Cache

> it's common to use DynamoDB to store session states

1. vs. ElastiCache
> in-memory, but dynamoDB is serverless
> both are key/value stores 
> in Auto Scaling group, using DynamoDB

2. vs. EFS
> Must be attached to EC2 instances as a network drive
> cannot use in lambda

3. vs. EBS and Instance Store
> EBS & instance Store can only be use for local caching, not shared caching


4. vs. S3
> S3 is higher latency, and not meant for small objects


# Write Sharding

> 특정 partition key에 집중될 경우 hot partition issue 가 생긴다.

> 위 문제를 해결하기 위해서는 partition 키에 suffix(random, calculate)를 붙여서 해결한다.





# Write Type

1. Concurrent Writes
> 덮어쓰기 문제
> 동시성 문제 해결해보자

2. Atomic Writes


3. Conditional Writes
> 특정 값일 때만 쓰기로 조건을 걸어 1개의 쓰기만 성공
> optimistic lock

4. Batch Writes




# Large Objects Pattern

> max Table size is 400 KB not match image or video

> then upload large object in S3 bucket

> and store metadata in dynamoDB

# Operations

1. Table clean up

+ option 1: Scan + DeleteItem
> very slow, consumes RCUs & WCU, expensive

* option 2: Drop Table + Recreate Table
> Fase, efficient, cheap

2. Copying DynamoDB Table

+ option 1: using AWS Data Pipeline 
+ option 2: Back up and restore into a new table
> Take some time
+ option 3: Scan + PutItem or BatchWriteItme
> Write your own code 



# Security & other features


* Security 
- VPC Endpoints available to access DynamoDB without using the Internet
- Access Fully controlled By IAM
- Encryption at rest using AWS KMS and in-transit using SSL/TLS

* Backup and Restore feature available

> Point-in-time Recovery (PITR) like RDS
> No performance impace

* Global Tables
> Multi-region, multi-active, fully replicated, high performance

* DynamoDB local
> can develop and test apps locally without accessing the DB web service(without internet)

* can migration to any DB service

