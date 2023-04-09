IAM
=========

# IAM  : Users & Groups 

- Users or Groups can be assigned JSON documents called pollicies


## aws IAM 계정 로그인 
 https://aws-admin-00001.signin.aws.amazon.com/console



 ## MFA (Multi Factor Authentication)

 - password + security device 

 - ex) google(1 - phone), Authy(multi), yubikey

 - root 계정에 사용하는 것 추천 / authy / 보안은 강력하나 물리적인 기기를 잃어버릴 경우 사용하기 힘듬

## AWS access 

- aws Management Console(password + MFA)

- aws Command Line Interface(CLI / access key)

- aws Software Developer kit(SDK / for code : protected by access key)

### access key 생성

- AWS console 에서 key 생성
- 다른 사용자와 공유 x 


## IAM Roles 

- AWS의 제품에 따라 사용할 수 있는 권한을 생성(Customizing)

## IAM Guidline & Best Practices

- AWS 계정 set up을 제외하고 root account 사용 x
- 하나의 유저는 하나의 aws user로 사용 / 계정 공유 x
- users는 groups로 권한을 할당
- 강력한 password policy 사용
- MFA(multi factor authentication) 사용
- aws service를 사용하기 위해 iam role 생성
- aws cli/sdk를 사용할 때는 access key 사용
- 계정 공유하지 마세요!

## IAM Section - Summary

* User: mapped to a physical user, has a password for AWS console
* Groups: contains users only
* Policies: JSON document that outlines permissions for users or groups
* Roles: for EC2 instances or AWS services
* Security: MFA + Password Policy
* Access keys: access AWS using the CLI or SDK
* Audit: IAM Credential Reports & IAM Access Advisor

### Note

* IAM policy는 하나 이상의 문으로 구성(Sid, Effect, Principal, Action, Resource, Condition)

* AWS Shared Responsibility Model에서 AWS의 책임은 : AWS infra





------------------------------------------------------------




# IAM(Identity and Access Management)

> 사용자의 접근 권한을 관리하는 서비스 

> 예를 들어 개발 부서 그룹은 EC2와 S3 서비스에 대한 엑세스 권한을 주고, DB 관리 부서는 RDS 엑세스 권한을 준다던지 세부 설정이 가능함 

> AWS 사용자 및 그룹을 만들고 관리 / AWS 리소스에 대한 액세스를 허용 및 거부 설정함으로써 전반적인 사용자 관리를 하는 서비스 

# IAM 기능 총 요약

1. 사용자 생성 / 관리 / 계정의 보안

> 사용자의 패스워드 정책 관리(일정 시간마다 pw 변경 등)

2. AWS 계정에 대한 공유 액세스 : aws 계정의 리소스 관리 및 권한을 다른 사람에게 부여 가능 

3. 세분화된 권한: 리소스에 따라 여러 사람에게 다양한 권한 부여 가능 

> 일부 사용자에게는 EC2 전체 액세스 권한, 일부에게는 S3 읽기전용 권한, 일부에게는 결제 정보에만 액세스할 수 있는 권한

4. EC2 애플리케이션 권한 자격 부여(IAM 역할 사용) : 사용자 뿐만 아니라 EC2에서 실행되는 어플리케이션에 IAM 기능을 이용해 자격증명 제공이 가능

> ex) 어떤 EC2나 S3 버킷이나 DynamoDB 테이블에 접근할 수 있는 액세스 권한을 지니도록 할 수 있다.

5. 멀티 팩터 인증(MFA)

> 보안 강화를 위해 암호, 액세스 키 이외에 디바이스 코드를 사용하여 인증

6. 자격증명 연동 : 기업 네트워크, 인터넷 자격 증명 공급자 같이 다른 곳에 이미 암호가 있는 사용자에게 AWS 계정에 대한 임시 액세스 권한 부여 가능 

7. 계정에 별명(alias) 부여 가능 (로그인 주소 생성 가능)

8. 글로벌 서비스 (리전 서비스 x): aws 계정은 전세계에서 유니크하다


참고  >> 
https://inpa.tistory.com/entry/AWS-%F0%9F%93%9A-IAM-%EA%B0%9C%EB%85%90-%EC%9B%90%EB%A6%ACuser-group-policy-role-IAM-%EA%B3%84%EC%A0%95-%EC%A0%95%EC%B1%85-%EC%83%9D%EC%84%B1





