## Sl4j
- Java 의 [로깅(Logging)](https://github.com/GukSense/TIL/blob/main/CS/Etc/Logging.md) 라이브러리로, Simple Logging Facade for Java의 약자로 다양한 logging 프레임워크에대한 인터페이스 역할을 한다.
- 인터페이스이기 때문에 단독으로 사용이 불가능합니다.
- 필요에의해 라이브러리를 변경할 때 코드의 변경없이 가능하다.

![image](https://github.com/GukSense/TIL/assets/101082667/318f2a75-4c4d-4856-a24f-0e45b0028cd3)
<br>
개발 할 때, Slf4j api를 사용하여 로깅코드를 작성
<br>
배포 할 때, 바인딩 된 logging 프레임워크가 실제 로깅 코드를 수행
<br>
### Bridge
- 다른 로깅의 API Logger 호출을 Slf4j 인터페이스로 연결해 Slf4j api가 대신처리할수있도록 해주는 라이브러리 (slf4j로 연결해주는 다리)
### Slf4j api
- 로깅에대한 인터페이스를 제공한다 로깅 역할을 수행할 추상메서드를 제공한다고 보면 된다. 주의할 점으로는 반드시 하나의 api에 하나의 Binding을 둬야한다.
### Slf4j Binding(.jar)
- Slf4j 인터페이스를 logging 프레임워크와 연결하는 어댑터 역할을 하는 라이브러리 Slf4j api 주의점과 같이 api에 하나의 binding을 둬야한다.

// 추후 logging 공부 후 다시 정리해볼 것

### log level 
- 아래로 내려 갈 수록 log 레벨이 높음
- trace -> 디버그 레벨이 너무 광범위한 것을 해결하기 위해서 좀 더 상세한 이벤트를 나타낸다.
- debug -> 개발시 디버그 용도로 사용하는 메시지
- info -> 어떠한 상태 변경과 같은 정보성 메시지를 나타낸다.
- warn -> 프로그램의 실행에는 문제가 없지만, 향 후 시스템 에러의 원인이 될 수 있는 경고성 메시지
- error -> 어떠한 요청을 처리하는 중 문제가 발생한 상태를 나타내는 메시지, 프로그램 동작에 큰 문제가 발생했다는 것으로 즉시 문제를 조사해야하는것
  
