AWS CLI, SDK, IAM
=================


```
$ aws -- -- (명령어) --dry-run ... (실제 사용하는 cli가 정상 작동하는지 확인하는 방법 / 실제 구동은 되지 않고 확인만)

# aws 서비스 구동시 오류 메세지는 보안을 위해 암호화되어 메세지 출력 / iam의 policy나 role을 통해 sts 복호화 권한을 받아 사용
$ aws sts decode-authorization-message "error-message-encoded"

# ec2 metadata에 접근
$ curl http://169.254.169.254/latest/meta-data/

# aws 계정 정보 접근
$ cat credentials

# 계정이 여러 개일 경우
# aws cli에  --profile 옵션을 달아주면 계정에 따른 iam 정책에 따라 aws service 사용가능
$ aws configure --profile "계정 이름" 

```

# MFA with CLI

> temporary session 생성 후 cli로 MFA 사용가능

> "STS GetSession Token" Api call

```
$ aws sts get-session-token  --serial-number "arn:-----"(자원 위치 정보) --token-code "------"(authy code에서 얻은 코드)
# MFA를 사용해서 얻은 임시적인 자격 증명으로 (AccessKeyId, SecretAccessKey, SessionToken, Expiration)

# 이렇게 얻은 credentials로 임시 aws 계정 접속 가능
$ aws configure --profile "---" 
# 임시로 얻은 정보 입력으로 로그인 

$ cat home/.aws/credentials
# credentials 파일에 접속하여 session token 입력


```


# SDK

> dynamoDB와 같은 서비스를 사용할 때 개발언어를 사용하여 aws 서비스 사용가능

> AWS cli는 Python SDK(Boto3) 사용

> default region : us-east-1

> DescribeInstances api for ec2 limits : 100 per sec

> GetObject on S3 limit: 5500 get per sec

> Exponential Backoff


# Aws Limits(Quotas)

> Running On-Demand Standard Instances: 1152 vCPU 사용가능

> 더 사용하고 싶으면 opening a ticket to request limit increase

> 더 사용하고 싶으면 using the Service Quotas API to request quata increase

# Exponential Backoff(Any AWS Service)

> ThrottilingException(조절오류) 발생한 경우 / api calls을 너무 많이 한 경우 생기는 문제

> 5xx server error occur then retry

> 4xx do not retry and backoff

> exponential Backoff는 대기 시간을 2의 제곱 수로 증가하면서 서버의 부하를 줄이는 방식

# AWS CLI Credentials Provider Chain

* order

1. Command line options /  ex) --region, --output, --profile

2. Environment vairables - AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, AWS_SESSION_TOKEN

3. CLI credentials file -aws configure /

4. CLI configuration file -aws configure

5. Container credentials - for ecs tasks

6. Instance profile credentials - for ec2 Intance Profiles

## java SDK

1. Java system properties - aws.accessKeyId and aws.secretKey
2. Environment variables - AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY
3. The defalut credential profiles file - ex at: ~/.aws/credentials, shared by many sdk
4. Amazon ECS container credentials - for ECS containers
5. Instance profile credentials - used on EC2 instances

## 자격증명 순서가 중요한 이유

> 특정 서비스에 접근할 수 있는 최소한의 권한을 부여했을 때 접근할 수 있는 자격에 대한 설정은 위와 같이 차례대로 확인한다.

> 때문에 우선순위가 높은 부분부터 권한 설정을 해야지 최소한의 권한을 부여할 수 있다.

> IAM의 역할 policy를 적극 활용하고 특정 서비스에 대한 최소한의 권한을 부여하여 안전하게 사용할 수 있다. 

> 자격증명을 코드로 저장하여 사용하지 말자!

# SigV4 request 

1. HTTP Header Option

2. Query String option(:S3 pre-signed URLs)

3. 