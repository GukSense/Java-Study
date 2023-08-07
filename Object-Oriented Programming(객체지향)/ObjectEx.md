## 객체 실제 사용 에시
- 구현목표
-  1.객체를 생성한다
   2.객체 마다 다른 값을 설정
   3.객체호출 하여서 실행

<br> Student class 를 만들어서 객체를 만들어주고 객체변수? 를 선언해준다.

```java
public class Student {
  private String name;
  private int age;
  private String address;
}  
```
<br> 아직 정리하지않았지만 클래스 객체안에 get set 메서드를 생성하여 만들어준다
```java
public class Student {
    // getter setter 생성
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public String getAddress() {
        return address;
    }

    public void setAddress(String address) {
        this.address = address;
    }
    
    private String name;
    private int age;
    private String address;

}
```
<br> 학생의 정보를 구현해줄 info 메서드를 생성하여준다<br>
```java
public void getInfo() {
        System.out.println(
                "이름: " + getName() + "\n" +
                "나이: " + getAge() + "\n" +
                "주소: " + getAddress() +"\n"
        );
    }
```
<br>메인 메인 메서드에서 객체를 생성하고 객체마다 setter 로 다른데이터를 입력해준다.
``` java
public class Main {
    public static void main(String[] args) {
        Student student1 = new Student();
        student1.setAge(17);
        student1.setName("민식");
        student1.setAddress("대구");

       
        Student student2 = new Student();
        student2.setAge(22);
        student2.setName("건식");
        student2.setAddress("서울");
    }
}
```
<br> set으로 설정 해 주었으니 info 메서드를 호출하여 확인
```java
public class Main {
    public static void main(String[] args) {
        Student student1 = new Student();
        student1.setAge(17);
        student1.setName("민식");
        student1.setAddress("대구");

       
        Student student2 = new Student();
        student2.setAge(22);
        student2.setName("건식");
        student2.setAddress("서울");
// info 메서드 호출
        student1.getInfo();
        student2.getInfo();
    }
}
        
```
```
이름: 민식
나이: 17
주소: 대구

이름: 건식
나이: 22
주소: 서울
```
<br> 값이 잘 출려 되는걸 확인 할 수 있다.
