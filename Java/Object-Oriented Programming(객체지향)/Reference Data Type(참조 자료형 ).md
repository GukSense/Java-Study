## 참조 자료형 (Reference Data Type)
- 데이터 타입의 종류에는 Reference Data Type (참조자료향) 과 Primitive Data Type (기본 데이터 타입)이 있다.
  - 기본타입 Ex) int , float, double, boolean etc..  참조자료타입 Ex) String, Date, Student etc.. 
- 기본 데이터 타입은  사용하는 메모리가 정해져있지만 참조 자료형은 클래스에 따라 다름
- 참조자료형을 사용하기 위해선 해당하는 클래스 변수로 선언을 해야한다. (단 String 클래스는 예외)

### 참조자료형 정의하여 사용하기
```
  학생이 수강한 과목들에 대한 성적을 산출하기 위한 경우 학생 클래스 속성에 과목이 모두 있으면 비효율적
  학생(Student)과 과목(Subject) 클래스를 분리하여 사용 Subject 클래스를 활용하여 수강한 과목들의 변수 타입으로 선언
  선언 된 Subject 변수는 생성 된 인스턴스가 아니므로 , Student 의 생성자에서 생성하여 사용
```
- 학생(Student) 클래스
```java
public class Student {

    private int studentId;
    private String studentName;

    Subject korean;
    Subject math;

    public Student(int studentId, String studentName) {
        this.studentId = studentId;
        this.studentName = studentName;

        korean = new Subject();
        math = new Subject();
    }

    public void  setKoreanSubject(int score) {
        korean.subjectName = "Korean";
        korean.score = score;
    }
    public void setMathSubject(int score) {
        math.score = score;
        math.subjectName = "Math";
    }
    public void showStudentScore(Student student) {
        System.out.println(
                "학생아이디: " + student.studentId + "\n" +
                "학생이름: " + student.studentName + "\n" +
                "과목: " + student.korean.subjectName + " 점수: " + student.korean.score + "\n" +
                "과목: " +  student.math.subjectName + " 점수: " + student.math.score + "\n"
        );
    }
}
```
- 과목(Subject) 클래스
```java
  public class Subject {
    int score;
    String subjectName;
  }

```
- Main 메서드
```java
  public class Main {
    public static void main(String[] args) {
        Student guk = new Student(1, "GangGuk");


        guk.setKoreanSubject(88);
        guk.setMathSubject(96);

        guk.showStudentScore(guk);
    }

}
```
- 입출력 결과
```
학생아이디: 1
학생이름: GangGuk
과목: Korean 점수: 88
과목: Math 점수: 96
```

- Subject 클래스에서 인스턴스로 과목명을 설정하기보단 클래스내에서 과목명을 더 셋업 하는 방법은 어땠을까 하는 고민이 든다.
