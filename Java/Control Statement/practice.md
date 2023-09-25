## 제어문 연습 문제 1번

```
 다음 조건식을 조건문(if문)으로 바꾸어보세요.
  grade = (scoe >= 90) ? 'A':'B';
```
```java
  int score = 0;
  String grade = "";
  Scanner scanner = new Scanner(System.in);
  System.out.print("점수를 입력하세요:");
  score = scanner.nextInt();

  if(score >= 90) {
      grade = "A";
      System.out.println(grade);
  }  else {
      grade = "B";
      System.out.println(grade);
  }
```
## 제어문 연습 문제 2번
```
 구구단을 짝수단만 출력하도록 프로그램을 만들어보세요.(continue문 사용) 
```
- 처음 나의 오류코드
```java 
public class Main {
    public static void main(String[] args) {
        int dan = 2;
        int num = 1;

        for (; dan <= 9; dan++) {
            if (dan % 2 != 0) {
                continue;
            }
            for (; num <= 9; num++) {
                int result = dan * num;
                System.out.println(result);
            }
        }

        System.out.println(dan);
        System.out.println(num);
    }
}
```
<br>결과값<br>
```
2
4
6
8
10
12
14
16
18
```
두번째 for문에서 num의 값을 다시 1로 초기화 시켜주지않았기 때문에,
두번째 루프를 벗어난후에, 계속 num = 10 인 상태다 그래서 두번째 루프 조건값에 해당되지않기 때문에 result 값이 출력되지않는 실수를 범했다.
<br>
num 의 값을 1로 초기화 시켜주도록 수정해주면 문제가 해결된다.

```java
 public class Main {
    public static void main(String[] args) {
        int dan = 2;
        int num = 1;


        for (; dan <= 9; dan++) {
            if (dan % 2 != 0) {
                continue;
            }
            for (num = 1; num <= 9; num++) {  //num의값을 초기화시켜주었다.
                int result = dan * num;
                System.out.println(result);
            }
            System.out.println();
        }
    }
}
```
<br>결과값<br>
```
2
4
6
8
10
12
14
16
18
~
8
16
24
32
40
48
56
64
72
```
