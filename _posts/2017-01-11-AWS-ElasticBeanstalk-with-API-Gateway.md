---
layout: post
title: AWS Elasticbeanstalk + API Gateway
---
Elasticbeanstal + API Gateway 설정 기록

-------------

가자고는 제휴사에게 상품 정보를 제공해주는 Open API 서버를 운영하고 있는데 얼마전부터 504에러가 발생하고 있다.

서버는 아래 그림과 같이 구성되어있다.

![architecture](http://xoxoms.github.io/images/2/cloud.png)

나는 504에러를 추적하기 위해 로그를 분석했지만 결과적으로 우리 endpint 내의 기능들은 모두 정상이었다. client는 60초동안 응답을 받지 못해 504 Gateway Timeout 응답 받았는데 우리 로그에는 길어도 10초 안에 모든 응답을 했던 것이다.

하여 public 하게 열려있는 classic loadbalancer가 아닌 network loadbalancer로 변경하고 외부에서의 연결을 차단하는 형태로 서버를 재구성하였는데 이 과정을 정리하기 위해 포스트를 남기게 되었다.
   
### 1. 배포 파일 준비 
AWS elasticbeanstalk는 war나 zip 두가지만 업로드할 수 있기 때문에 소스를 war로 패키징하여 준비한다. 만약 elasticbeanstalk의 loadbalancer의 타입이나 timezone 등의 초기설정을 바꾸려면 .ebextensions라는 directory를 만들고 거기에 설정 파일들을 넣은 후 .ebextensions directory와 war를 zip으로 압축한다. 

자세한 내용은 아래 링크 참고
 
[https://docs.aws.amazon.com/ko_kr/elasticbeanstalk/latest/dg/applications-sourcebundle.html](https://docs.aws.amazon.com/ko_kr/elasticbeanstalk/latest/dg/applications-sourcebundle.html)

### 2. elasticbeanstalk
#### 2.1. elasticbeanstalk appication 생성
우측 상단 새 애플리케이션 생성을 누르고 애플리케이션 이름을 적절하게 넣어주면 elasticbeanstalk application이 생성된다.
	
#### 2.2 application 환경 생성 (실제 loadbalancer와 EC2 인스턴스 환경 생성)

2.1에서 만든 application란에 있는 환경 생성 버튼을 누르면 환경 티어 선택 창이 나타나는데 웹 서버 환경을 선택해준다.
application 환경정보를 등록하고 원하는 플랫폼을 선택한 후 애플리케이션 코드란에 0번에서 준비한 배포파일을 업로드 후 하단의 추가 옵션 구성을 선택한다. (추가 옵션 구성을 선택하지 않고 바로 환경생성 버튼을 누르면 모든 설정들이 default로 설정됨)
![upload](http://xoxoms.github.io/images/2/0.png)

#### 2.3 추가 옵션 구성
로드 밸런서와 EC2 인스턴스의 옵션을 설정한다.

##### 2.3.1. 소프트웨어
* S3에 elasticbeanstalk 로그를 저장하거나 CloudWatch에 로그스트림을 저장하는 설정을할 수 있다.

##### 2.3.2 인스턴스
* 인스턴스의 성능과 용량 등을 선택할 수 있다. 배포할 시스템의 요구사항에 부합하게 인스턴스를 선택한다. (t2.medium과 범용 SSD를 사용)

##### 2.3.3 용량
* 생성할 인스턴스의 수를 설정하고 모니터링 수준을 정할 수 있다. 마찬가지로 시스템의 요구사항에 맞게 인스턴스 수를 설정한다. 모니터링 수준은 CPU 사용률을 지표로 설정하였다.

##### 2.3.4 로드 밸런서
* loadbalancer에서 가용할 포트를 설정한다. Classic laodbalancer를 사용할 경우 필요한 설정이지만 나는 network loadbalancer를 사용하기 때문에 스킵.

##### 2.3.5  롤링 업데이트와 배포
* elasticbeanstalk이 소스 코드 병경 사항과 소프트웨어 구성 업데이트를 전파하는 방법을 선택한다.(배포 방식 설정) 롤링 방식과 한번에 1개의 인스턴스를 배포하도록 설정함.
* 구성 업데이트 항목은 VPC 구성이나 EC2 인스턴스가 변경되면 가동 중지 없이 환경의 인스턴스를 대체한다.

##### 2.3.6 보안
* pem 키 등록

##### 2.3.7 모니터링
* health 체크 경로를 설정한다.

##### 2.3.8 알림
* 장애시 알릴 이메일 주소 등록

##### 2.3.9 네트워크
* VPC와 인스턴스 서브넷, 권한그룹등을 설정한다.

#### 2.4 elasticbeanstalk 생성 후
환경이 생성되는데는 시간이 조금 걸리는데 이 작업이 정상적으로 완료되면 AWS EC2 서비스의 loadbalancer와 EC2 인스턴스가 정상적으로 생성되었는지 확인해보자. application 환경의 플랫폼을 Tomcat으로 설정했다면 구성메뉴의 소프트웨어 구성에서 JVM 명령줄 옵션과 JVM 힙 크기 등을 설정할 수 있다. 
![upload](http://xoxoms.github.io/images/2/1.png)

### 3. API Gateway

API Gateway를 사용하면 클라이언트마다 고유의 API Key를 할당할 수 있는데 사용 제한량을 조절하여 더 많은 요청처리를 하게 하거나 제한하는 것이 가능하고 클라이언트 별 사용량과 Cloud Watch를 이용한 모니터링이 가능하도록 해준다. 

또 API Gateway에 등록한 API외 요청에 대해서는 반려하도록 앞단에서 필터링 해주므로 유효하지 않은 요청이나 DDOS 공격에 대해 신경을 쓸 필요가 없게된다.

#### 3.1. API 작성

API Gateway를 사용하려면 서버에서 제공하는 API를 API Gateway에게 알려줘야한다. 이러한 작업은 API 작성 메뉴를 통해서 가능한데 상당히 번거롭지만 API 가져오기 기능이 있으므로 한번 작성해두면 카피하기 쉽다. 

API에서 제공하는 스펙을 모두 작성하고 아래 스텝으로 넘어간다.

#### 3.2. 사용자 지정 도메인 이름 

우리 서비스의 domain name을 등록할 수 있다. 도메인 이름을 등록하려면 ACM 인증서가 필요한데, Certification Manager에서 발급받을 수 있다. 

참고로 API Gateway는 us-east-1(버지니아 북부)에서 생성된 인증서만 사용가능하므로 인증서 발급시 region이 us-east-1인지 확인해야한다.

발급받은 인증서를 등록하고 3.1에서 작성한 API를 매핑해주면 대상 도메인 이름이 발급되는데 이 값을 Route 53에 등록하면 domain name으로 API 호출이 가능해진다.

![upload](http://xoxoms.github.io/images/2/2.png)
 