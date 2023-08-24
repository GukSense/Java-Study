## 객체간의 협력 (Collaboration)
### 객체 지향 프로그래밍에서의 협력 
- 객체지향 프로그래밍 에서는 객체간의 협력이 이루어진다.
- 협력을 위해서 필요한 메세지를 전달하고 이를 처리하는 기능이 구현되어야 함
- 객체 협력의  예 <br>
  ![image](https://github.com/GukSense/Java-Study/assets/101082667/10352260-4ff3-418b-8a0a-8024ffeab477)

## 버스와 지하철을 타는 예제 프로그래밍
```
철수는 버스와 지하철을 타고 학교에갑니다.
철수가 현재 가지고 있는 금액은 5000원이고, 요금 1200원 지하철을 타고 환승해서 요금 1000원 버스를 타서 학교에 도착합니다.
철수가 학교로 가는 상황을 객체지향적으로 구현해보세요.
```
### 학생클래스
```java
public class Student {
  private String name;
  private int money;
  public Student(String name, int money) {    // 객체 생성 동시에 생성자로 name,money 설정
      this.name = name;
      this.money = money;
  }
  public String getName() {
      return name;
  }
  public int getMoney() {
      return money;
  }
  public void setMoney(int fare) {
      money -= fare;
  }
  public void takeSubway(Subway subway) {  
      System.out.print(name +"고객님 요금액은 " + subway.getSubwayFare() + " 입니다.");
      subway.setSubwaySales();
      subway.setPassengerNum();
      setMoney(subway.getSubwayFare());
      System.out.println("이용해 주셔서 감사합니다.");
  }
  public void takeBus(Bus bus) {
      System.out.print(name + "고객님 요금액은 " + bus.getBusFare() + " 입니다.");
      bus.setBusSales();
      bus.setPassengerNum();
      setMoney(bus.getBusFare());
      System.out.println("이용해 주셔서 감사합니다.");
  }
  public void printInfoStudent() {
      System.out.println(
              "학생 " + getName() + "의 현재 머니는 " + getMoney() + "원 입니다."
      );
  }
}
```
- 처음 takeSubway, takeBus 메서드를 생성할 때, Student 클래스가 아닌, 각 Subway 클래스와 Bus 클래스에 메서드를 생성하는 실수를 하였다.
  - 단순하게 버스와지하철이니까 각 클래스에 하나씩 생성하였는데 사용하는 객체의 주도? 가 Student 클래스에 있으니까 Student 클래스에 메서드를 생성하는게 맞다고 생각해서 수정해주었다.
- 메서드의 매개변수로 다른 클래스의 객체를 받아 올 수 있다.
    
### 지하철 클래스
```java
public class Subway {
    private int subwayNum;
    private int passengerNum;
    private int subwaySales;
    private int subwayFare;

    public Subway(int subwayFare) {
        subwaySales = 0;
        passengerNum = 0;
        this.subwayFare = subwayFare;
    }
    public int getSubwayNum() {
        return subwayNum;
    }

    public void setSubwayNum(int subwayNum) {
        this.subwayNum = subwayNum;
    }

    public int getPassengerNum() {
        return passengerNum;
    }

    public void setPassengerNum() {
        passengerNum ++;
    }

    public int getSubwaySales() {
        return subwaySales;
    }
    public void setSubwaySales() {
        subwaySales += subwayFare;
    }

    public int getSubwayFare() {
        return subwayFare;
    }

    public void setSubwayFare(int subwayFare) {
        this.subwayFare = subwayFare;
    }
    public void printSubwayInfo() {
        System.out.println(
                "오늘 하루 지하철 이용고객 수는 " + getPassengerNum() + " 이고, " +
                "오늘 총 수입은 " + getSubwaySales() + " 입니다.\n"
        );
    }
}
```
- passenger 은 처음 초기화 후 프로그램이 종료 될때까지 값이 다시 초기화 될 수 없으니까 final로 선언 해주는건 어떠했을까 라는 생각이 들었다.
### 버스 클래스
```java
public class Bus {
    private int busNum;
    private int passengerNum;
    private int busSales;
    private int busFare;

    public Bus(int busFare) {
        this.busFare = busFare;
        busSales = 0;
    }
    public int getBusNum() {
        return busNum;
    }

    public void setBusNum(int busNum) {
        this.busNum = busNum;
    }

    public int getPassengerNum() {
        return passengerNum;
    }

    public void setPassengerNum() {
        passengerNum++;
    }

    public int getBusSales() {
        return busSales;
    }

    public void setBusSales() {
        busSales +=  busFare;
    }

    public int getBusFare() {
        return busFare;
    }

    public void setBusFare(int busFare) {
        this.busFare = busFare;
    }

    public void printBusInfo() {
        System.out.println(
                "오늘 하루 버스 이용고객 수는 " + getPassengerNum() + " 이고," +
                        "오늘 총 수입은 " + getBusSales() + " 입니다.\n"
        );
    }
}

```
### 메인 클래스
```java
public class Main {
    public static void main(String[] args) {

        Subway s = new Subway(1200);
        Bus b = new Bus(1000);
        Student chul = new Student("철수", 5000);

        chul.takeBus(b);
        chul.printInfoStudent();

        chul.takeSubway(s);
        chul.printInfoStudent();

        System.out.println();

        s.printSubwayInfo();
        b.printBusInfo();

    }
}
```
- 결과
```
철수고객님 요금액은 1000 입니다.이용해 주셔서 감사합니다.
학생 철수의 현재 머니는 4000원 입니다.
철수고객님 요금액은 1200 입니다.이용해 주셔서 감사합니다.
학생 철수의 현재 머니는 2800원 입니다.

오늘 하루 지하철 이용고객 수는 1 이고, 오늘 총 수입은 1200 입니다.

오늘 하루 버스 이용고객 수는 1 이고,오늘 총 수입은 1000 입니다.
```

### 후기
- 메서드의 기능 구현 자체는 어렵지않지만 객체들간의 관계를 생각해서, 각 객체가 가지고있어야할 메서드를 구현해낸다는게 생각보다 어려웠다.
- 객체의 주도권?을 좀 더 생각해서 기능 구현을 해보는 연습이 필요 할 것 같다.
- 그리고 하나의 메서드안에 여러개의 함수를 넣어서 구현하는게 디자인적으로 옳은지 궁금점이 들었다 추후에 물어 볼 사람이있으면  물어보고 의견을 듣고 싶다.
