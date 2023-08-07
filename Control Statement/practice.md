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
