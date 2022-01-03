## **ResponseEntity**를 사용하는 이유


### **ResponseEntity**?
---
Spring에서 제공하는 클래스중 _HttpEntity_ 라는 클래스가 존재하는데 _HttpEntity_는 HTTP 요청 또는 응답에 해당하는  Header,Body를 포함하고있는 클래스임

내가 가장 많이 쓰는 방법은

```
@RequestMapping(value = "/user", method = { RequestMethod.GET })
	public ResponseEntity<String> testUser(@RequestParam String user){
      
      Message message = Message.builder()
          .message("유저의 정보가 존재하지 않습니다.")
          .build();

    
    /* 어떤 로직을 수행 */

    return new ResponseEntity<>(message,HttpStatus.OK);
  }

```
이런식으로 많이 사용한다

~~직접 코드를 돌린건 아니고 이런식으로 사용한다는것~~

