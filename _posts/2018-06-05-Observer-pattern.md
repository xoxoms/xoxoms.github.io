---
layout: post
title: Observer pattern
---
옵저버 패턴 간단 정리

-------------

한 객체의 상태가 바뀌면 그 객체에 의존하는 다른 객체들한테 연락이 가고 자동으로 내용이 갱신되는 방식으로 일대다 의존성을 갖는다.
"서로 상호작용을 하는 객체 사이에서는 가능하면 느슨하게 결합하는 디자인을 사용해야한다."

* 변경되는 데이터를 관리하는 subject, 데이터 변경을 모니터링 하는 observer가 존재한다
* 신문 구독 메커니즘을 통해 옵저버 패턴을 이해하자
    * 출판사는 subject, 구독자는 observer가 된다.
        * subject에서 일부 데이터를 관리한다.
        * subject의 데이터가 달라지면 observer에게 그 소식이 전해진다.
        * observer 객체들은 subject 객체를 구독하고 있으며, subject 객체의 데이터가 바뀌면 내용을 전달받는다.
    * observer 객체는 동적으로 추가될 수 있어야 한다.
    * observer 객체는 동적으로 제거될 수 있어야 한다.
* subject와 observer는 일대다 관계를 갖는다.
* subject의 상태가 바뀌면 observer에게 연락이 간다.
* observer는 subject에 의존한다.
* subject 인터페이스와 observer 인터페이스가 들어있는 클래스 디자인을 바탕으로 구현한다.
* loose coupling
    * 두 객체가 느슨하게 결합되어 있다는 것을 의미한다.
    * 두 객체가 서로 상호작용을 하지만 서로에 대해 모른다는 것을 의미한다.
    * 옵저버 패턴은 주제와 옵저버가 느슨하게 결합되어 있는 객체 디자인을 제공한다.
* 자바에 내장되어 있는 Observer, Observable을 통해 옵저버 패턴을 사용할 수 있다.
    * Observer는 class이므로, 상속을 받아야하는 단점이 있다.
                    
            
* 참고

    https://github.com/xoxoms/design-pattern/tree/master/src/observer