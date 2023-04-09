AWs Integration & Messaging | SQS, SNS, Kinesis
==================

> deploying multiple applications, they will ivevitably need to communicate tiwh one another 

> using Messaging service, decouple each application and make safe each application

- SQS: queue model
- SNS: pub/sub model
- Kinesis: real-time streaming model

# SQS

> SQS Queue

> producer send Messages

> Cousumer poll messages

> decoupling apllications 

> using SDK 

> in cloudWatch, Queue length can be metrcis

- 가시성 시간 초과(중복되는 컨슈머 문제를 해결하기 위해 메세지를 polling 하면 처리되지 않더라도 큐에서 보이지 않음)

- 배달 못한 편지 -> Dead Letter queue 를 사용하여 debug 등으로 문제해결

- Delay queue 

> up to 15 min

- Long Polling

> 큐에 메시지가 없을 경우 api calls를 줄이기 위해 wait 하는 기능




# SNS


> send one message to multiple receivers

> pub / sub

* To Publist 

> Topic Publish (SDK)

> Direct Publish (for mobile apps SDK / Google GCm, Apple APNS, Amazon ADM)


## SNS + SQS Fan out 

> SNS Topic -> SQS Queue + SQS Queue ... 

## S3 Events to Multiple queues


## Kinesis

> collect, process, analyze streaming data in real-time

## Kinesis Data Streams

- Shards ...

> 데이터 스트림을 분석하는 사용자 정의 애플리케이션 개발에 사용

> 데이터를 받으면 일정 기간동안 내구성있게 데이터를 저장하기 위한 서비스 

## Kinesis Data Firehose:
> 데이터 스트림을 AWS 데이터 저장소에 적재(S3)
> 데이터를 입력받고 S3, redshift, elasticsearch로 전송

## Kinesis Data Analytics
> SQL을 사용하여 데이터 스트림 분석
> kinesis data stream + firehose와 연결하여 sql 검색 가능
> 수행 결과를 다시 data stream, firehose에 전달
> 스트리밍 소스에 연결 -> sql 코드 쉽게 작성 -> 지속적으로 sql 결과를 전달함

* 데이터를 처리하기 위한 2가지 컨셉
    - 스트림(in-memory table) -> 가상의 테이블 or view
    - 펌프(연속 쿼리) -> 실제 데이터를 앞서 만든 view에 넣어주는 역할

## Kinesis Video Streams
> 분석을 위한 비디오 스트림 캡쳐 및 처리, 저장

