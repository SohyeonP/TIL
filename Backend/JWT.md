# JWT

구분: API, JSON, 암호화
링크: https://jwt.io/,https:/./velopert.com/2389

### JSON WEB TOKEN

---

웹 표준 (RFC-7519) 으로 두 개채에서 JSON 객체를 사용하요 가볍고 자가수용적인 방식으로 정보를 안정성있게 전달 하는것

자가 수용적- 자체적으로 정보를 지니고 있는것

쉽게 전달 가능

### 사용되는 상황

- 회원인증: 유저의 로그인 화면  유저가 서버에 요청을 할때 마다 JWT 를 포함하여 전달
- 정보 교류:JWT두 개체 사이에서 아정성있게 정보를 교환하기 좋은 방법

![https://velopert.com/wp-content/uploads/2016/12/jwt.png](https://velopert.com/wp-content/uploads/2016/12/jwt.png)

### Header

---

**typ:** 토큰의 타입을 지정

**alg:** 해싱 알고리즘을 지정 보통 HMAC SHA256이나 RSA사용,알고리즘은 토큰을 검증할때 signayture 에서 사용

### Payload

---

토큰에 담을 정보가 들어있는 부분 정보의 한조각을 'claim'이라고 부르고 name/value로 한쌍으로 이루어져있음 토큰안에는 여러개의 클레임을 넣을수 있음 3가지가 있음

- Registered claim-등록된
    
    등록된 클레임들은 토큰의 정보를 담기위한 클레임들 등록된클레임의 사용은 모두 선택적 
    
    - `iss`: 토큰 발급자 (issuer)
    - `sub`: 토큰 제목 (subject)
    - `aud`: 토큰 대상자 (audience)
    - `exp`: 토큰의 만료시간 (expiraton), 시간은 NumericDate 형식으로 되어있어야 하며 (예: 1480849147370) 언제나 현재 시간보다 이후로 설정되어있어야합니다.
    - `nbf`: Not Before 를 의미하며, 토큰의 활성 날짜와 비슷한 개념입니다. 여기에도 NumericDate 형식으로 날짜를 지정하며, 이 날짜가 지나기 전까지는 토큰이 처리되지 않습니다.
    - `iat`: 토큰이 발급된 시간 (issued at), 이 값을 사용하여 토큰의 `age` 가 얼마나 되었는지 판단 할 수 있습니다.
    - `jti`: JWT의 고유 식별자로서, 주로 중복적인 처리를 방지하기 위하여 사용됩니다. 일회용 토큰에 사용하면 유용합니다.
- Public claim -공개
    
     중복되지 않은 이름을 가지고 있어야함 ,충돌 방지를 위해 클레임 이름 형식을 URL형식을 짓는다.
    
- Private claim -비공개
    
    양측간의 협의하에 사용되는 클레임, 이름이 중복되어 충돌 가능성 있는 클레임 사용할때 유의
    

### Signature

---

토큰의 가장 마지막 부분

해더의 인코딩값+ 정보의 인코딩값 ⇒ 모아서 비밀키로 암호화 

[JWT.IO](https://jwt.io/)

만든 JWT는 여기서  비 암호화 해서 볼수 있다.