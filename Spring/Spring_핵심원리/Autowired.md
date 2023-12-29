## 의존관계 주입
- 스프링의 핵심 기능에는 컨테이너와 빈이 있고, 이 컨테이너와 빈에서 객체지향설계의 핵심인 OCP, DIP 를 잘 지키도록 도와주는것 중 하나가 의존관계주입이다.
- 스프링에서 의존관계 주입을 하는 대표적인 방법은 *생성자주입*,*필드주입*,*세터주입* 이 있다.

### 생성자 주입
- 생성자를 통해 의존관계를 주입받는 방법.
- 생성시점에 한번 호출 되기 때문에, *불변*하고, *필수* 의존관계에 주로 사용한다. (설정 초기때만 호출되고, 외부에서 수정 할 수 없도록 하기위 )
- **생성자가 하나만 있으면, `@Autowired` 를 생략할 수 있다.**
**사용예시**

```java

    @Component
    public class MyComponent {
    
        private final MyDependency myDependency;
    
        // 생성자 주입 (생략가능
        @Autowired
        public MyComponent(MyDependency myDependency) {
            this.myDependency = myDependency;
        }
    
    }
  

```
### 필드 주입
- 필드에 주입하는 방법.
- 코드가 간결해지는 장점이 있다.
- 외부에서 변경이 불가하여 테스트하기 불편해진다.
  - 테스트환경에서 스프링환경없이 순수한 자바코드로만 테스트를 할 수 없음. 
  - 테스트환경에서 사용은 괜찮다.
  - 스프링 설정을 목적으로 하는 `Configuration` 같은 곳 에서만 별도로 사용.
**사용예시**

```java

    @Component
    public class MyComponent {
     
     @Autowired
     private MyDependency myDependency;
    
    }
  

```
### 세터 주입
- 필드 값을 변경하는 수정자 메서드를 통해 의존관계를 주입하는 방법.
- 선택, 변경 가능성이 있는 의존관계에 사용한다.
  - ex) 중간에 구현체를 바꾸고싶은 경우, 호출하여 사용.
- `@Autowired` 는 주입 할 대상이 없으면 오류가 발생하는데, 주입 할 대상이 없어도 동작하게 할려면 `@Autowired(required = false` 로 지정해주면 된다.
**사용예시**


```java
    @Component
    public class MyComponent {
    
     private MyDependency myDependency;
    
     // 세터 주입
     @Autowired
     public void setMyDependency(MyDependency myDependency) {
         this.myDependency = myDependency;
     }
    
    }
  

```
### 조회 빈이 2개 이상일때 Autowired
#### 필드명매칭
- Autowired 는 기본적으로 타입 매칭을 먼저하고(타입순으로 우선 조회), 같은 타입빈이 2개 이상일 경우 필드명으로 이름을 매칭한다.
<br>**예시**

```java
  
    /* 기존코드
    @Autowired
    private Dependency dependency;
    */
    // 개선코드
    private MyDependency firstDependency;
    
```
#### @Qualifier 사용
- 추가 구분자를 붙여주는 방법. (빈 이름을 변경하는것은 아니다.)
<br>**빈 등록시 @Qualifier를 붙여 준다.**
```java
@Component
@Qualifier("mainDataSource")
public class FirstDataSource implements Repository {}
```

```java
@Component
@Qualifier("secondDataSource")
public class SecondDataSource implements Repository {}
```
<br>**의존관계주입할때 @Qualifier를 붙여 주고 등록이름을 적어준다.**
```java
@Autowired
public DataService(@Qualifier("mainDataSource") Repository respository) {
    this.respository = respository;
}
```
<br>*@Qualifier 매칭순서*
- 1. @Qualifier끼리 매칭
  2. 없으면 빈 이름 매칭
  3. 1번 2번 둘다 없을시 `NoSuchBeanDefinitionException` 예외 발생.
  

#### @Primary 사용
- 같은타입의 빈 중에서 우선순위를 지정해줄 수 있다.
- `@Qualifier` 와 달리 `@Primary` 하나만 지정해두고 의존관계 주입에서 `@Qualifier`를 명시해주지 않아도 되는 장점이 있다. 즉, 코드가 더 깔끔하다.
<br> **예시**
```java
@Component
@Primary
public class FirstDataSource implements Repository {}
```
#### 활용과 우선순위.
- 메인으로 사용할 빈에는 `@Primary`을 사용하여 기본 디폴트 값을 지정해주고, 특별한 상황에 사용할 빈으로는 `@Qualifier` 지정하여 사용하는것이 코드를 깔끔하게 유지 할 수 있다.
- 앞서 말했듯이, `@Primary` 는 기본 디폴트처럼 동작하고,`@Qualifier` 는 상세하게 동작하기 때문에 스프링은 자동보다는 수동이, 넓은선택권보다는 좁은 선택권이 우선권을 가져간다. 그래서 둘이 붙는다면 `@Qualifier` 우선권이 높다.
