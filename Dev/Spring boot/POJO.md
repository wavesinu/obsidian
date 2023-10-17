
### POJO(Plain Old Java Object)란?
![[Pasted image 20231009161151.png]]
>POJO는 말 그대로 해석하면, <font color="#9c86e9">"오래된 방식의 간단한 자바 객체"</font>라는 말로서, Java EE 등의 중량 프레임워크들을 사용하게 되면서 해당 프레임워크에 종속된 무거운 객체를 만들게 된 것에 반발해서 사용하게 된 용어이다.
### POJO의 특징
- POJO는 특정 규약, 싱속, 또는 주석을 강제하지 않는 간단한 Java 객체를 의미한다.
- POJO는 특정 프레임워크나 기술에 종속되지 않아야 한다.
- 주로 데이터를 나타내거나 전송하는 데 사용되며, 비즈니스 로직을 포함할 수도 있다.
- POJO는 특정 기술이나 방법론에 제한받지 않기 때문에 유연하게 사용할 수 있다.
### POJO를 지향하는 이유
- Spring Framework 이전에는 원하는 엔터프라이즈 기술이 있다면 그 기술을 직접적으로 사용하는 객체를 설계했다. 그리고 이러한 개발 방식이 만연하고 있었다.
- 특정 기술과 환경에 종속되어 의존하게 된 자바 코드는 가독성이 떨어지고 유지보수에 어려움이 있다.
	- 이는 특정 기술의 클래스를 상속받거나, 직접 의존하게 되어 확장성이 매우 떨어지는 단점이 있다.
	- 즉, Java가 객체지향 설계([[OOP Principle]])의 장점들을 잃어버리게 되었다는 것이다.
POJO를 지향함으로써 얻을 수 있는 이점들은 다음과 같다.
1. **간결성**: 
   - 특정 규약, 인터페이스, 상속, 주석 등에 종속되지 않아 코드가 간결하고 이해하기 쉽다.
2. **유연성**:
   - 특정 프레임워크나 기술에 종속되지 않아 다양한 환경에서의 사용이 가능하다.
3. **재사용성**: 
   - 독립적인 특성으로 인해 다른 프로젝트나 모듈에서 쉽게 재사용할 수 있다.
4. **테스트 용이성**: 
   - 외부 의존성이 적어 단위 테스트하기가 더 쉽다.
5. **프레임워크와의 결합도 감소**: 
   - 특정 프레임워크나 라이브러리에 대한 의존성이 줄어든다.
6. **코드의 명확성**: 
   - 비즈니스 로직에 집중할 수 있게 되어 코드의 목적이 더 명확해진다.
### POJO 개념을 적용한 예시
```java
public class ExampleListener implements MessageListener {

  public void onMessage(Message message) {
    if (message instanceof TextMessage) {
      try {
        System.out.println(((TextMessage) message).getText());
      }
      catch (JMSException ex) {
        throw new RuntimeException(ex);
      }
    }
    else {
      throw new IllegalArgumentException("Message must be of type TextMessage");
    }
  }

}
```
- 위 코드는 JMS 라는 기능을 사용하기 위해 `MessageListener` 인터페이스를 상속받을 것을 알 수 있다. 
	- 이렇게 POJO 기반의 코드를 작성하지 않게 되면 이후 JMS와 기능을 비슷하지만 다른 솔루션을 사용하고자 할 때 교체하기가 굉장히 힘들어지게 된다.
```java
@Component
public class ExampleListener {

  @JmsListener(destination = "myDestination")
  public void processOrder(String message) {
    System.out.println(message);
  }
}
```
- 위 예제는 JmsListner를 상속받지 않고 어노테이션을 통해 객체를 주입받은 상황이다.
	- 이런식으로 코드를 작성하게 되면 해당 클래스와의 결합도가 낮아져 다른 솔루션으로 변경하고 할 경우 `@JmsListener`를 `@(다른 솔루션)`으로 코드를 수정만 하면 가능하므로 유지 보수에 있어 좀 더 유용하게 활용할 수 있다.
- <font color="#9c86e9">어떠한 인터페이스에도 종속되지 않는다.</font>
---
```embed
title: "Spring의 기본 특징-POJO"
image: "https://velog.velcdn.com/images/galaxy/post/ddad5ed8-9a0f-474f-9f93-43b90979624b/9941A1385B99240D2E.png"
description: "올해 1월달부터 스프링 프레임워크를 이용해 쇼핑몰 웹사이트를 구현해보는 프로젝트를 진행 중에 있다. 오늘은 스프링 프레임워크의 특징에 대해 간단히 정리해보고자 한다.아직까지 완벽하게 개념이 정리된 건 아니고 전반적인 흐름에 대해서만 이해하고 있는 상태라 프로젝트를 구현"
url: "https://velog.io/@galaxy/Spring%EC%9D%98-%EA%B8%B0%EB%B3%B8-%ED%8A%B9%EC%A7%95-POJO"
```
