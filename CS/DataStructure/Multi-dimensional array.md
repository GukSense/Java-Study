## 다차원 배열
- 2차원 이상의 배열을 의미하며, 배열의 요소로 또 다른 배열을 가진 배열을 말한다.
- EX) int[][] multiArr = {{1,2,3}{4,5,6,7}};
  <br>
  ![image](https://github.com/GukSense/Java-Study/assets/101082667/1b804e1a-c31d-427d-b2fa-ccafe8e5236b)

  
### 예제)2차원 배열을 순회하는 코드 구현
```
int [][] multiArr = {{1,2,3},{4,5,6,7}};
```
```
처음 잘못 작성한 코드
```
```java
public static void main(String[] args) {
    int [][] multiArr = {
            {1,2,3},
            {4,5,6,7}
    };
    for (int i=0; i<multiArr[0].length;i++) {
        for (int j=0; j<multiArr[1].length; j++) {
            System.out.print(multiArr[i][j]+", ");
            break;
        }
        System.out.println();
    }

}
```
```
결과값 -> 1, 2, 3, Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: Index 3 out of bounds for length 3
	at org.example.Main.main(Main.java:11)
```
- ArrayIndexOutOfBoundsException 에러가 발생해버렸다. 이 에러는 <b>인덱스가 배열의 크기보다 크거나 음수 인덱스에 대한 요청</b> 이 있을 경우 발생하는 오류다.
  <br> 첫번째 for문을 돌때 multiArr[0].length 의 값은 3 이 되는데 multiArr 의 1차배열은 2개밖에 없기 때문에 3번째 1차배열 인덱스 요청이 불가하기 때문에 발생한 오류
    <br><b>쉽게 설명하면 multiArr[3][j] 배열은 존재하지않는데 요청해버려서 생긴 오류</b>
- 나도모르게 2차배열의 원소수만 신경쓴 for문을 만들어버렸다.
- 내가 고려해야할 것은 1차적으로 열을 돌면서 그 후에 행을 도는 것을 신경썼어야하는데 행의 원소개수만 고려해버렸다.
```
오류수정코드
```
```java
for (int i=0; i<multiArr.length;i++) {
    for (int j=0; j<multiArr[i].length; j++) {
        System.out.print(multiArr[i][j]+", ");

    }
    System.out.println();
}
```
```
결과값 ->1, 2, 3, 
        4, 5, 6, 7, 
```
- 이번엔 올바르 결과값이 나왔다.
- 여기서 알 수있는 것은 1차배열은 multiArr, 2차배열은 multiArr[] 로 지정? 된다는 것이다.
