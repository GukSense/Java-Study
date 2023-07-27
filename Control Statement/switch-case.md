## Switch-Case (스위치케이스)
- if, if-else 문 보다 가독성이 좋다.
- 조건이 특정 숫자이거나 문자열일때 사용
- EX) <br>
      switch(조건식) { <br>
      <br>
      case 값: 수행될 로직  <br>
              break; //참일경우 switch-case 문 탈출  <br>
      case 값: 수행될 로직  <br>
              break; //참일경우 switch-case 문 탈출  <br>
      case 값: 수행될 로직  <br>
              break; //참일경우 switch-case 문 탈출  <br>
      <br>
      }  <br>
      <br>

스위치케이스문은 조건이 범위가아닌 하나의 값으로 특정 할 수 있을때 사용하면 if문보다 더 가독성 있게 사용 할 수 있다.
### Switch-Case 사용예시

```
month에따라 계절명을 알려주는 코드를 switch-case 를 사용해 작성해보세요.
```
```java
public static void main(String[]args {
      Scanner scanner = new Scanner(System.in);
      int month = scanner.nextInt();
      String session = "";

      System.out.print("계절을 입력해주세요:");

      switch(month) {

            case 3: case 4: case 5: 
                  session = "봄";  
                  break;
            case 6: case 7: case 8: case 9:
                  session = "여름";
                  break;
            case 10: case 11:  
                  session = "가을";
                  break;

            case 12: case 1: case 2:
                  session = "겨울";
                  break;
      }
      System.out.println("현재 계절은 " + session + " 입니다.");
}
```

### Switch-expression 와 사용예시
- java 12부터 새롭게 추가 된 switch문
- 조건을 , 로만 구분해주면 돼서 코드가 효율적이다.
- 값이 리턴되지 않기 때문에 break 를 사용하지않는다.
- yield 예약어를 사용

```java
public static void main(String[]args {
      Scanner scanner = new Scanner(System.in);
        System.out.print("계절을 입력해주세요:");
        int month = scanner.nextInt();

        String session = switch (month) {

            case 3, 4, 5 -> {
                yield "봄";
            }
            case 6, 7, 8, 9 -> {
                yield "여름";
            }
            case 10, 11 -> {
                yield "가을";
            }
            case 12, 1, 2 -> {
                yield "겨울";
            }
            default -> {
                yield "오류";
            }
        };
        System.out.println("현재 계절은 " + session + " 입니다.");
    }
```
default 를 지정해주지 않을 경우 java: the switch expression does not cover all possible input values 오류가 뜬다. 
또는 String session 값으로 리턴값을 받는다고 하였기 때문에 yield 로 반드시 리턴을 해주어야 한다. 그러지 않을 경우 이때도 java: the switch expression does not cover all possible input values 가 뜬다. 
