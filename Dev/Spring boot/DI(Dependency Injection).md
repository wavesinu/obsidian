### 의존관계 주입이란?
>의존성 관계 또는 주입(DI, Dependency Injection)이란, 클래스간 의존성을 외부에서 주입하는 것을 뜻한다.
>의존성 주입은 일반적으로 클래스에 대한 의존성의 <font color="#9c86e9">인터페이스화를 통한 코드 유연성 증대 + 클래스의 인스턴스를 외부에서 생성하여 주입</font>을 동시에 하는 방향으로 이루어진다.

### 의존관계란 무엇인가?
"A가 B를 의존한다."는 표현은 추상적이지만, 다음과 같이 정의할 수 있다.
>***의존대상 B가 변하면, 그것이 A에 영향을 미친다.***

즉, B의 기능이 추가 또는 변경되거나 형식이 바뀌면, 그 영향이 A에 미친다.
다음의 햄버거 가게 요리사 예시를 통해 알아보자.
- `햄버거 가게 요리사는 햄버거 레시피에 의존한다.` 햄버거 레시피가 변화하게 되었을 때, 변화된 레시피에 따라 요리사는 햄버거 만드는 방법을 수정해야 한다.
	- 레시피의 변화가 요리사의 행위에 영향을 미쳤기 때문에, "요리사는 레시피에 의존한다"고 할 수 있다.
```java
class BurgerChef {
    private HamBurgerRecipe hamBurgerRecipe;

    public BurgerChef() {
        hamBurgerRecipe = new HamBurgerRecipe();        
    }
}
```
### 의존관계를 인터페이스로 추상화하기
- 지금의 구현에서는 HamBurgerRecipe만을 의존할 수 있는 구조로 되어있다. 더 다양한 BurgerRecipe를 의존 받을 수 있게 구현하려면 `인터페이스로 추상화`해야 한다.
```java
class BurgerChef {
    private BurgerRecipe burgerRecipe;

    public BurgerChef() {
        burgerRecipe = new HamBurgerRecipe();
        //burgerRecipe = new CheeseBurgerRecipe();
        //burgerRecipe = new ChickenBurgerRecipe();
    }
}

interface BugerRecipe {
    newBurger();
    // 이외의 다양한 메소드
} 

class HamBurgerRecipe implements BurgerRecipe {
    public Burger newBurger() {
        return new HamBerger();
    }
    // ...
}
```
- 의존관계를 인터페이스로 추상화하게 되면, 더 다양한 의존관계를 맺을 수 있고, 실제 수현 클래스와의 관계가 느슨해지고([[Loose Coupling]]), 결합도가 낮아진다.
### 
---
```embed
title: "의존관계 주입(Dependency Injection) 쉽게 이해하기"
image: ""
description: "이번 글에서는 DI(의존성 주입, 의존관계 주입)의 개념을 설명한다."
url: "https://tecoble.techcourse.co.kr/post/2021-04-27-dependency-injection/"
```
