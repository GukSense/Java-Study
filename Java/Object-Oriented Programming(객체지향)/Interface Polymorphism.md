# 인터페이스의 다형성을 활용해서 구현 해보는 예제
- DAO 에서 연결 될 DB Type 에 따라 다른 로직처리를 할 것이다.
- 환경파일에서 DB 타입 정보를 읽고 그 정보에맞는 인터페이스 인스턴스를 생성해서 실행하는 로직 구현
  ![image](https://github.com/GukSense/TIL/assets/101082667/832866cb-ce66-4300-959d-b732b76941e8)


  ## 도메인 클래스
  유저 정보가 담긴 도메인 클래스
  ```java
  package javaProject.interfacePra.userInfo;

  public class UserInfo {
  	//domain
  	private String userName;
  	private Long userId;
  	private String userPassword;
  	
  	public String getUserName() {
  		return userName;
  	}
  	public void setUserName(String userName) {
  		this.userName = userName;
  	}
  	public Long getUserId() {
  		return userId;
  	}
  	public void setUserId(Long userId) {
  		this.userId = userId;
  	}
  	public String getUserPassword() {
  		return userPassword;
  	}
  	public void setUserPassword(String userPassword) {
  		this.userPassword = userPassword;
  	}		
  }
  ```
  ## UserDAO 인터페이스 구현
  db에 접근하는 로직은 insert , update , find 등을 구현하였다.
  ```java
  package javaProject.interfacePra.userInfo.userDAO;

  import javaProject.interfacePra.userInfo.UserInfo;
  
  public interface UserDAO {
  	void insertUserInfo(UserInfo user);
  	void updateUserInfo(UserInfo user);
  	void findUserInfo(UserInfo user);
  }
  ```
## 인터페이스 구현 클래스
DB 와 연결 했다는 가정하에 임시로 println으로 구현해주었다. Oracle 클래스는 Oracle, Mysql은 Mysql 로 출력 되도록
```java
  package javaProject.interfacePra.userInfo.userDAO.mySql;
  import javaProject.interfacePra.userInfo.UserInfo;
  import javaProject.interfacePra.userInfo.userDAO.UserDAO;

  public class Mysql implements UserDAO {
  
  	@Override
  	public void insertUserInfo(UserInfo user) {
  		System.out.println("insertInto Mysql DB userId=" + user.getUserId());
  		
  	}
  
  	@Override
  	public void updateUserInfo(UserInfo user) {
  		
  		System.out.println("updateInto Mysql DB usderId="+ user.getUserId());
  	}
  
  	@Override
  	public void findUserInfo(UserInfo user) {
  		System.out.println("find UserId from Mysql" + user.getUserId());
  		
  	}
  	
  }
  public class Oracle implements UserDAO {
  
  	@Override
  	public void insertUserInfo(UserInfo user) {
  		System.out.println("insertInto ORacle DB userId=" + user.getUserId());
  		
  	}
  
  	@Override
  	public void updateUserInfo(UserInfo user) {
  		System.out.println("updateInto Oracle DB usderId="+ user.getUserId());
  		
  	}
  
  	@Override
  	public void findUserInfo(UserInfo user) {
  		System.out.println("find UserId from Oracle" + user.getUserId());
  		
  	}
  	
  }
```

## db.properties 환결파일
```java
DBTYPE=ORACLE
```
## Test를 위한 Main 클래스
```java
public class userClient {

	public static void main(String[] args) throws IOException {
		
		FileInputStream fis = new FileInputStream("db.properties");
		
		Properties prop = new Properties();
		prop.load(fis);
		
		String dbType = prop.getProperty("DBTYPE");
		System.out.println(dbType);
		
		UserInfo user = new UserInfo();
		user.setUserId((long) 124);
		
		UserDAO userDao = null;
		
		if(dbType.equals("ORACLE")) {
			userDao = new Oracle();
		} else if(dbType.equals("MYSQL")) {
			userDao = new Mysql();
		} else {
			System.out.println("Not Supported");
		}
		
		if(userDao != null) {
			userDao.insertUserInfo(user);
			userDao.findUserInfo(user);
			userDao.updateUserInfo(user);
		}
	}

}
```

- 환경파일의 key 값과 value 값을 읽어오기 위해 FileInputStream 클래스와 Properties 클래스를 사용하였습니다.
- dbType 값에 따라 다른 인스턴스를 생성하도록 구현하여 구현 후 에는 insertUserInfo(user),userDao.findUserInfo(user),userDao.updateUserInfo(user) 를 실행합니다.
- 인터페이스를 통해 큰 수정없이 다양한 로직을 확장하고 적용 할 수 있는것을 알수있다.
