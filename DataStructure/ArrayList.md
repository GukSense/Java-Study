## ArrayList
### 객체 배열을 구현한 ArrayList
- Collection 프레임워크 의 일종이며 , java.util 패키지에 속해있다.
- 기존의 배열은 선언한 배열의 길이보다 요소가 커지면 배열을 재선언 하고 복사해줬어야 했다. (상당히 비효율적)
- 배열의 요소를 추가하거나 삭제하면 다른요소들의 이동에 대한 구현도 따로 했어야함
- ArrayList 는 객체가 추가되어서 용량을 초과하면 자동으로 부족한 크기만큼 용량이 늘어난다.
  - 즉 배열과의 가장 큰 차이점은 <b> 배열은 크기가 고정되어있지만 ArrayList 는 크기가 가변적 변한다</b>
  <br>![image](https://github.com/GukSense/Java-Study/assets/101082667/a0496cb3-8676-46ee-bf19-a82731fd133c)
### ArrayList 생성 방법
- java.util 패키지에서 임포트 해주어야한다.
  ```
  import java.util.ArrayList;
  ```
  - ArrayList 를 생성해준다.
  ```java
  ArrayList<Integer> integers1 = new ArrayList<Integer>(); // 타입 지정
  ArrayList<Integer> integers2 = new ArrayList<>(); // 타입 생략 가능
  ArrayList<Integer> integers3 = new ArrayList<>(10); // 초기 용량(Capacity) 설정
  ArrayList<Integer> integers4 = new ArrayList<>(integers1); // 다른 Collection값으로 초기화
  ```
  ### ArrayList 엘리먼트 추가 / 변경 방법
  - add() 메서드를 통해 추가, set() 메서드로 변경할 수 있습니다.
  - add()는 기본적으로 리스트의 가장 끝에 값을 추가합니다.
  - 별도로 인덱스를 지정하면 해당 인덱스에 값이 추가되고 그 인덱스부터의 값들이 1 칸씩 밀립니다.
  ```java
  추가
  public class Main {
    public static void main(String[] args) {
        ArrayList list = new ArrayList<String>();
        list.add("A");
        list.add("B");
        list.add("C");
        list.add("D");
        list.add("E");
        System.out.println(list);
    }
  }
  ```
  ```
  Result
  [A, B, C, D, E]
  ```
  ```java
  변경
  public class Main {
      public static void main(String[] args) {
          ArrayList list = new ArrayList<String>();
          list.add("A");
          list.add("B");
          list.add("C");
          list.add("D");
          list.add("E");
          
          list.set(1,"F"); // 2번째 인덱스의 값을 "F"로 변경한다.
          System.out.println(list);
      }
  }
  ```
  ```
  결과
  [A, F, C, D, E]
  ```
  
  ### ArrayList 요소삭제 및 개수 확인
  - remove() 메서드를 통해 원하는 인덱스 요소 삭제 , clear() 메서드로 전체삭제를 할 수 있다.
  ```
  public class Main {
    public static void main(String[] args) {
        ArrayList list = new ArrayList<String>();
        list.add("A");
        list.add("B");
        list.add("C");
        list.add("D");
        list.add("E");
        list.remove(1);
        System.out.println(list);
        list.clear();
        System.out.println(list);
    }
  }
  ```

  ```
  결과값
  [A, C, D, E]
  []
  ```
  - size() 로 요소 개수를 확인할 수 있다.
  ```java
  public class Main {
    public static void main(String[] args) {
        ArrayList list = new ArrayList<String>();
        list.add("A");
        list.add("B");
        list.add("C");
        list.add("D");
        list.add("E");
        System.out.println(list.size());
    }
  }
  ```
  ```
  결과값
  5
  ```
  ### ArrayList 특정 인덱스의 값, 인덱스의 위치 찾기
  - get() 로 특정위치의 요소 값을 , indexOf() 로 요소의 인덱스를 알 수 있다.
  ```
  public class Main {
    public static void main(String[] args) {
        ArrayList list = new ArrayList<String>();
        list.add("A");
        list.add("B");
        list.add("C");
        list.add("D");
        list.add("E");
        System.out.println(list.get(3));
        System.out.println(list.indexOf("B"));
    }
  }
  ```
  ```
  결과값
  D  // 3번째 인덱스의 위치한 값인 D
  1  // "B"값의 위치인 1
  ```
  - indexOf 메서드는 중복된 값이 있으면 가장낮은 인덱스르 우선으로 반환한다.
  ### ArrayList 요소 중복
  - ArrayList는 값의 중복을 허용하는 Collection 이다 따라서 값이 중복되는것이 비효율적이거나 원치않으면 Set Collection을 사용하는것이 좋디.
  - ArrayList 의 중복이 문제가 되는 간단한 예시
  ```java
  public class Main {
    public static void main(String[] args) {
        ArrayList list = new ArrayList<String>();
        list.add("A");
        list.add("B");
        list.add("C");
        list.add("D");
        list.add("E");
        list.add("B");
        System.out.println(list);
        System.out.println(list.get(3));
        System.out.println(list.indexOf("B"));
    }
  } 
  ```
  ```
  결과값
  [A, B, C, D, E, B]
  D
  1 // list에서 "B" 값은 2개있지만 낮은 인덱스를 우선순위로 두기 때문에 1 하나만 나오는 모습 다만 이는 indexOf 메서드의 문제이지 중복 데이터의 문제라고 보기엔 어려울 수 있다.
  ```
  - 1. 중복된 데이터로 인해 정확한 정보를 유지하기 어려울 수 있다.
    2. 특정 데이터를 수정하거나 검색해야 할 때 중복된 항목으로 인해 어떤 항목을 수정해야하는지 혼란스러울 수 있다.
    3. 중복된 항목은 메모리의 낭비를 초래할 수 있다. 대규모 데이터 집합에서는 특히 주의해야한다.
