## instance(인스턴스)
- 인스턴스화 -> 클래스로부터 객체를 만드는 과정
- 클래스는 하나 이지만 클래스로 부터 파생되는 인스턴스는 여러개로 각각 메모리를 따로 가진다. 따라서 인스턴스 별 각각 다른 멤버변수를 가진다.
- new 키워드를 통해 생성 할 수 있다.
- 알아서 메모리를 생성하여 끌어쓰고 다시 삭제되는 스택형 메모리인 함수와 달리 동적으로 생성해줘야한다 (new 키워드를 통해 생성)

### 객체 생성방법
```
  객체 생성 방법
  클래스명 변수명;
  변수명 = new 클래스명();
```
```java
class InstanceTest {
  public static void main(String[] args){
    Tv t = new Tv();
    t.channel = 10;    // Tv 클래스의 t 인스턴스 메모리의 channel 변수에 10이 할당되었다.
    System.out.println("현재 채널은  " + t.channel + "입니다.");
  }
}
class Tv {
  int channel;
}
```
## Constructor
- 클래스의 인스턴스 객체를 생성할 떄 클래스명 변수명 = new <U>클래스명()</U> 으로 생성하는데 이때 <U>클래스명()</U> 부분이 생성자이다.
- EX) Tv t = <U>new Tv()</U>
- 함수처럼 기능을 호출 하는것이 아닌 위에 말했듯이 객체를 생성하거나 클래스 변수를 초기화하기 위해 호출한다.
- 생성자는 반환 값 이 없다.
- 클래스의 이름과 동일하다.
- 클래스에느 반드시 하나 이상의 생성자가 존재하고 클래스에 생성자가 하나도 없는 경우 컴파일러가 생성자 코드를 넣어준다. 
  - EX)
     ```java
     class Tv {
        int channel;
     }
     public static void main(String[] args) {
      Tv t = new Tv()    // class Tv 에는 생성자 메서드가 없지만 public Tv(){} 를 컴파일러가 자동으로 생성해주기때문
     tv.channel = 6;
     }
     ```
- 클래스에 임의로 생성자를 만들었다면 그에 맞게 생성자를 호출 해 주어야한다.
  - EX)
    ```java
     class Tv {
      int channel;
      public Tv(int channel){
        this.channel = channel;
      }
    }
    class ConstructorTest {
      public static void main(String[] args ){
        int channel = 0;
        Tv t1  = new Tv() // X
        Tv t2 = new Tv(channel); // O
      }
    }
    ```
- 만약 생성자를 통해 셋업을 하고싶지않고 인스턴스 생성만 하고싶은데 저런식으로 클래스에 생성자가 구현 되어있다면 디폴트 생성자를 생성해주면 된다.
  - EX)
    ```java
     class Tv {
      int channel;
      public Tv(int channel){
        this.channel = channel;
      }
      public Tv() {

      }
    }
    class ConstructorTest {
      public static void main(String[] args ){
        int channel = 0;
        Tv t1  = new Tv() // O
        Tv t2 = new Tv(channel); // O
        // 두개의 코드가 모두 맞는것이 된다.
      }
    }
    ```
    - 이를 여러가지 생성자를 정의하는 생성자 오버로딩이라고 한다.
