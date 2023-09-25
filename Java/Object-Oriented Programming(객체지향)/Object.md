## 객체(Object)
- 사전적의미: 의사나 행위가 미치는 대상
- 구체적,추상적 데이터의 단위 (회원,주문,배송,생산)

  ## 객체지향 프로그래밍과 절차지향 프로그래밍
  - 절차지향 프로그래밍 -> 시간이나 사건의흐름에따라 진행되는 프로그래밍
    - 물건을 고른다->장바구니에 넣는다 -> 주문을한다 -> 금액을 지불한다 -> 배송이 시작된다 -> 집으로 배송된다.
  - 객체지향 프로그래밍 -> 객체를 중심으로 객체가 가지고있을 기능,데이터 등을 중점적으로 협력하는 방식으로 프로그래밍한다.

  - Ex) <br>
  ![image](https://github.com/GukSense/Java-Study/assets/101082667/dfb93d70-13c6-45a8-8eee-6352ed6f9c3d)
  <br>

  
## 객체지향 프로그래밍 실제구현
- 온라인쇼핑몰에서 회원 로그인을 하고 여러 판매자가 판매하고있는 제품 중 하나를 골라 주문을한다.
- 성적확인을 위해 학사관리 시스템에 로그인하여 수강한 과목들의 성적을 확인했다.
- 아침에 회사 가는길에 별다방 커피숍에 들려 아이스 카페라떼를 주문했다.

<br><b>온라인쇼핑몰에서 회원 로그인을 하고 여러 판매자가 판매하고있는 제품 중 하나를 골라 주문을한다.<br>

  ```java
  public class Member {
    private int id;
    private String name;
    private DateOfSubscription;
    private String password;
    private String address;
  }
  ```
  ```java
  public class Order {
    private int orderId;
    private int sellerId;
    private orderCode;
    private orderDate;
  }
  ```
<br><b>성적확인을 위해 학사관리 시스템에 로그인하여 수강한 과목들의 성적을 확인했다.<br>
```java
public class Student {
  private int studentId;
  private String name;
  private String password;
  private int majorCode;
  private int grade;
}
```
```java
  public class Major {
    private String name;
    private String category;
    private int date;
  }
```

- 객체를 정의한다
- 객체의 속성을 멤버변수로, 역할을 메서드로 구현
- 각 객체간의 협력을 구현한다.
