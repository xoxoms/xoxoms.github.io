---
layout: post
title: HTTP Status Codes - 5xx
---
What is the 5xx of HTTP Status Codes?

## HTTP Status

-------------
HTTP Status Code는 HTTP 상태코드로써 클라이언트가 서버에게 요청 메시지를 보냈을 때 무슨 일이 일어났는지를 말해준다.
상태 코드는 각 응답 메시지의 시작줄에 담겨 반환되는데 *200*에서 *299*까지의 상태 코드는 성공을, *300*에서 *399*까지의 상태 코드는 리소스가 옮겨졌음을(redirection), 
*400*에서 *499*까지의 상태코드는 클라이언트가 뭔가 잘못된 요청했음을 의미하고 *500*에서 *599*까지의 코드는 서버에서 뭔가 실패했음을 의미한다.

## 5xx ERRORS

-------------
클라이언트가 올바른 요청을 보냈음에도 서버 자체에서 에러가 발생하는 경우가 있는데 클라이언트가 서버의 제한에 걸린 것일 수도 있고 혹은 게이트웨이 리소스와 같은 서버의 보조 구성요소에서 발생한 에러일 수도 있다.

아래는 일반적인 서버의 구성을 나타내는 그림으로 5xx 에러의 이해를 돕기위해 첨부하였다.

5xx 에러 설명에 등장하는 Gateway와 proxy는 Web Server로 inbound server와 upstream server는 Web Application Server라고 생각하면 된다.

![server architecture](http://xoxoms.github.io/images/architecture.png)

### 500 Internal Server Error
The server encountered an unexpected condition that prevented it from fulfilling the request.

서버가 요청을 처리하는 도중 예상치 못한 에러가 발생하는 경우.

### 501 Not Implemented

The server does not support the functionality required to fulfill the request.

클라이언트가 요청한 기능을 서버가 지원하지 않을 때 발생.

### 502 Bad Gateway

The server, while acting as a gateway or proxy, received an invalid response from an inbound server it accessed while attempting to fulfill the request.

게이트웨이나 프록시의 역할을 수행하는 서버가 inbound 서버에 접근을 시도 했지만 유효하지 않은 응답을 받았을 때 발생. 

### 503 Service Unavailable

The server is currently unable to handle the request due to a temporary overload or scheduled maintenance, which will likely be alleviated after some delay.

서버의 트래픽이 갑자기 증가하거나 유지관리를 위해 다운되어 요청을 처리하지 못할 때 발생. 일시적인 장애로 시간이 지나면 정상으로 돌아옴을 의미한다. 

### 504 Gateway Timeout

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