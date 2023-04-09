Beanstalk
==============

# 특징

1. Managing infrastructure

2. Deploying code

3. Configuring all the databases, load balancers, etc

4. Scaling concerns

5. Most web apps have the same architecture(ALB + ASG)

6. All the developers want is for their code to run

7. Possibly, consistently across different applications and environments

> 웹 어플리케이션을 배포하고 확장하고 관리하는데 있어 쉽고 빠르게 할 수 있도록 돕는 완전 관리형 서비스 

> 개발에 필요한 환경을 미리 구성해 놓으면 그 환경을 기반으로 auto scaling 및 다중 인스턴스 배포를 수월하게 할 수 있다.

> 업데이트 + 로그 관리 기능 지원

# 장점 

1. 시간 및 비용 절감

2. 사용에 따른 추가 요금 없음(리소스에 대해서만 비용 지불)

3. 빠르고 간단한 시작

4. 개발자 생산성

5. 완전한 자원 제어

6. 불필요한 자원 낭비 x

# 구성 시나리오 

1. 환경 전체 구성(Elastic BeanStalk)

2. load balancer 추가

3. Auto Scaling Group 설정

4. EC2 인스턴스 시작

5. 모든 구성 연결

6. DNS 설정하여 외부에 Publish

7. 로그 및 앱 버전 설정 s3에 저장

# Infra Structure 구성

1. 사용자 코드: 사용자는 애플리케이션 작성에만 집중
2. HTTP 서버
3. App 서버, 인터프리터
4. 운영체제
5. 호스트 


# 배포에 필요한 정보

1. 코드
2. 리전
3. 스택타입: php, node.js, .net, docker, java 등등
4. 단일 인스턴스 vs auto scaling, load balancing
5. 데이터베이스(RDS): 선택사항

# 업데이트 배포 정책

1. All at once:
> 모든 인스턴스에 동시에 새 버전 배포. 배포시간은 가장 짧지만 모든 인스턴스가 업데이트 되기 때문에 다운타임 발생

2. Rolling update
> 기존 인스턴스 중 일부를 배치단위로 선정하여 새 버전 배포. 업테이트 중인 배치 인스턴스에 대해서는 서비스가 작동하지 않을 수 있음
> 서비스 다운 타임을 방지하기 위해 특정 개수의 인스턴스들을 업데이트 하는 식으로 하여 다운 타임 방지

3. Rolling update with additional batch: 
> Rolling update 방식을 그대로 따르나, Rolling update 방식처럼 기존의 인스턴스 외에 추가 인스턴스를 구성하여 배포하는 방식
> 추가 인스턴스를 구성하기 때문에 Rolling update에 비해 배포 시간이 더 많이 걸리지만 배포 실패시의 영향은 더 적다.

4. Immutable:
> 기존의 인스턴스는 그대로 두고, 새로운 Auto Scaling 배치 그룹을 생성
> rolling update처럼 기존의 인스턴스에 변화 x 
> 새 배치 그룹에는 먼저 하나의 인스턴스 만을 붙여서 정상적으로 동작하는 지 체크한 후
> 정상일 경우 기존의 인스턴스 갯수만큼 배포 인스턴스들을 띄우게 된다.
> roll back이 빼름 

* Blue/Green 기법

> Environment 자체를 새로 생성하는 방식. 

> 기존의 환경을 clone하여 새로운 환경을 생성. 

> DNS가 다르기 때문에 기존 환경과 새로운 환경의 URL를 교체하는 작업

- 장점: 이전 환경이 실행 중이므로 빠른 롤백 가능. 다운 타임없이 배포 가능 / 실패하더라도 기존 인스턴스에 영향을 미치지 않는다.
- 단점: 새로운 환경이 생성되기 때문에 배치가 느리다. RDS는 따로 Clone이 안되기 때문에 별도의 복제가 필요하다.

# Traffic Splitting

- Canary Testing
> New application version is deployed to a temporary ASG with the same capacity

> if main ASG exists, create temporary ASG and split traffic very small

> and health check.

> and then according to the result of health check, rollback and migrate instances in temp ASG to main ASG

> no application down time




# Deployment Process

1. Describe dependencies
> requirement.txt for python, package.json for Node.js

2. Package code as zip and describe dependencies

3. Console: upload zip file(create new app version) and then deploy

4. CLI : create new app version using CLI(uploads zip) and tehn deploy


# Life cycle Policy

- can create 1000 application versions

- need to remove old versionsx

- Base on time or space

# Extension

- in zip file, there is yaml/json format file to extend elastic beanstalk

- extensions is .config 

- in root of source code, in the .ebextensions/ directory

- can add resource such as RDS, Elastic cache, DynamoDB...

# AMI(Custom Image) vs Custom Platform

1. Custom Image is to tweak an existing Beanstalk Platform(Python, Node.js, Java...)
2. Custom Platform is to create an Entirely new Beanstalk Platform


# 배포전략 참고

https://dev.classmethod.jp/articles/ci-cd-deployment-strategies-kr/