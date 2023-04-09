Cloud Formation
====================

> AWS 리소스들을 자동으로 생성해주는 IAC 도구
> AWS 구성을 재사용하기 쉽게 코드로 작성해두는 것

* Ansible과의 차이점 

> Ansible은 리소스 구성을 넘어서 서버 운영까지 자동화 : Devops에 더 가까움
> CloudFormation은 리소스 구성만 하는 말 그대로의 IaC

# 장점 

1. Cost

2. Productivity

3. Separation of concern

    - app, VPC, network의 Stack을 나눠 분산하여 개발 수행

4. Don't re-invent the wheel

> 저장이 가능하다는 점. 기록이 남는 다는 점의 이점 / 시간낭비 x


# Template 구조

1. AWS TemplateFormatVersion(포맷 버전)

- 템플릿의 기능 식별

2. Description

- 템플릿에 대한 설명
- 선택사항이긴 하나 템플릿에 대한 전체적인 설명을 해주는 게 좋다

3. Parameter

- 스택 생성시 넘겨지는 파라미터들
- 템플릿 내부에서 Ref 함수로 참조한다.

4. Resources(주내용)

- aws 내에서 생성될 리소스들을 뜻함
- Yaml에서의 구조 

# VPC 구성

```
# VPC Yaml file

VPC:
    Type: AWS::EC2::VPC
    Properties:
        CidrBlock: 10.0.0.0/16
        EnableDnsHostnames: true
        Tags:
            - keys: Name
              Value: myVPC
```


# parameters

> to provide inputs to your AWS CloudFormation template

> !Ref 를 사용하여 재참조하여 코드의 재사용을 높일 수 있음

```
Parameters:
  <ParameterLogicalID>:
    Type: <ParameterType>
    Default: <DefaultValue>
    Description: <ParameterDescription>
    AllowedValues:
      - <AllowedValue1>
      - <AllowedValue2>
    ConstraintDescription: <ConstraintDescription>

!Ref <ParameterLogicalID>

```

# Mappings

> fixed variables within your cloudFormation Template

> can handle to differentiate between different environments(dev, prod), regions, AMI, etc

> all the values are hardcoded within the template


```
Mappings:
    Mapping01:
        key01:
            Name: Value01
        key02: 
            Name: Value02
        key03:
            Name: Value03


RegionMap:
    us-east-1:
        "32": "ami----"
        "64": "ami----"
    us-west-1:
        "32": "ami----"
        "64": "ami----"
        ...

# reference Map

!FindMap [MapName, "TopLevelKey, SecondLevelKey]
```

# Outputs

> CloudForamtion의 stack이나 자원을 참조할 수 있게 하는 방식 

```
Outputs:
    <OutputLogicalID>:
        value: <OutputValue>
        Export:
            Name: <ExportName>
        
Outputs:
    BucketURL:
        Value: !GetAtt MyBucket.WebsitURL
        Export:
            Name: my-bucket-url

!ImportValue my-bucket-url
```

# Coditions

> control the creation of resources or outputs based on a condition

- Environments(dev/test/prod)
- aws Region
- parameters

```
And, Equals, If, Not, Or
!Equals[ !Ref EnvType, prod]
```


# Intrisic Funtion

- Ref
- Fn::GetAtt
- Fn::FindInMap
- Fn::ImportValue  -- import values in other templates
- Fn::Join  -- 배열 안의 값 합치기(delimeter 존재)
- Fn::Sub    -- 문자열 대체
- Condition Functions
   - Fn::If  
   - Fn::Not  
   - Fn::Equals

# Rollback 

# Drifts

# 참조 

https://honglab.tistory.com/82