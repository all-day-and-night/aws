VPC(Virtual Private Cloud)
========

> 사용자가 정의하는 aws 계정 사용자 전용 가상의 네트워크

> ip 주소 범위 선택, 서브넷 생성, 라우팅 테이블 및 네트워크 게이트웨이 구성 등을 커스터마이징 가능


* Subnet: Tied to an AZ, network partition of the VPC

* Internet Gateway: at the VPC level, provide internet Access

* NAT Gateway / Instance: give internet access to private subnets

* NACL: stateless, subnet rules for inbound ando outbound

* Security Groups: Stateful, operate at the EC2 instance level or ENI

* VPC Peering: Connet tow VPC with non overlapping IP ranges, non transitive

* VPC Endpoints: Provide private access to AWS Services within VPC

* VPC Flow Logs: network traffic logs

* Site to Site VPN: VPN over public internet between on-premises DC and AWS

* Direct Connect: direct private connection to a AWS

# 3-tier architecture

