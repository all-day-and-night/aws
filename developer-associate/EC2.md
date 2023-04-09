Elastic Cloud Computing
=========================


## ssh 연결
```
$ ssh -i EC2Tutorial.pem  ec2-user@{public ip} 

$ chmod 0400 {.pem 파일} 보안상 권한을 너무 열어두었기 때문에 권한 레벨 수정 

```

## 주의할 점

* aws cli로 IAM api 키를 호출하는 짓은 ㄴㄴ

## EC2 기초

* On demand
* Reserved instances
> 1 또는 3년 
> 긴 워크로드에 적합


* Savings Plans

* Spot instance
> 가장 저렴한 EC2 / 다른 서버의 빈 공간을 사용하여 저렴하게 사용할 수 있지만 EC2 인스턴스를 잃을 수 있어 안정성이 떨어짐

* Dedicated Hosts
> 규정 준수 요구 사항이 강한 회사나 라이선스 모델이 복잡한 소프트웨어에 적합 / 가장 비쌈

> 물리적 코어 및 기본 네트워크 소켓 가시성 기반으로 비용 청구 

* Capacity Reservations

* EC2 인스턴스 안팍의 트래픽 제어 / 보안 그룹을 사용하여 통신 규칙 customizing

* 컴퓨팅 최적화 EC2 인스턴스는 배치처리, 미디어 트랜스코딩, 고성능 웹 서버, 고성능 컴퓨팅, 과학 모델링 및 머신러닝, 전용 게임 서버에 적합

* 인스턴스 수행 전 소프트웨어 설치가 필요한 애플리케이션이면, bash script를 작성하여 사용자 데이터에서 스크립트 입력 > 인스턴스 실행 전 bash script 수행 > 소프트웨어 설치 후 인스턴스 실행

* 인메모리 데이터베이스를 사용하는 중요 애플리케이션일 경우 메모리 최적화 인스턴스 사용

* 스토리지 최적화 ec2 인스턴스는 대규모 데이터 셋에 대한 높은 순차 읽기/쓰기 액세스 권한이 필요한 워크로드에 필요 

* 