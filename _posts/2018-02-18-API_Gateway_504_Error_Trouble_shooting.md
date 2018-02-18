---
layout: post
title: API Gateway 504 Error Trouble shooting
---
API Gateway 504 Error

-------------

### 1. Open API
레저큐는 레저 상품을 제공하는 Open API를 운영하고 있다. API 서버는 Spring Data JPA로 개발되었고, AWS 서비스를 통해 제공하고 있다.

### 2. 504 Error 발생
Open API를 사용하고 있는 제휴사에서 상품 정보를 수집하는데 간헐적으로 504 Error가 발생하고 있다는 연락을 해왔다. 504 Error은 Gateway Timeout으로 엔드포인트에서 일정시간동안 유효한 응답을 받지 못했을때 나타나느 에러이다,
![504](http://xoxoms.github.io/images/4/504.png)

### 3. 504 Error 재현

### 4. AWS Support

### 5. AWS Load balancer

### 6. NLB + VPC Link API Gateway

### 7. 마무리