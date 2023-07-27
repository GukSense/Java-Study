## IF 문

### 조건문 이란?
- 주어진 조건에 따라 다른 로직을 수행할 떄 사용하기 좋은 문법
- EX) 만약 (조건식) {<br>
수행 할 로직
} 그렇지않다면 {<br>
수행 할 로직 <br>
}<br>


자바에서 가장 기초적이면서도 많이 사용하게 될 문법이다. 하지만 if문은 너무 많이 남발? 중첩해서 사용하는것은 지양해야한다.
- 가독성이 좋지 않다. 프로그래밍은 팀으로 같이 작업하는 경우가 많기 때문에, 다른 사람이 들어와서 관리 하더라도 코드를 이해할 수 있게 설계를 해야한다. But if 문이 중첩으로 들어가있으면 이해하기 어렵다.
- optional , enum , stream 등을 사용하여 콛드 가독성을 높여주는게 좋다.
- 혹여 if문을 중첩 할 상황이 나온다면 함수로 따로 빼서 깔끔하게 코드를 구성해주는것도 좋다.

  ### if 문의 종류 (if, if-else, if else-if)

  - IF: 조건이 참일 경우의만 동작하는 로직만 있으면 될 경우 사용
  - IF-else: 조건이 참인 경우와 참이아닌 모든경우에 사용 될 로직일때 사용
  - IF-elseif: 조건이 참인경우뿐 아니라 불 일 경우에도 다른 여러조건이 더 들어갈 때 사용
 

    <b>IF문 사용예시
    ```java
    public static void main(String[args]) {
      if(조건식) {
        수행 될 로직    //참일 경우
      }
    }
    ```
    <b>IF else문 사용예시
    ```java
    public static void main(String[args]) {
       if(조건식) {
        수행 될 로직    //참일 경우
        } else {
          수행 될 로직  // 참이아닌 모든경우에 수행 될 로직
        }
    }
    ```

    <b>IF else-if문 사용예시
    ```java
    public static void main(String[args]) {
       if(조건식) {
        수행 될 로직    //참일 경우
        } else if(조건식) {
          수행 될 로직  // 조건1에 불이면서 조건2에는 참일 경우 수행
        }
    }
    ```

    ### if문을 활용 예시

    ```
     로그인한 회원의 레벨이 5 이상이면 "VIP회원님 안녕하세요"를 출력하는 코드를 작성하세요. 
    ```

    ```java
    public static void main(String[args]) {
        int level = 0;
        String str = "";
        Scanner scanner = new Scanner(System.in)
        level = scanner.nextInt();
        
        if(level > 0 && level < 5) {
            str = "회원님 안녕하세요";
        } else if(level >= 5){
            str = "VIP회원님 안녕하세요";
        } else {
            str = "잘못 입력 하셨습니다.";
        }
        System.out.println(str);
    }
    
    ```

    - 필요한 값으로 회원의 레벨, 안내될 문구가 필요하다고 생각해서 정수타입 level , 문자열타입 str 변수를 선언해주고 값을 초기화 해주었다.
    - 조건식으로 1. 레벨이 1~4일때 <br>
                2. 레벨이 5이상일때<br>
                3. 레벨이 음수일때 <br>
      읈 생각하여 조건식을 구현해주었고 첫번째 조건에서 1~4 , 두번째 조건식에서 5 이상일때 , 그외 나머지인 경우는 값이 음수인 경우밖에없으니 else 만 사용하여 따로 조건을 더 설정하지않았다.

<b>IF문은 될 수있으면 중첩해서 사용하지말고 가독성있게 코드를 설계하여 사용해주어야 하는것을 명심하자.
