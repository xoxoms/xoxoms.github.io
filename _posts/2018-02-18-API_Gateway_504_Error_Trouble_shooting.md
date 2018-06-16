---
layout: post
title: API Gateway 504 Error Trouble shooting
---
API Gateway 504 Error

-------------

### 1. 레저큐 Open API
레저큐는 레저 상품이나 시설사의 정보를 제공하는 Open API를 운영하고 있다. Open API 가이드 문서를 보고 적절하게 개발 한다면 도메인이 레저나 오락시설과 거리가 먼 기업체라도 비교적 쉽게 레저 상품을 게시하고 취급할 수 있게 된다. 

아직은 상용하고 있는 제휴사가 Open API 서버는 



모든 API 서버가 그렇듯이 오토 스케일링에 적합한 AWS 내에서 서비스 하고 있다. 







### 2. 504 Error 발생
Open API를 사용하고 있는 제휴사에서 상품 정보를 수집하는데 간헐적으로 504 Error가 발생하고 있다는 연락을 해왔다. 504 Error는 Gateway Timeout으로 엔드포인트에서 일정시간동안 유효한 응답을 받지 못했을때 나타나느 에러이다.
![504](http://xoxoms.github.io/images/4/504.png)

### 3. 504 Error 재현

### 4. AWS Support

### 5. AWS Load balancer

### 6. NLB + VPC Link API Gateway

### 7. 마무리