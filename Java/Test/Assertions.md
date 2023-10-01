## JUnit5
- Java 8 부터 사용가능
- 테스트 주도 개발 TDD 를 위해 사용
## Assertions
- 테스트가 원하는 결과를 제대로 리턴하는지 에러는 발생하지 않는지 확인할 때 사용하는 메소드
### Assertions _ 주요 메서드
assertEquals
 - 두 값을 비교하여 일치여부 판단
 - assertEquals(expected, actual)	두 값이 일치 할시 true 반환
```java
@Test
public void test() {
    float square = 2 * 2;
    float rectangle = 2 * 2;

    assertEquals(square, rectangle);
}
```
assertArrayEquals
- 예상 배열과 실제 배열이 동일한지 확인
- 두 Array가 동일하면 True 
```java
@Test
public void test() {
    char[] expected = { 'J', 'u', 'p', 'i', 't', 'e', 'r' };
    char[] actual = "Jupiter".toCharArray();

    assertArrayEquals(expected, actual, "Arrays should be equal");
}
```
fail
- 제공된 실패 메시지와 기본 원인으로 테스트에 실패
- 개발이 완료되지 않은 테스트를 표시하는 데 유용
```java
@Test
public void test() {
    // Test not completed
    fail("FAIL - test not completed");
}
```

