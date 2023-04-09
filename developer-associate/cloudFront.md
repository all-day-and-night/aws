Cloud Front
=============

* Content Delivery Network(CDN)


> 콘텐츠를 효율적으로 전달하기 위해 여러 노드를 가진 네트워크에 데이터를 저장하여 제공하는 시스템

> ISP(Internet Service Provider)에 직접 연결되어 데이터를 전송하므로, 콘텐츠 병목을 피할 수 있음.

# CDN 특징

> 웹 페이지, 이미지, 동영상 등의 컨텐츠를 본래 서버에서 받아와 캐싱

> 해당 컨텐츠에 대한 요청이 들어오면 캐싱해 둔 컨텐츠 제공

> 컨텐츠를 제공하는 서버와 실제 요청 지점 간의 지리적 거리가 매우 먼 경우 or 통신 환경이 안 좋은 경우 
> 요청 지점의 cdn을 통해 빠르게 컨텐츠 제공 가능

> 서버의 요청이 필요없기 때문에 서버의 부하를 낮추는 효과 

# Edge location

> 컨텐츠가 캐싱되고 유저에게 제공되는 지점

> aws 가 cdn을 제공하기 위해서 만든 서비스인 cloudFront의 캐시서버(데이터 센터의 전 세계 네트워크)

> geo-ip를 통해 whitelist, blacklist 선정 가능

# Cloud Front vs. S3 Cross Region Replication

1. Cloud Front 
- Global edge network
- Files are cached for a TTL(maybe a day)
- Great for static content that must be available everywhere

2. S3 Cross Region Replication

- Must be setup for each region you want replication to happen
- Files are updated in near real-time
- Read only
- Great for dynamic content that needs to be available at low-latency in few regions


# signed urls

> temporary access 

> similar to pre-signed urls(in S3)

> use cookies. then one cookie help to access several files 