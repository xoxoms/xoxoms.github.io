---
layout: post
title: Strategy pattern
---
전략 패턴 간단 정리

-------------

알고리즘 군을 클래스로 정의하고, 각각을 캡슐화하여 교환해서 사용할 수 있도록 만드는 패턴.
스트래티지 패턴을 사용하면 알고리즘을 사용하는 클라이언트는 독립적으로 알고리즘을 변경할 수 있다.

* 어플리케이션에서 달라지는 부분을 찾아내고, 달라지지 않는 부분으로 부터 분리한다.
    * 달라지는 부분을 찾아서 나머지 코드에 영향을 주지 않도록 "캡슐화"한다.
        * 코드를 변경하는 과정에서 의도하지 않은 일이 일어나는 것을 줄이고, 시스템의 유연성을 향상 시킨다.
* 인터페이스에 맞춰서 프로그래밍 해야한다.
    * 상위 형식(인터페이스나 추상 클래스)에 맞춰서 프로그래밍 한다는 뜻
    * 실제 실행시에 쓰이는 객체가 코드에 의해서 고정되지 않도록 해야한다.
        * setter를 이용하여 참조를 동적으로 바꿀 수 있게 함으로써 특정 인터페이스를 구현한 구현체들을 자유자재로 사용할 수 있다.
    * 비권장 유형
        * Dog dogDoll = new Dog();
dogDoll.bark(); // 유연성이 전혀없다. 만약 인스턴스가 강아지 인형이라면 짖을 수 없는데, 무조건 짖어야한다.
    * 권장 유형
        * Animal animal = new Dog(); // 강아지 인스턴스 생성
animal.makeSound(); // makeSound() 내부에서 적절하게 인터페이스를 사용하도록 구현하면 강아지, 고양이 등 모든 동물의 울음소리를 낼 수 있도록 할 수 있다.
animal.setSound(new MeowSound()); // 고양이 울음 소리로 변경
animal.makeSound();
* 런타임에도 동적으로 함수의 행위를 변경할 수 있도록 유연하게 코딩해야한다.
    * 클래스에는 인터페이스를 참조하는 필드를 두고, setter나 생성자에서 인터페이스 구현체를 참조하도록 정의한다.
* "A는 B이다"보다 "A에는 B"가 있다가 나을 수 있다.
    * 상속 보다 구성을 활용하는 것이 좋다.
        * 구성은 두 클래스를 합치는 것을 의미한다.
            * Duck 클래스에 FlyBehavior, QuackBehavior 클래스를 참조하도록 구성하는 것
            * 알고리즘을 별도의 클래스의 집합으로 캡슐화할 수있다.
            * 실행시에도 구성요소로 사용하는 객체를 동적으로 변경가능하다.
            
* 참고

    Head First Design Patterns
    
    https://github.com/xoxoms/design-pattern/tree/master/src/strategy