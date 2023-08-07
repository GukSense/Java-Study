## 제어문 연습 문제

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

```
 구구단을 짝수단만 출력하도록 프로그램을 만들어보세요.(continue문 사용) 
```
```java 오류코드
public class Main {
    public static void main(String[] args) {
        int dan = 2;
        int num = 1;

        for (; dan <= 9; dan++) {
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
