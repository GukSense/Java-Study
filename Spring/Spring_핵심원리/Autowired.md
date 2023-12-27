## 의존관계 주입
- 스프링의 핵심 기능에는 컨테이너와 빈이 있고, 이 컨테이너와 빈에서 객체지향설계의 핵심인 OCP, DIP 를 잘 지키도록 도와주는것 중 하나가 의존관계주입이다.
- 스프링에서 의존관계 주입을 하는 대표적인 방법은 *생성자주입*,*필드주입*,*세터주입* 이 있다.

### 생성자 주입
- 생성자를 통해 의존관계를 주입받는 방법.
- 생성시점에 한번 호출 되기 때문에, *불변*하고, *필수* 의존관계에 주로 사용한다. (설정 초기때만 호출되고, 외부에서 수정 할 수 없도록 하기위 )
- **생성자가 하나만 있으면, `@Autowired` 를 생략할 수 있다.**
**사용예시**

``

    @Component
    public class MyComponent {
    
        private final MyDependency myDependency;
    
        // 생성자 주입 (생략가능
        @Autowired
        public MyComponent(MyDependency myDependency) {
            this.myDependency = myDependency;
        }
    
    }
  

``
### 필드 주입
- 필드에 주입하는 방법.
- 코드가 간결해지는 장점이 있다.
- 외부에서 변경이 불가하여 테스트하기 불편해진다.
  - 테스트환경에서 스프링환경없이 순수한 자바코드로만 테스트를 할 수 없음. 
  - 테스트환경에서 사용은 괜찮다.
  - 스프링 설정을 목적으로 하는 `Configuration` 같은 곳 에서만 별도로 사용.
**사용예시**

``

    @Component
    public class MyComponent {
     
     @Autowired
     private MyDependency myDependency;
    
    }
  

``
### 세터 주입
- 필드 값을 변경하는 수정자 메서드를 통해 의존관계를 주입하는 방법.
- 선택, 변경 가능성이 있는 의존관계에 사용한다.
  - ex) 중간에 구현체를 바꾸고싶은 경우, 호출하여 사용.
- `@Autowired` 는 주입 할 대상이 없으면 오류가 발생하는데, 주입 할 대상이 없어도 동작하게 할려면 `@Autowired(required = false` 로 지정해주면 된다.
**사용예시**

``

    @Component
    public class MyComponent {
    
     private MyDependency myDependency;
    
     // 세터 주입
     @Autowired
     public void setMyDependency(MyDependency myDependency) {
         this.myDependency = myDependency;
     }
    
    }
  

``

