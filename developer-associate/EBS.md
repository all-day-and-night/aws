EBS Elastic Block Store
=========================

> EC2가 연산에 관한 (cpu, 메모리 등) 처리를 한다고 하면, EBS는 데이터를 저장하는 역할(SSD, HDD)을 한다.

> EC2에서 사용할 영구 블록 스토리지 볼륨을 제공

> 인스턴스가 종료되어도 별개로 작동하여 유지 가능 


## EBS Volume

> EBS로 생성한 디스크 하나하나 저장 단위 

> ex) C, D 드라이브 처럼 물리적 하드 드라이브로 나누는 단위


* Volume 유형 타입 

1. 범용(General Purpose of GP3) : SSD

2. 프로비저닝 된 IOPS(Provisioned IOPS or IO2) : SSD

> io1/ io2의 ebs 즉 IOPS 성능이 높은 ebs 만이 여러 인스턴스를 연결할 수 있다. 

3. Throughput Optimized HDD or st1

4. 콜드 HDD(SC1)

5. 마그네틱

* IOPS

> Ops per Sec





참고 >> 


https://inpa.tistory.com/entry/AWS-%F0%9F%93%9A-EBS-%EA%B0%9C%EB%85%90-%EC%82%AC%EC%9A%A9%EB%B2%95-%F0%9F%92%AF-%EC%A0%95%EB%A6%AC-EBS-Volume-%EC%B6%94%EA%B0%80%ED%95%98%EA%B8%B0