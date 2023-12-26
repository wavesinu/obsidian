Java 7부터 `java.lang` 패키지에 `AutoCloseable` 인터페이스가 추가되었다.
[AutoCloseable (Java Platform SE 7 )](https://docs.oracle.com/javase/7/docs/api/java/lang/AutoCloseable.html)
# Method Summary

|Modifier and Type|Method|Description|
|---|---|---|
|void|close()|Closes this resource, relinquishing underlying resoureces.|
# Method Detail

```java
void close() throws Exception
```

- try-with-resources 문으로 관리되는 객체인 경우, close 메서드가 자동으로 호출된다.
- close 메서드 구현시 구체적인 exception을 throw하고, close 동작이 전혀 실패할 리가 없을 때는 exception을 던지지 않도록 구현하는 것이 권고됨.
- close 메서드에서 `InterruptedException`을 던지지 않는 것이 권고됨.
- 멱등성을 유지하는 것을 추천한다.
	`AutoCloseable.close()` 메서드는 멱등성을 유지하는 것이 필수적이지는 않다.
	즉, `AutoCloseable.close()` 메서드를 최초 한 번 호출 이후 다시 호출했을 때, side effect가 발생할 수 있다.

멱등성을 유지하는 것이 필수적인 사항은 아니지만, 유지할 수 있도록 메서드를 구현하는 것을 추천한다.
반면, `Closeable.close()` 메서드는 멱등성을 유지하는 것이 필수적이므로, 몇 번을 호출해도 부작용이 없다.
>연산을 여러 번 적용하더라도 결과가 달라지지 않는 성질을 멱등성([[idempotent]])이라고 한다.