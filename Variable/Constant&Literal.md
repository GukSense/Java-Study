## Constant (상수)

- 변하지않는 값. ex) 1년 12개월, 원주율 3.14 등등
- 프로젝트를 진행 시 프로그램에서 변하지 않고 고정된 값인 경우 상수를 선언하여 사용한다.
- 상수를 사용하면 변하지않는 값을 반복적으로 사용하여 사용 시 의미있는 문자 인식하기 쉽고, 값이 변하야 할 때 선언 부분만 변경하면 되므로  유지 보수가 쉽다.
- 반드시 대문자로 선언해야한다.
- 선언을 하면 사용 전 반드시 초기화를 해주어야하고, 한번 초기화 한 값은 변경 할 수 없다.
- 선언 방법은 변수의 데이터타입 앞에 'fianl' 을 붙여주기만 하면 된다.

### 사용 예시
```java
  public static vodi main(String[] args) {
    final int MAX_NUM = 100;
    final int MIN_NUM;
    MIN_NUM = 10;
    System.out.println(MAX_NUM); // 100
    System.out.println(MIN_NUM); // 10
    MIN_NUM = 50;   // 오류 
    System.out.println(MIN_NUM); // 오류 한번 선언한 상수는 변경 할 수 없다. 제일 처음 선언한 값에서 수정하여야한다.
  }
```


## Literal(값)
- 리터럴은 데이터(값) 그자체를 의미한다.
- 리터럴에도 타입이 있다. 앞서 정리했던 정수형 타입의 long, 실수형 타입의 float 의 리터럴에는 뒤에 접미사 L,f 를 꼭 붙여주어야한다.

### 리터럴 타입의 형변환
- 타입의 형변환이 가능하다. ex) int -> Long
- But 타입의 형변환 시 규칙이있다 <br>
  작은 데이터크기를 가진 타입에서 큰 데이터 타입 즉 <br>
  - 1바이트 -> 2바이트 or 4바이트 -> 8바이트 의 형변환은 자동 형변환이 가능해서 따로 지정해 줄 필요가없지만
  - 8바이트 -> 4바이트는 따로 형변환 표시를 해주어야한다.

- 내가 정리한 공식은 이와같다
  ```
    (데이터타입의 크기가)작은 것에서 큰 곳으로는 갈수 있지만 큰 곳에서 작은곳으로 갈때는 표현을 해주어야하고, 더 세밀한 수에서 덜 세밀한 수로 갈때도 표현을 해주어야한다.
  
  ```

  ```java
    public static void(String[] args) {
      
      int inum = 1000;
      byte bnum = inum;    // 오류  
      byte bnum2 = (byte)inum;  // O
    
      Long lnum;
      double dNum = 3.14;
      lnum = dNum  // 오류
      lnum = (long)dNum // O
    }
  ```
