Auto Scalining Group
======================

> 필요에 따라 서비스를 빠르게 확장하거나 축소할 수 있는 유연셩

> CPU, 메모리, 디스크, 네트워크 트래픽과 같은 시스템 자원들의 메트릭(Metric)값을 모니터링 하여 서버 사이즈를 자용으로 조정

# Scale up vs Scale out

1. Scale up

> 단순히 자원의 성능을 높이는 것

2. Scale out 

> 성능을 높이기 보다는 자원의 수를 늘리는 것 

> AWS의 경우 인스턴스의 수를 증가하여 트래픽 부하를 분산 

> Auto Scaling을 사용할 경우 트래픽과 부하에 따라 인스턴스의 수를 자동으로 조절가능 

# Purpose

1. 정확한 수의 EC2 인스턴스를 보유하도록 보장 

- 그룹의 최소 인스턴스 숫자와 최대 인스턴스 숫자 관리

2. 다양한 스케일링 정책 적용 가능 

- CPU의 부하에 따라 인스턴스 크기 늘리기/줄이기

3. 가용영역에 인스턴스가 골고루 분산될 수 있도록 인스턴스를 분배

- 서비스 장애가 발생하더라도 문제없이 서비스 이용 

## AWS Template

> Auto Scaling을 위해 생성해야 하는 서비스

> 커스텀 이미지 / 



## cpu 사용량 테스트 

```
$ sudo amazon-linux-extras install epel -y

$ sudo yum install stress -y

$ stress -c 4
```



>> 참고 
https://inpa.tistory.com/entry/AWS-%F0%9F%93%9A-EC2-%EC%98%A4%ED%86%A0-%EC%8A%A4%EC%BC%80%EC%9D%BC%EB%A7%81-ELB-%EB%A1%9C%EB%93%9C-%EB%B0%B8%EB%9F%B0%EC%84%9C-%EA%B0%9C%EB%85%90-%EA%B5%AC%EC%B6%95-%EC%84%B8%ED%8C%85-%F0%9F%92%AF-%EC%A0%95%EB%A6%AC
