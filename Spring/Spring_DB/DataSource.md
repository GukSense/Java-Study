``
김영한 강사님의 스프링 DB 데이터 접근핵심원리를 보고 복습을 위해 정리하였습니다. 
``
[강의링크](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-db-1)


### Connection을 획득하는 방법들
- 1. DriverManager 를 통해 신규 Connection 객체를 생성하는 방법
  2. HikariCP 커넥션 풀 로 생성된 커넥션 조회
  3. DBCP2 커넥션 풀 로 생성된 커넥션 조회

### Connection 획득 방법 변경에서의 문제
- 예를들어 애플리케이션에서 DriverManager 를 사용하여 Connection 을 획득하여 사용 중 이였다가 HikariCP 커넥션 풀 을 사용하는 방법으로 변경이 필요하다면,
  <br> **애플리케이션의 코드도 함께 변경해야하는 문제가 생긴다.** 의존관계가 `DriverManager` 에서  `HikariCP` 로 변경되기 때문이다.


## DataSource 이란?
- ![image](https://github.com/GukSense/TIL/assets/101082667/c9cd3577-f72b-436c-b415-423bd1f87716)
- DB Connection 획득하는 방법을 추상화 한 인터페이스
- DB 연결정보를 저장하고, Connection을 생성하고, ConnectionPool에 등록하고 관리하는 역할을 한다.
- DataSource 핵심 기능은 Connection 조회 하나라고 봐도 무방
- ```java
  public interface DataSource {
    Connection getConnection() throws SQLException;
  }
  ```
- 대부분의 `ConnectionPool`은 `DataSource` 를 이미 구현해두었기 때문에 `HikariCP 커넥션 풀` , `DBCP2 커넥션 풀` 의 코드를 직접 의존하는 것이 아니라 `DataSource`인터페이스에만 의존하도록 애플리케이션 로직을 작성하면된다.
- `ConnectionPool` 구현 기술을 변경하고 싶다면 해당 구현체로 갈아 끼우기만 하면 된다.
  -  **주의**
  -  `DriverManager` 은 `DataSource`  을 구현하지않는다 따라서   `DriverManager` 를 사용하다가 `DataSource` 기반의 커넥션 풀을 사용할려면 관련코드를 다 수정해야한다. 이런 문제를 해결하기 위해 스프링은 `DriverManager` 도 `DataSource` 를 통해 사용 할 수 있도록
  `DataSourceDriverManager` 라는 `DataSource` 를 구현한 클래스를 제공한다.

### DataSource 를 사용한 커넥션 획득방법 예시와 DriverManager 과의 차이

<br> **DriverManager**

```java
void drivrManager() throws SQLException {
        Connection connection = DriverManager.getConnection(URL, UESRNAME, PASSWORD);
        log.info("connection={}, class={}", connection,connection.getClass());
}
```
<br> **DataSource**
```java
void driverManagerDataSource() throws SQLException {
        DataSource dataSource = new DriverManagerDataSource(URL, UESRNAME, PASSWORD);
        useDataSource(dataSource);
}
```
```java
void useDataSource(DataSource dataSource) throws SQLException {
        Connection dataSourceConnection = dataSource.getConnection();        
        log.info("connection={}, class={}", dataSourceConnection,dataSourceConnection.getClass());        
}
```
- `DriverManager` 를 사용하는 방법은 Connection 을 획득할 때 마다,`URL`, `UESRNAME`, `PASSWORD` 파라미터를 계속 넘겨야한다. 하지만  `DataSource` 는 한번 설정할때 값만 입력해놓으면, 획득 할 때는 `dataSource.getConnection()` 만 호출하면 된다.

### 설정과 사용의 분리
- *설정* :  `DataSource` 를 만들고 필요한 속성들을 사용해서  `URL`, `UESRNAME`, `PASSWORD` 같은 부분을 입력하는 것을 말한다.<br>
이렇게 설정과 관련 된 속성들은 한곳에 모아놓고 관리하는 것이 향후 변경에 유연하게 대처할 수 있다.
- *사용* :  설정은 신경쓰지않고 `dataSource.getConnection()` 만 호출해서 사용하면 된다.
- 애플리케이션을 개발할 때, 설정은 한 곳에서 하지만 사용은 여러곳에서 하게된다.
- 객체를 설정하는 부분과 사용하는 부분을 좀 더 명확하게 분리 할 수 있다.
