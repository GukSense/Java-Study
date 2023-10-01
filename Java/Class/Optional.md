## Optional
### Optional 이란?
- 자바에서 NullPointException 를 방지할 수 있도록 도와주는 클래스이다.
- Null이 올 수 있는 값을 감싸는 Wrapper 클래스다.
- Null이 발생하면 오류가 발생할 가능성이 높은 경우 '결과없음'을 명확하게 드러내기 위해 메소드의 반환타입으로 사용되도록 설계되었다.

### Optional 사용예시
우편번호 검사코드(Optional이 없을 시)
```java
public String findPostCode() {
    UserVO userVO = getUser();
    if (userVO != null) {
        Address address = user.getAddress();
        if (address != null) {
            String postCode = address.getPostCode();
            if (postCode != null) {
                return postCode;
            }
        }
    }
    return "우편번호 없음";
}
```
Optioanl 사용코드
```java
public String findPostCode() {
    // 위의 코드를 Optional로 펼쳐놓으면 아래와 같다.
    Optional<UserVO> userVO = Optional.ofNullable(getUser());
    Optional<Address> address = userVO.map(UserVO::getAddress);
    Optional<String> postCode = address.map(Address::getPostCode);
    String result = postCode.orElse("우편번호 없음");

    // 그리고 위의 코드를 다음과 같이 축약해서 쓸 수 있다.
    String result = user.map(UserVO::getAddress)
        .map(Address::getPostCode)
        .orElse("우편번호 없음");
}
```

### 숙지사항
<br> Optional은 반한타입으로써 에러발생할수 있는 경우 결과를 명확하게 하기위해서 만들었다.
 Null 을 반환하는것보다 값의 유무르 나타내는 객체를 반환하는것이 합리적일때 사용하여야한다. 
