# DDD란?
DDD(Domain Driven Design) 또는 도메인 주도 설계라고 부른다. 도메인 패턴을 중심에 놓고 설계하는 방식이다.
#### 특징
- 도메인 그 자체와 도메인 로직에 초점을 맞춘다. 일반적으로 많이 사용하는 데이터 주도 설계 접근법을 탈피해서 순수한 도메인의 모델과 로직에 집중하는 것을 말한다.
- 보편적인 언어의 사용(Ubiquitous)이다. 도메인 전문가와 소프트웨어 개발자 간의 커뮤니케이션 문제를 없애고 상호 이해할 수 있고, 모든 문서와 코드에 이르기까지 동일한 표현과 단어로 구성된 단일화된 언어체계를 구축해나가는 과정을 말한다.
- 분석 작업과 설계, 그리고 구현에 이르기까지 통일된 방식으로 커뮤니케이션이 가능해진다.
- 소프트웨어 엔티티와 도메인 컨셉을 가능한 가장 가까이 일치시키는 것이다. 분석 모델과 설계가 다르고 그것과 코드가 다른 구조가 아니라 도메인 모델부터 코드까지 항상 함께 움직이는 구조의 모델을 지향하는 것이 DDD의 핵심원리이다.
# 객체지향에서부터
도메인 주도 설계를 이해하기 위해서는 우선 객체지향을 이해할 필요가 있다.
>객체지향에서의 핵심은 실세계의 객체들이 서로 간의 상호작용을 바탕으로 책임, 협력, 역할의 관점을 가지고 메시지를 교환하는 것이다.

객체지향의 핵심은 결국 객체(무언가를 만드는 주체)라고 할 수 있다.
그렇다면 객체를 어떻게 추려내고, 어떤 객체가 필요한지 알 수 있고, 이 객체들이 어떻게 서로 상호작용 할 수 있을까?
여러 방법들이 존재하겠지만, 도메인 주도 설계를 통해 이 문제를 해결할 수 있다.
# 도메인이란?
도메인은 실세계에서 사건이 발생하는 집합이라고 생각하면 쉽다.
예를 들어, 옷 쇼핑몰의 경우 **손님들이 주문하는 도메인**(Order Domain)이 있을 수 있고, 점주 입장에서는 **옷을 관리하는 도메인**(Manage Domain)이 있을 수 있고, 쇼핑몰 입장에서는 월세, 관리비 등 **건물에 대한 관리를 담당하는 도메인**(Building Domain)이 있을 수 있다.
>이러한 도메인들이 서로 상호작용 할 수 있게 하는 설계가 바로 도메인 주도 설계다.


# 데이터 주도 설계란?

데이터 주도 설계란 객체가 가져야 할 데이터에 초점을 두고 설계를 하는 방식을 일컫는다.
데이터 주도 설계에서는 객체 자신이 포함하고 이쓴 데이터를 조작하는 데 필요한 행동을 정의한다.

```java
public class Movie {

    private String title;
    private Duration runningTime;
    private Money fee;
    private List<DiscountCondition> discountConditions;

    private MovieType movieType;
    private Money discountAmount;
    private double discountPercent;

    // getter, setter..
}
```
설계 시 협력을 고민하지 않았기에 과도한 접근자와 수정자가 탄생하게 된다. 이는 후에 객체가 어떤 곳에 사용될 지 알 수 없기 때문에 최대한 많은 접근자와 수정자를 만드는 결과를 낳게 된다.

결과적으로 데이터 중심 설게는 외부에 대부분의 구현이 노출되기 때문에 캡슐화 원칙을 위반하게 된다.

내부 구현이 퍼블릭 인터페이스에 노출되며, 다른 객체들과 강하게 결합하게 된다. 이로 인해 객체의 내부 구현이 변경될 때 이 인터페이스에 의존하는 모든 객체들이 함께 변경되므로, 높은 결합도를 유지하게 된다.
# 왜 도메인 주도 설계를 사용해야 하는가?
- 도메인 모델의 적용 범위를 구현까지 확장하여 도메인 지식을 코드에 반영
- 공통의 언어를 사용하여 도메인과 구현을 충분히 만족하는 모델을 만든다.
- 실제 코드로 구현 가능한 현실성 있는 도메인 모델 분석과 그것을 추상화하는 설계가 가능해진다.

# [[MSA]]에서 유독 도메인 주도 설계를 많이 찾는 이유는?
- 분산된 모놀리스 시스템
- 무조건 트렌디한 기술을 적용하는 것은 독이 될 수 있다.
- 소프트웨어의 목적에 대해 생각해볼 필요가 있다.