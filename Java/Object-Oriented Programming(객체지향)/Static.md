## Static 변수
- 공통으로 사용하는 변수가 필요한 경우
- 여러 인스턴스가 공유하는 기준 값이 필요한 경우
  -  학생마다 새로운 학번 생성
  -  카드회사에서 카드를 새로 발급할때마다 새로운 카드 번호를 부여
- 인스턴스가 생성될 때 만들어지는 변수가 아닌, 처음 프로그램이 메모리에 로딩 될 때 메모리를 할
-  ![image](https://github.com/GukSense/Java-Study/assets/101082667/28b67760-e5db-4618-8989-1ce18905fc0b)

### static 변수 선언과 사용
```
static int num;
```
- 클래스 변수, 정적변수라고도 한다.
- 인스턴스 생성과 상관 없이 사용가능하므로 클래스 이름으로 직접 창조


### 예제
- Employee class
```java
public class Employee {
    public static int seriaNum = 1000;
    private int EmployeeId;
    private String employeeName;
    private String department;

    public int getEmployeeId() {
        return EmployeeId;
    }

    public void setEmployeeId(int employeeId) {
        EmployeeId = employeeId;
    }

    public String getEmployeeName() {
        return employeeName;
    }

    public void setEmployeeName(String employeeName) {
        this.employeeName = employeeName;
    }

    public String getDepartment() {
        return department;
    }

    public void setDepartment(String department) {
        this.department = department;
    }
}

```
- Main class
```java
public class Main {
    public static void main(String[] args) {
        Employee e1 = new Employee();
        e1.setEmployeeName("Guk");
        System.out.println(e1.seriaNum);
        e1.seriaNum++;
        
        Employee e2 = new Employee();
        e2.setEmployeeName("Dae");
        System.out.println(e2.seriaNum);
    }
}
```
- 출력값
```
1000
1001
```
  - e1 인스턴스 객체에서 static 변수인 seriaNum을 ++ 했는데 e2 인스턴스 객체의 seriaNum 값도 같이 오른것을 알 수 있다, 따라서 인스턴스가 생성 될 때 만들어지는 변수가 아니라 클래스에서 공통적으로 사용하는 변수 란 걸 알 수 있다.
  - 좀 더 올바른 Main class 에서 static 변수를 호출하는 방법은 이와 같다. 출력값은 위에 것과 똑같이 나온다.
  ```java   
  public class Main {
      public static void main(String[] args) {
          System.out.println(Employee.seriaNum);
          Employee.seriaNum++;
          System.out.println(Employee.seriaNum);
      }
  }
  ```

### static 메서드 (클래스 메서드)에서는 인스턴스 변수를 사용 할 수 없다. 
  - static 메서드는 인스턴스 생성과 무관하게 클래스 이름으로 호출 할 수 있다.
  - 인스턴스 생성 전에 호출 할 수 있으므로 static 메서드 내부에서는 인스턴스 변수를 사용 할 수 없다.
  - Employee.java
  ```java
  public static void setSeriaNum(int seriaNum) {
    int i = 0;
    employeeName  = "Guk"; // 오류
    Employee.seriaNum = seriaNum; // Not오류
  }
  ```
### 변수의 유효 범위와 메모리
- ![image](https://github.com/GukSense/Java-Study/assets/101082667/243e84df-9b46-43d4-bae6-a46e6db2a430)
  - static 변수는 프로그램이 메모리에 있는 동안 계속 그 영역을 차지하므로 너무 큰 메모리를 할당하는 것은 좋지않다.
  - 클래스 내부의 여러 메서드에서 사용하는 변수는 멤버 변수로 사용하는 것이 좋음.
  - 멤버 변수가 너무 많으면 인스턴스 생성 시 쓸데없는 메모리가 할당 됨.
