## 상속 (Inheritance)
### 상속이란?
- 기존의 클래스를 재사용하여 새로운 클래스를 작성하는 방법
### 상속의 장점
- 적은양의 코드로 새로운 클래스를 작성 할 수 있다.
- 코드를 공통적으로 관리 할  수 있다.
  - ----> 재사용성을 높여 효율적이며 중복을 제거하기 때문에 코드의 생산성과 유지보수에 좋다.
### 상속을 하는 방법
```java
class B extends A {
}
```
### 상속을 할 때 고려해야 하는 것들
- 상속은 하나만 받을 수 있다. 다중상속은 불가능하다
  - ex) class B extends A,B,C <-- X
- 상속은 "IS-A" 관계를 성립되어야한다. 하위 클래스는 상위 클래스의 한 유형이거나 하위 유형이어야한다.
  - ex) 사람은 포유류. <--- 부모: 포유류 자식: 사람
  <br> ![image](https://github.com/GukSense/Java-Study/assets/101082667/a352e356-c8b8-47c0-ab6d-f40f9ac000b2)

- 부모클래스의 멤버를 자식클래스에서 접근 할 수 있는지 고려해야함
  - private 멤버는 상속이 되지않고 protected, public 멤버만 상속이 가능하다.
- final로 선언된 클래스는 상속될 수 없다.
- 계층구조관리
  - 클래스의 상속은 계층구조를 형성하기 때문에 클래스간의 관계를 명확히 관리해야한다. 잘못 사용시 클래스의 복잡성이 증가 할 수 있다.
## 상속에서 클래스 생성과정
### 하위클래스가 생성되는 과정
- 하위클래스를 생성하면 상위클래스가 먼저 생성 됨
- 따라서 클래스가 상속받은 경우 하위클래스에서 반드시 상위 클래스의 생성자를 호출해야한다.
### 하위클래스 호출 시 상위클래스가 먼저 생성되는 예시
<br> Parent.java
```java
public class Parent {
    public Parent(){
        System.out.println(
                "Call Parent()"
        );
    }
}
```
<br> Child.java
```java
public class Child extends Parent {
    public Child(){        
        System.out.println("Call Child()");
    }
}
```
<br> Main.java
```java
public class ExtendsTest {
    public static void main(String[] args) {
        Child c = new Child();
    }
}
```

<br> 상위클래스 생성시 Call Parent() , 하위 클래스 생성시 Call Child() 가 출력 되도록 셋팅 후 main 클래스에서 하위클래스인 Child 를 호출 해 보면 결과는 다음과 같다.
<br> Result
```java
Call Parent()
Call Child()
```
- 나는 분명 Child 클래스를 생성했는데 상위 클래스인 Parent 생성자가 먼저 호출되고 그 뒤 하위클래스 인 Child 생성자가 호출 된 것을 확인 할 수있다.

### 하위클래스는 밥드시 상위클래스의 생성자를 호출해야한다. 의 예시
```java
public class Parent {
  private String parentString;

  public Parent(String parentString){
      this.parentString = parentString;
      System.out.println("Call Parent()");
  }
}
```
<br> Child.java
```java
public class Child extends Parent {
    public Child(){        
        System.out.println("Call Child()");
    }
}
```
<br> Main.java
```java
public class ExtendsTest {
    public static void main(String[] args) {
        Child c = new Child();
    }
}
```
- Child 클래스에서 다음과같은 오류가 뜬다 There is no default constructor available in 'example2.Parent' 
- 앞의 예시에서는 상위클래스 Parent에서 default 생성자가 있기때문에 따로 생성자 호출을 super() 로 부모클래스의 생성자를 호출하지않아도 컴파일 과정에서 자동으로 추가해줬기 때문이다.
- 다음과 같은 오류에서 해결방법은 2가지가 있다.
  - 1. 상위 클래스 Parent에 default 생성자를 만들어준다.
  - 2. 하위 클래스 Child에 super() 를 통해 상위클래스 생성자를 명시적으로 지정해준다.<br>
<b>super() 로 해결하는 방법
<br> Child.java
```java
public class Child extends Parent {
    public Child(){
        super("상위클래스 스트링");        
        System.out.println("Call Child()");
    }
}
```
