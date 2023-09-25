## 다형성(polymorphism)
- 하나의 객체가 여러가지 타입을 가질 수 있는것을 말한다.
- Java 에서는 부모클래스 타입의 참조변수로 자식클래스 타입의 인스턴스를 참조할수 있도록 구현하였다.

### 예시
- 상위클래스 개념인 Animal.class 가 있고 하위 클래스 개념인 Person,Tiger,Eagle class 가 있다고 했을때, Animal 클래스의 move() 메서드는 특징에맞게 각 하위클래스에서 다르게 구현 할 것이다.
<br>
Animal.class
```java
public class Animal {
  public void move() {
    System.out.println("동물이 움직인다.");
  }
}
```

Person.class
```java
public class Person {
  public void move() {
    System.out.println("사람은 두발로 걷는다.");
  }
}
```

Tiger.class
```java
public class Tiger {
  public void move() {
    System.out.println("사자는 네발로 걷는다.");
  }
}
```

Eagle.class
```java
public class Eagle {
  public void move() {
    System.out.println("독수리는 날개로 날아다닌다.");
  }
}
```
다형성 구현 테스트
```java
public class PolymorphismTest {
    public static void main(String[] args) {
      Animal aPerson = new Person();
      Animal bTiger = new Tiger();
      Animal cEagle = new Eagle();

      ArrayList<Animal> animalList = new ArrayList<>();
      animalList.add(aPerson);
      animalList.add(bTiger);
      animalList.add(cEagle);

      for(Animal a : animalList) {
        a.move();
      }  
    }
}
```
다형성 구현 테스트 결과
```
사람은 두발로 걷는다.
사자는 네발로 걷는다.
독수리는 날개로 날아다닌다.
```

- 1. 참조변수 타입은 3개의 변수모두 Animal 타입이지만 move() 메서드 결과값이 다른 것을 알수있다.
  2. 그 이유는 인스턴스 참조를 Person, Tiger, Eagle 로 다르게 선언해주었기 때문.

