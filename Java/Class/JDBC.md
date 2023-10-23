## JDBC
![image](https://github.com/GukSense/TIL/assets/101082667/ed91abc5-5f6e-4e02-b083-9922cab3d674)
- 자바기반 애플리케이션의 데이터를 DB에 저장및 업데이트하거나 DB데이터를 자바에서 사용할수 있 도록 도와주는 API
- JDBC 에서는 3가지 기능을 표준 인터페이스로 제공한다.
  -  Java.sql.Connection -> 연결
  -  java.sql.Statement -> SQL을 담은 내용
  -  java.sql.ResultSet -> SQL 요청 응답
## JDBC 사용하기 전 문제와 해결
- DB를 다른 종류의 DB로 변경 시, 각 DB에 맞는 사용코드로 함께 변경해야하는 문제
  - 애플리케이션 로직을 JDBC 표준 인터페이스에만 의존하여 DB변경시 구현 라이브러리만 변경시킨다 따라서 서버 사용코드는 그대로 유지할수 있게 됨
- 개발자가 DB별로 Connection, Sql문, 결과응답시 사용될 코드? 을 새로 학습해야하는 문제
  - JDBC 표준 인터페이스 사용법만 익히면 다른 수십개에도 동일 적용시킬수 있다.
## JDBC 동작흐름
![image](https://github.com/GukSense/TIL/assets/101082667/3e9bab0a-302e-4cd6-be42-6b8253fc6651)
- Java 애플리케이션 내에서 JDBC api 를 사용하여 DB에 접근하는구조
- JDBC api 를 사용하기 위해서는 JDBC 드라이버를 먼저 로딩후 DB와 연결해야한다.
![image](https://github.com/GukSense/TIL/assets/101082667/38a3b9bf-fb6e-4424-86b2-e75455e0864b)
- 1. JDBC 드라이버 로딩 -> 사용하고자하는 JDBC 드라이버를 선택하고 DriverManager 클래스를 통해 로딩한다. 
- 2. Connection 객체 생성 -> DriveManager를 통해 데이터베이스와 연결되는 섹션인 Connection 객체를 생성한다.
- 3. Statement 객체 생성 -> 작성된 Sql 쿼리문을 실행하기위한 객체
- 4. Query 실행  -> Statement 객체를 이용하여 입력한 sql 쿼리문을 실행
- 5. ResultSet 객체로부터 데이터 조회 -> 실행한 sql 쿼리문으로 가지고오는 데이터정보들
- 6. 사용된 객체 Close -> JDBC api 를 통해 사용한 객체 Connection, Statement, ResultSet을 사용한 순서의 역순으로 닫는다.
