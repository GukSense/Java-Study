## Singleton (싱글톤) 
- 프로그램에서 인스턴스가 단 한개만 생성되어야 하는 경우 사용하는 디자인 패턴
- static 변수, 메서드를 활용하여 구현 할 수 있다.
- 간단히 설명하면 싱글톤 패턴은 객체의 인스턴스를 한개만 생성되게 하는 패턴을 말한다
### 어떠한 경우에 사용하는가?
- 프로그램 내에서 하나의 객체만 존재해야 한다.
- 프로그램 내에서 여러 부분에서 해당 객체를 공유하여 사용해야한다.
### 싱글톤 패턴의 장점
1. 메모리 효율적 사용
싱글톤 패턴으로 한개의 인스턴스만을 고정 메모리 영역에 생성하고, 추후 해당 객체에 접근할 때  메모리 낭비를 방지할 수 있다.
2. 속도가 빠르다.
이미 생성된 인스턴스를 활용하여 효율적인 속도가 나온다.
3. 데이터 공유가 쉽다.
전역 인스턴스 이기때문에 다른 여러 클래스에서 데이터를 공유하며 사용 할 수 있다. 그러나 동시성 문제를 잘 유의하여 설계해줘야한다.
### 싱글톤 패턴 구현하기
```java
public class Singleton {
  private static final Singleton instance  = new Singleton();
  
  private Singleton(){}
  
  public static Singleton getInstance() {
    if(instance == null) {
      instance = new Singleton();
    }
    return instance;
  }
}
```
<br> 외부에서 객체를 메서드로 instance 를 반한해서 가져온다.
```java
public class Main() {
  public static void main(String[] args) {
    Singleton singleton1 = Singleton.getInstance();
    Singleton singleton2 = Singleton.getInstance();

    System.out.println(singleton1);
    System.out.println(singleton2);
  
    /*Result
      org.example.Singleton@7ef20235
      org.example.Singleton@7ef20235
    */        
  }
}
```
<br> 두 객체가 하나의 인스턴스 값을 사용하여 같은 주소 값을 출력하는 것을 볼 수있다.
### 싱글톤 사용시 주의사항
- "해당 객체의 인스턴스가 한 개만 존재하여야 하는지?"
- "사용을 하였을 때의 동시성 문제가 발생하지 않는지" 체크하여 사용해주자.
