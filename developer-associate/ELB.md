ELB + ASG
============

1. 확장성(Scalability)

- vertical
> 수직적 확장(Scale up)


- horizontal 
> 수평적 확장(Scale out)


2. 고가용성(High Availability)

> to survive a data center loss

> multi Az(for horizontal Scalability)

# Elastic Load Balancing(ELB)

> servers that forward traffic to multiple servers downstream

> Spread load across multile downStream instances

> Expose a single point of access(DNS) to your application

> Seamlessly handle failures of downstream instances

> health check to your instance

> Provide SSL termination(HTTPS) for your websites

> Separate public traffic from private traffic

> 서로 다른 instance에 대한 하나의 엔드포인트를 제공하여 백엔드 인스턴스에 대한 고려없이(client) 동일한 엔드포인트로 요청을 전송할 수 있다.

# ELB 세션 유지 방법

1. Sticky Session 
- 한 사용자의 요청을 하나의 인스턴스와 연결하여 처리하게 만드는 기능
- ELB에서 독자적으로 발행한 쿠키를 사용하는 것과 애플리케이션에서 사용하는 것 중에 선택 가능

2. Elastic Cache 
- 모든 인스턴스에서 세션 정보를 공유하도록 할 수 있다.
- 내결함성, 가용성, 확장성을 고려하여 요즘에는 거의 이 기술을 이용 




# kinds of Managed Load Balancers

1. Classic Load Balancer

> 초기에 제공되던 서비스

> 서버의 기본 주소가 바뀌면 Load Balancer를 새로 생성해야하며 하나의 주소에 하나의 대상 그룹으로 밖에 못 보낸다.

> 데이터 수정/변경이 불가 / 포트, 헤더 등의 변경을 하지 못한다. 

2. Application Load Balancer

> OSI 7 layer에서 Application Layer를 다룸

> 사용자와 직접 접하는 계층으로 health check를 http/https 프로토콜을 사용하여 수행한다.

> application layer에는 http/https뿐만 아니라 FTP, DNS, DHCP, WebSocket 등 다양한 프로토콜 존재

> 단순 부하분산 뿐만 아니라 http/https 헤더 정보를 이용해 부하분산 실시(지능적인 라우팅 가능)

> 로드밸런서 하나만 설정하면 트래픽을 모니터링하여 각 대상 그룹에 라우팅

> path 뿐만 아니라 port에 따라 다른 대상 그룹으로 매핑할 수 있다. (Docker 환경에서 유용하게 작동)

> EC2이외에도 lambda, IP로 연결 가능 / 마이크로 아키텍처 구성에 좋음

> SSL 암복호화 대신 진행

- ALB는 L7단의 로드 밸런서를 지원
- ALB는 HTTP/HTTPS 프로토콜의 헤더를 보고 적절한 패킷으로 전송
- ALB는 IP주소 + 포트번호 + 패킷 내용을 보고 스위칭
- ALB는 IP 주소가 변동되기 때문에 Client에서 Access 할 ELB의 DNS Name을 이용
- ALB는 L7단을 지원하기 때문에 SSL 적용이 가능

3. network Load Balancer 

> Transport Layer 

> http 헤더를 사용하지 못하기 때문에 tcp + udp 요청을 받아들여 부하분산 실시

> 고성능 환경에서 부하분산에 적합한 솔루션

> elastic IP로 공인 IP를 고정할 수 있는 점

> ALB와 다르게 IP, DNS 둘다 사용가능

- NLB는 L4단의 로드 밸런서를 지원
- NLB는 TCP/IP 프로토콜의 헤더를 보고 적절한 패킷으로 전송
- NLB는 IP + 포트번호를 보고 스위칭
- NLB는 할당한 Elastic IP를 Static IP로 사용이 가능하여 DNS Name과 IP주소 모두 사용이 가능
- NLB는 SSL 적용이 인프라 단에서 불가능하여 애플리케이션에서 따로 적용해 주어야 합니다.



## ALB vs NLB

> nlb에 비해 7계층까지 확인하는 alb의 기능이 더 많음

> nlb는 network 계층까지만 확인하므로 alb보다 빠르다.

> 단순한 라우팅이 필요하고 트래픽이 극도로 많은 경우 alb 보다는 nlb를 사용하는 것이 적합

> alb는 path-based routing 가능 > path를 확인하여 특정 서버로 라우팅시켜야 할 경우 적합 (api gateway)

- ALB : 클라이언트가 웹화면을 요청하는 상황일 때(HTTP, HTTPS 프로토콜을 사용해서 어플리케이션 레벨에 접근할 때)
- NLB : 내부로 들어온 트래픽을 처리하고, 내부의 인스턴스로 트래픽을 전송할 때

4. Gateway Load Balancer 

> OSI 계층의 3계층인 network 계층에서 작동 

> 방화벽, 침입 탐지 및 방지 시스템, 심층 패킷 검사 시스템과 같은 가상 어플라이언스를 배포, 확장 및 관리 가능

> 트래픽이 ec2에 도달하기 전 먼저 트래픽을 검사하거나 분석하거나 인증하거나 로깅하는 작업 수행 할 수 있는 서비스

> 트래픽 체킹 역할


## Connection Draining(연결 드레이닝)

- 로드밸런서가 트래픽을 분산한 인스턴스가 특별한 이유로 종료시켜야 할 때
> 받은 트래픽을 모두 처리할 때까지 인스턴스의 종료를 지연시킨다 => 최종 요청을 보낸 사용자까지 처리한 후에 인스턴스의 연결을 종료 

##



>> 참고
https://inpa.tistory.com/entry/AWS-%F0%9F%93%9A-ELB-Elastic-Load-Balancer-%EA%B0%9C%EB%85%90-%EC%9B%90%EB%A6%AC-%EA%B5%AC%EC%B6%95-%EC%84%B8%ED%8C%85-CLB-ALB-NLB-GLB





