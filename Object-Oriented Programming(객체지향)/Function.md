## 함수 (Function)
- 하나의 기능을 수행하는 일련의 코드
- 호출하여 사용 및 함수가 실행되면 반환값을 얻을 수 있다.
- 여러곳에서 호출하여 사용 할 수 있다.
- <b>코드의 재사용성, 가독성을 높일 수 있다.
<br><b>함수 구현 방법<br>
```java
int sumInt(int n1, int n2) {
  int result = n1 + n2;
  
  return result;
}
```

- 반환될 값이 있다면 데이터타입을 정해준다 ex)int 없다면  void 로 작성
- 매개변수가 있다면 () 안에 선언해주면 된다.
- {} 에는 함수 동작과정, 값 등을 작성한다.

### 함수 호출 예시
```java
  public class Main {
    public static void main(String[] args) {
        int dan = 2;
        int num = 10;

        System.out.println(resultSum(dan,num));
    }
    public static int resultSum(int n1, int n2) {
        int result = n1 * n2;
        return result;
    }
}
```
### 함수 호출과 스택 메모
![image](https://github.com/GukSense/Java-Study/assets/101082667/3c1284ae-3ab8-410b-aa56-1ecea4f20a24)

- 위 함수 호출 예시의 동작과정을 보면
  - 1. main() 가 호출되면서 젤 밑 스택에 쌓임
    2. resultSum(n1,n2) 가 호출되면서 두번째 스택에 쌓임
    3. resultSum(n1,n2) 의 모든 작업이 완료되고 반환이 끝나면  젤 위 스택부터 순서대로 제거 된다.
    4. 따라서 함수는 호출시 스택 메모리에 데이터가 쌓였다가 반환이 끝나면 메모리데이터가 삭제된다고 볼 수 있다.
