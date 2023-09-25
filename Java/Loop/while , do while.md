## 반복문
### While 문
- 조건이 참인 경우 계속 돌아가는 반복문
- 주어진 조건이 참인 동안은 계속해서 반복해서 돌아간다.
- 조건이 맞지않을 경우 바로 반복수행을 멈추게 됨
- 조건식은 주로 반복횟수 or 값의 비교결에 따라 true ,fasle 판단 되는 경우로 지정
- Ex) <br>
while (조건식) { <br> 
반복수행 될 로직 // 조건식이 참일 경우 끝없이 반복한다.
}<br>

<b>  for 문은 보단 디테일한 설정을 할 수 없다. <br>
<br>
### while 사용예시

```
숫자 1~ 부터 10까지의 합을 반복문을 사용해서 구현해보세요.
```
```java
public static void main(String[args]) {
    int num = 1;
    int sum = 0;
    while(num <=10) {
        sum += num;
        num++;
    }
    System.out.println("1~10 까지의 총합은" + sum  " 입니다." );
}
```

- 정수 num 값을 1로 초기화 해주고 num이 10이하 일 때 까지는 참인 반복문 while 을 구현하였다.
- 반복
    - 첫번째 수행로직에서 sum에 num 값을 더해주면 sum -> 1 num++ 연사자로 로직 수행후 num -> 2
    - num == 2 이기때문에 아직 참 -> num 값이 11이 될때까지 반복

  ### do-while 사용예시
  - 조건과 상관없이 한번은 수행문을 수
  - while 문은 조건을 먼저 체크하고 반복 수행을 한다면 do-while 문은 조건과 상관없이 수행을 한번 하고나서 조건을 체크한다.
  ```
        문제
        do while문을 사용하여 대문자 Z가 입력될 때까지 입력된 문자를 출력하는 코드를 작성하세요.
        Z가 입력되면 프로그램을 종료한다는 문구를 출력 후 프로그램을 종료하세요.   
  ```
  ```java
  public static void main(String[] args) {
  
        Scanner scanner = new Scanner(System.in);
        char ch = ' ';

        do {
            System.out.print(
                    "문자를 입력해주세요:"
            );
            String str = scanner.nextLine();
            ch = str.charAt(0);

            if (ch > '0' && ch <= '9') {
                System.out.println("숫자" + ch + " 입니다.");
            } else if (ch >= 'a' && ch <= 'z') {
                System.out.println("소문자 "  + ch + " 입니다.");
            } else if (ch >= 'A' && ch < 'Z') {
                System.out.println("대문자 "  + ch + " 입니다.");
            }
        } while (ch != 'Z'); System.out.println("프로그램을 종료합니다.");
    }
  ```
  - 아스키코드표를 보면 'A'~'Z' 까지 65~90 'a'~'z' 는 97~122 다 따라서 if-else 조건식에서 ch >= 'a' && ch <= 'z' 으로 지정하면 그 사이값의 범위를 조건으로 지정 할 수 있다.
  - false 조건이 돼야 프로그램 종료를 선언 할 수 있기 때문에 ch != 'Z' 조건을 설정해주었다.
 
  <b> for 문은 좀 더 디테일한 값의 시작 지점, 반복범위 등을 지정 할 수 있고 while 은 값의 트루 폴스 여부를 조건식으로 할 때 더 효율적인 코드구성이 가능한것 같다.
