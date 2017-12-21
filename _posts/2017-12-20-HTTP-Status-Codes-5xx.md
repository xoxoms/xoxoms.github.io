---
layout: post
title: HTTP Status Codes - 5xx
---
What is the 5xx of HTTP Status Codes?

## HTTP Status Code

-------------
HTTP Status Code는 HTTP 상태코드로써 2XX 부터 5XX 까지로 구현되어 있는데 클라이언트가 서버에게 요청을 보냈을 때 무슨 일이 일어났는지를 말해준다.

*2XX* - 요청이 정상적으로 완료되었음

*3XX* - 리소스가 옮겨졌음(redirection)
 
*4XX* - 클라이언트가 잘못된 요청을 하여 요청을 완료하지 못했음

*5XX* - 서버에서 에러가 발생하여 요청을 완료하지 못했음

## 5xx ERRORS

-------------
클라이언트가 올바른 요청을 보냈음에도 서버에서 에러가 발생하는 경우가 있는데 이런 경우에 5xx ERROR를 의심해볼 수 있다.
5xx ERROR은 서버 제한에 걸린 것일 수도 있고 게이트웨이나 서버의 구성요소에서 발생한 에러일 수도 있다.

아래는 일반적인 서버의 구성을 나타내는 그림으로 5xx 에러의 이해를 돕기위해 첨부하였다.

![server architecture](http://xoxoms.github.io/images/HTTP-Status-Codes-5xx/architecture.png)

### 500 Internal Server Error

![500](http://xoxoms.github.io/images/HTTP-Status-Codes-5xx/500.png)

The server encountered an unexpected condition that prevented it from fulfilling the request.

서버가 요청을 처리하는 도중 예상치 못한 에러가 발생하는 경우.

### 501 Not Implemented

![501](http://xoxoms.github.io/images/HTTP-Status-Codes-5xx/501.png)

The server does not support the functionality required to fulfill the request.

서버가 요청사항을 수행하는 데 필요한 기능을 지원하지 않을 때 발생

### 502 Bad Gateway

![502](http://xoxoms.github.io/images/HTTP-Status-Codes-5xx/502.png)

The server, while acting as a gateway or proxy, received an invalid response from an inbound server it accessed while attempting to fulfill the request.

게이트웨이나 프록시의 역할을 수행하는 서버가 inbound 서버로 부터 유효하지 않은 응답을 받았을 때 발생. 

### 503 Service Unavailable

![503](http://xoxoms.github.io/images/HTTP-Status-Codes-5xx/503.png)

The server is currently unable to handle the request due to a temporary overload or scheduled maintenance, which will likely be alleviated after some delay.

서버의 트래픽이 갑자기 증가하거나 유지관리를 위해 다운되어 요청을 처리하지 못할 때 발생. 일시적인 장애로 시간이 지나면 정상으로 돌아옴을 의미한다. 

### 504 Gateway Timeout

![504](http://xoxoms.github.io/images/HTTP-Status-Codes-5xx/504.png)

The server, while acting as a gateway or proxy, did not receive a timely response from an upstream server it needed to access in order to complete the request.

게이트웨이나 프록시의 역할을 수행하는 서버가 upstream 서버에게 요청을 보냈지만 적절한 시간 내에 요청이 완료되지 못한 경우에 발생.


## HTTP Status Codes를 숙지한다면?

---
* 대략적인 에러 발생 위치와 원인을 판단하기 용이하므로 불필요한 삽질 최소화
* 에러가 발생했을 때 HTTP Status Codes를 이용하여 명확한 커뮤니케이션이 가능
* 그리고 또 뭐가 있을까요..???????


## 참고자료

---

HTTP 완벽가이드

[https://httpstatuses.com](https://httpstatuses.com)