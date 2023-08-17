## This 
- 1.인스턴스 자신의 메모리를 가르킨다.
- 2.생성자에서 또 다른 생성자를 호출 할 떄 사용
- 3.자신의 주소(참조)값을 반환 함

  ### 자신의 주소(참조)값을 반환 함
  - 다음 인스턴스 변수 t의 주소값과 this 를 출력 값이 동일 한것을 볼 수 있다.
  ```java
    class Tv {
      public void printThis() {
        System.out.println(this);
      }
    }
  public class main {
    public static void main(String[] args) {
      Tv t = new Tv();
      System.out.println(t);
      t.printThis();
    }
  }
  ```
- 출력결과
  ```
    Tv@27d6c5e0
    Tv@27d6c5e0
  ```
  ### 생성자에서 또 다른 생성자를 호출 할 떄 사용

```java
class Tv {
  String name;
  int price;

  public Tv() {
    this("samsung", 1000);
  }
  public Tv(String name, int price) {
    this.name = name;
    this.price = price;
  } 
}
public class main {
    public static void main(String[] args) {
      Tv t = new Tv();
      System.out.println(t.name);
      System.out.println(t.price);
    }
  }
```
- 출력 결과
  ```
  samsung
  1000
  ```
  
