```java
int[] arr = new int[5];
Arrays.setAll(arr, (i)-> (int)(Math.random() * 5) + 1);
```
위 코드에서 `(i)-> (int)(Math.random() * 5) + 1`가 바로 람다식이다. 이 람다식이 하는 일을 메서드로 표현하면 다음과 같다.

```java
int method(){
	return (int)(Math.random() * 5) + 1;
}
```
- 람다식은 메서드의 매개변수로 전달되어지는 것이 가능하다.
- 메서드의 결과로도 반환될 수 있다.
**람다식으로 인해 메서드를 변수처럼 다루는 것이 가능해진다.**

# 람다식 작성하기
- '람다식 = 익명 함수' 이므로 메서드에서 이름과 반환타입을 제거하고 매개변수 선언부와 몸통 `{}` 사이에 `->` 를 추가한다.
```java
int max(int a, int b){
	return a > b ? a : b;
}
```

```java
(int a, int b) -> {
	return a > b ? a : b
}
```
- 반환값이 있는 메서드의 경우, return 문 대신 `expression`으로 대체할 수 있다. 식의 연산 결과가 자동적으로 반환값이 된다.
	- 이때는 문장(statement)이 아닌 식(expression)이므로 끝에 `;`를 붙이지 않는다.
```java
(int a, int b) -> a > b ? a : b
```
- 람다식에 선언된 매개변수의 타입은 **추론이 가능한 경우** 생략할 수 있는데, 대부분은 생략이 가능하다.
	- 람다식에 반환 타입이 없는 이유도 항상 추론이 가능하기 떄문이다.
```java
(a, b) -> a > b ? a : b    // 반환 타입(int) 생략
```
- 선언된 매개변수가 하나뿐인 경우, 괄호 `()`를 생략할 수 있다.
	- 단, 매개변수의 타입이 있는 경우에는 괄호 `()`를 생략할 수 없다.
```java
(a) -> a * a
=
a -> a * a    // OK

(int a) -> a * a
int a -> a * a    // Error
```
- 마찬가지로 괄호`{}`안의 문장이 하나일 때에도 괄호`{}`를 생략할 수 있다. 이 때 문장의 끝에는 `;`를 붙이지 않아야 한다.
```java
(String name, int i) -> {
	System.out.println(name + "=" + i);
}
```

```java
(String name, int i) -> System.out.println(name + "=" + i)
```
- 그러나 괄호`{}`안의 문장이 return문일 경우에는 생략할 수 없다.
