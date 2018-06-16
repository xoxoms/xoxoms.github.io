---
layout: post
title: Decorator pattern
---
데코레이터 패턴 간단 정리

-------------

객체에 추가 요소, 행동를 동적으로 더한다. 서브클래스를 만드는 경우에 비해 훨씬 유연하게 기능 확장이 가능하다. 기존 코드를 수정하지 않고도 행동을 확장할 수 있다는 장점이 있다. (OCP를 철저히 지킨다.)
* 들어가기 전에..
    * OCP (Open-Closed Principle)
        * 클래스는 확장에 대해서 열려있어야 하지만 코드 변경에 대해서는 닫혀 있어야 한다.
        * 디자인, 설계할 때 현실적으로 모든 부분에 대해서 OCP를 적용할 수 없다.
            * 가장 바뀔 확률이 높은 부분을 중점적으로 살펴보고 OCP를 적용해야한다.
                * 바뀔 확률이 높은 부분을 찾는데는 도메인의 비즈니스 이해도, 객체지향 시스템 디자인 경험이 크게 작용된다.
* 데코레이터 패턴은 특정 객체를 감싸서 그 객체의 기능, 행위를 확장하는데 사용한다.
    * 데코레이터 자신이 감싸고 있는 구성요소의 메소드를 호출한 결과에 새로운 기능을 더함으로써 행동을 확장한다.
* 구성 요소를 감싸는 데코레이터의 개수에는 제한이 없다.
    * 그러므로 데코레이터 패턴을 쓰면 관리해야할 객체가 늘어난다.
        * 하지만 빌더 패턴과 팩토리 패턴을 사용하면 좀 더 캡슐화되어 있는 코딩을 할 수 있다.
* 데코레이터 패턴은 감싸고 있는 객체에 따라서 분기해야하는 경우에는 맞지 않는다.
    * 단순히 행위를 확장하는데 사용한다.
    * 감싸고 있는 객체가 무엇인지는 고려하지 않는다.
* 인터페이스와 추상 클래스 모두 데코레이터 패턴을 사용할 수 있다.
    * 추상 클래스를 이용한 데코레이터 패턴의 요소
        * A. 최상위 추상 클래스 (실제 꾸며질 객체의 추상 클래스)
        * B. 구현 클래스 (A를 상속. 실제 꾸며질 객체)
        * C. 데코레이터 추상 클래스 (A를 상속. B를 꾸며줄 데코레이터들의 추상클래스)
        * D. 데코레이터 구현 클래스 (C를 상속. B를 구성 요소로 갖고, B를 꾸며준다.)
* java.io 패키지 내의 FileInputStream을 포함한 많은 클래스들이 데코레이터 패턴으로 구현되어있다.
    * BufferedInputStream, BufferedOutputStream 등
* What is difference between Decorator Pattern and Proxy Pattern?
    * Relationship between a Proxy and the real subject is typically set at compile time, Proxy instantiates it in some way, whereas Decorator is assigned to the subject at runtime, knowing only subject's interface.
        * 출처: https://stackoverflow.com/questions/18618779/differences-between-proxy-and-decorator-pattern
    * When using Proxy Pattern, we usually create an instance of abject inside the proxy class. And when using Decorator Pattern, we typically pass the original object as a parameter to the constructor of the decorator.
        * 출처: https://powerdream5.wordpress.com/2007/11/17/the-differences-between-decorator-pattern-and-proxy-pattern/
            
* 참고

    Head First Design Patterns
    
    https://github.com/xoxoms/design-pattern/tree/master/src/decorator