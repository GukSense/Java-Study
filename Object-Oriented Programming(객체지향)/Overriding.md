## Overriding(오버라이딩)
- 자식클래스에서 부모클래스의 메서드를 사용할때 구현내용을 변경하고싶을 경우 메서드를 재정의해서 사용하는것을 말한다.
### Overriding(오버라이딩) 구현조건
- 메서드의 이름, 매개변수 리스트, 반환타입이 동일해야한다.
- 메서드위에 애노테이션 주석을 달아주어야한다. ex)  @Override

### Overring vs Overloading
- 1. Overring
  - 부모클래스의 메서드를 재정의하기 위해 사용
  - 메서드의 이름, 매개변수 리스트, 반환타입이 같아야한다.
- 2. Overloading
  - 같은이름의 함수나 메서드를 여러개 정의하기 위해서 사용
  - 메서드의 이름은 같아야하지만, 매개변수 타입,개수, 반환타입은 달라도 된다.

### 사용 예시
부모 클래스
```java
  public class Parent {
    public int add(int a, int b) {
      int result = a + b;
      return result; 
    }    
  }
```
자식클래스
```java
  public class Child extends Parent {
    @Override
    public int add(int a, int b) {
      int result = a + (2*b);
      return result; 
    }
  }
```
테스트결과
```java
  public class OverridingTest {
    public static void main(String[] args) {
        Child c = new Child();
        System.out.println(c.add(3,5));        
    }
}
```
```
13
```

   
