## Array(배열)
### 배열이란?
- 동일한 자료형의 순차적 자료 구조
- 인덱스 연산자[] 를 통해서 빠른 참조가 가능
- 배열의 순서는 0부터 시작
- 자바에서는 객체배열을 구현한 ArrayList를 많이 활용 함
### 배열 선언과 초기화
<br>배열선언하기
```
int[] arr = new int[10];
int arr2[] = new int[10];
```
![image](https://github.com/GukSense/Java-Study/assets/101082667/3906a942-4237-4b4c-8f19-a141029ac191)

<br>배열 초기화
```
int[] arr = new int[] {1,2,3,4,5,6,7,8,9,10};  // 개수 생략해야함
int[] arr = {1,2,3,4,5,6,7,8,9,10};  // new int[] 생략가능
int[] arr;
arr = new int[] {1,2,3,4,5,6,7,8,9,10};  // 선언 후 배열을 사용하는 경우는 new int[] 를 생략할 수 없다.
```
### 배열 사용하기
- [] 인덱스 연산자의 활용 -> 배열 요소가 저장된 메모리의 위치를 연산하여 찾아 줌
- 배열을 이용하여 합을 구하기
```java
int[] arr = new int[10];
int total = 0;

for(int i=0, num=1; i<arr.length; i++, num++) {
  arr[i] = num;
}
for(int i=0; i<arr.length; i++) {
  total += arr[i];
}
System.out.println(total);
//output 55;
```

## 객체배열 사용하기
### 객체 배열 선언과 구현
- 기본 자료형 배열은 선언과 동시에 배열의 크기만큼의 메모리가 할당되지만, 객체배열의 경우엔 객체의 주소가 들어갈(4바이트,8바이트) 메모리만 할당되고(null) 각 요소 객체는 생성하여 저장해야함
- ![image](https://github.com/GukSense/Java-Study/assets/101082667/dd18c7ef-f971-4d9d-8e07-abb4f69f558c)

```java
public class Main {
    public static void main(String[] args) {
        Book[] bookArr = new Book[5];
        for (book:bookArr) {
            System.out.println(book);
        }
    }
}
/* Result
  null
  null
  null
  null
  null
*/
```
<br> 주소값이 참조된게 없기 때문에 null이 나온다. 그렇다면 값을 참조해주면 어떻게 될까?

```java

public class Main {
    public static void main(String[] args) {
        Book[] bookArr = new Book[5];
        bookArr[0] = new Book("1번","무라카미하루키");
        bookArr[1] = new Book("2번","무라카미하루키2");
        bookArr[2] = new Book("3번","무라카미하루키3");
        bookArr[3] = new Book("4번","무라카미하루키4");

        for (Book book:bookArr) {
            book.showInfo();
        }
    }
}
/* Result
제목: 1번
저자: 무라카미하루키

제목: 2번
저자: 무라카미하루키2

제목: 3번
저자: 무라카미하루키3

제목: 4번
저자: 무라카미하루키4

Exception in thread "main" java.lang.NullPointerException: Cannot invoke "org.example.Book.showInfo()" because "book" is null
	at org.example.Main.main(Main.java:12)
*/
```
<br>5번째 배열은 값을 참조 하지않았기에 null Exception 이 나온다.
<br> null 있는 부분을 제외하고 ,  갑이 참조된 만큼만 출력하고싶다면?
```java
public class Main {
    public static void main(String[] args) {
        Book[] bookArr = new Book[5];
        int count = 0;
        bookArr[0] = new Book("1번","무라카미하루키"); count++;
        bookArr[1] = new Book("2번","무라카미하루키2");count++;
        bookArr[2] = new Book("3번","무라카미하루키3");count++;
        bookArr[3] = new Book("4번","무라카미하루키4");count++;

        for (int i=0; i<count; i++) {
            bookArr[i].showInfo();
        }
    }
}
/* Result
제목: 1번
저자: 무라카미하루키

제목: 2번
저자: 무라카미하루키2

제목: 3번
저자: 무라카미하루키3

제목: 4번
저자: 무라카미하루키4 
*/
```
<br> 좀 더 깔끔한 코드로 적을려면 Book 클래스내에서 멤버변수로 count을 static 변수로 선언하고 생성자가 초기화 될 때마다 count++ 로 구현 후 
for(){} 에서 i<Book.count; 로 셋업해주는게 더 깔끔한 코드로 구현 되었을것이다.

### 객체배열 복사하기
- System.arrayCopy(src, srcPos, dest, destPos,length) 자바에서 제공하는 배열 복사 메서드이다.
- 얕은 복사
  - 객체 주소만 복사되어 한 쪽 배열의 요소를 수정하면 같이 수정된다.
  - 즉, 두 배열이 같은 객체를 가리킴
```java
public class Main {
    public static void main(String[] args) {
        Book[] bookArr = new Book[4];
        Book[] bookCopy = new Book[4];
        bookArr[0] = new Book("1번","무라카미하루키");
        bookArr[1] = new Book("2번","무라카미하루키2");
        bookArr[2] = new Book("3번","무라카미하루키3");
        bookArr[3] = new Book("4번","무라카미하루키4");
        System.arraycopy(bookArr,0,bookCopy,0,4);
        for (Book book:bookArr) {
            book.showInfo();
        }
        System.out.println("===============================================");
        for (Book book:bookCopy) {
            book.showInfo();
        }
    }
}
/*Result
제목: 1번
저자: 무라카미하루키

제목: 2번
저자: 무라카미하루키2

제목: 3번
저자: 무라카미하루키3

제목: 4번
저자: 무라카미하루키4

===============================================
제목: 1번
저자: 무라카미하루키

제목: 2번
저자: 무라카미하루키2

제목: 3번
저자: 무라카미하루키3

제목: 4번
저자: 무라카미하루키4


Process finished with exit code 0


*/
```
<br> 두 객체배열의 값이 같은걸 확인할 수 있다.
```java
public class Main {
    public static void main(String[] args) {
        Book[] bookArr = new Book[4];
        Book[] bookCopy = new Book[4];
        bookArr[0] = new Book("1번","무라카미하루키");
        bookArr[1] = new Book("2번","무라카미하루키2");
        bookArr[2] = new Book("3번","무라카미하루키3");
        bookArr[3] = new Book("4번","무라카미하루키4");
        System.arraycopy(bookArr,0,bookCopy,0,4);
        bookArr[0].setTitle("변경된 제목");
        bookArr[0].setAuthor("변경된 작가");
        for (Book book:bookArr) {
            book.showInfo();
        }
        System.out.println("===============================================");
        for (Book book:bookCopy) {
            book.showInfo();
        }
    }
}
```
<br>Result
```java
제목: 변경된 제목
저자: 변경된 작가

제목: 2번
저자: 무라카미하루키2

제목: 3번
저자: 무라카미하루키3

제목: 4번
저자: 무라카미하루키4

===============================================
제목: 변경된 제목
저자: 변경된 작가

제목: 2번
저자: 무라카미하루키2

제목: 3번
저자: 무라카미하루키3

제목: 4번
저자: 무라카미하루키4


Process finished with exit code 0

```
<br> 따라서 bookArr 의 값을 변경하면 bookCopy 의 값도 같이 변경된다.
### 해결방법
- bookArr 의 값만 복사해오면 된다.
```java
public class Main {
    public static void main(String[] args) {
        Book[] bookArr = new Book[4];
        Book[] bookCopy = new Book[4];
        bookArr[0] = new Book("1번","무라카미하루키");
        bookArr[1] = new Book("2번","무라카미하루키2");
        bookArr[2] = new Book("3번","무라카미하루키3");
        bookArr[3] = new Book("4번","무라카미하루키4");

        for (int i=0; i<bookArr.length; i++) {
            bookCopy[i] = new Book();
            bookCopy[i].setTitle(bookArr[i].getTitle());
            bookCopy[i].setAuthor(bookArr[i].getAuthor());
        }
        bookArr[0].setTitle("변경된 제목");
        bookArr[0].setAuthor("변경된 작가");
        for (Book book:bookArr) {
            book.showInfo();
        }
        for (Book book:bookCopy) {
            book.showInfo();
        }
    }
}
```
<br>Result
```java
제목: 변경된 제목
저자: 변경된 작가

제목: 2번
저자: 무라카미하루키2

제목: 3번
저자: 무라카미하루키3

제목: 4번
저자: 무라카미하루키4

제목: 1번
저자: 무라카미하루키

제목: 2번
저자: 무라카미하루키2

제목: 3번
저자: 무라카미하루키3

제목: 4번
저자: 무라카미하루키4


Process finished with exit code 0

```
주소값이 아닌 값만 가지고 오기때문에 bookArr의 값이 변경된다하여 같이 변경되지않는다.

