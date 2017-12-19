---
layout: post
title: HTTP Status Codes - 5xx
---
What is the 5xx of HTTP Status Codes?

## HTTP Status

-------------
HTTP Status Code는 HTTP 상태코드로서 클라이언트가 서버에게 요청 메시지를 보냈을 때 무슨 일이 일어났는지를 말해준다.
상태 코드는 각 응답 메시지의 시작줄에 담겨 반환되는데 200에서 299까지의 상태 코드는 성공을, 300에서 399까지의 상태 코드는 리소스가 옮겨졌음을(redirection), 
400에서 499까지의 상태코드는 클라이언트가 뭔가 잘못된 요청했음을 의미하고 500에서 599까지의 코드는 서버에서 뭔가 실패했음을 의미한다.

## 5xx ERRORS

-------------
클라이언트가 올바른 요청을 보냈음에도 서버 자체에서 에러가 발생하는 경우가 있는데 클라이언트가 서버의 제한에 걸린 것일 수도 있고 혹은 게이트웨이 리소스와 같은 서버의 보조 구성요소에서 발생한 에러일 수도 있다.

아래는 일반적인 서버의 구성을 나타내는 그림으로 5xx 에러의 이해를 돕기위해 첨부하였다.

5xx 에러 설명에 등장하는 Gateway와 proxy는 Web Server로 inbound server와 upstream server는 Web Application Server라고 생각하면 된다.

![server architecture](http://xoxoms.github.io/images/architecture.png)

### 500 Internal Server Error
The server encountered an unexpected condition that prevented it from fulfilling the request.

서버가 처리할 수 없는 요청을 받았을 때 발생.

### 501 Not Implemented

The server does not support the functionality required to fulfill the request.

클라이언트가 요청한 기능을 서버가 지원하지 않을 때 발생.

### 502 Bad Gateway

The server, while acting as a gateway or proxy, received an invalid response from an inbound server it accessed while attempting to fulfill the request.

게이트웨이나 프록시의 역할을 수행하는 서버가 inbound 서버에 접근을 시도 했지만 유효하지 않은 응답을 받았을 때 발생. 

### 503 Service Unavailable

The server is currently unable to handle the request due to a temporary overload or scheduled maintenance, which will likely be alleviated after some delay.

서버의 트래픽이 갑자기 증가하여 요청을 처리하지 못할 때 발생. 일시적인 장애로 약간의 시간이 지나면 정상으로 돌아옴. 

### 504 Gateway Timeout

The server, while acting as a gateway or proxy, did not receive a timely response from an upstream server it needed to access in order to complete the request.

게이트웨이나 프록시의 역할을 수행하는 서버가 upstream 서버로 부터 적절한 시간내에 응답을 받지 못하여 요청을 완료할 수 없을 때 발생.


## 정리

---

누군가가 만들어 놓은 API를 사용할 때 예상하지 못한 응답을 받는 경우가 있는데 
HTTP Status Code를 잘 숙지하고 있다면 에러의 발생 위치와 원인을 대략적으로 알수있기 때문에 비정상 응답에 어떤 조치를 취해야할지 판단하기 용이하고 
이는 개발자 상호간의 커뮤니케이션과 개발 생산성에 큰 영향을 끼치므로 반드시 알고 넘어가야하는 내용이라고 생각한다. 

## 참고자료

---

[HTTP 완벽가이드](http://kyobobook.co.kr/product/detailViewKor.laf?mallGb=KOR&ejkGb=KOR&barcode=9788966261208)

[https://httpstatuses.com](https://httpstatuses.com)