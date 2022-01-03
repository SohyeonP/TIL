## Eclipse 주석 커스텀 하기
---

이클립스의 주석 단축키는 `'ctrl +shift +/'` 주석 해제는 `'ctrl+shift+\'` 이다. 하지만 주석을 하게 되면  영역으로만 되면 좋겠지만 그렇지 않고 줄바꿈이 이루어 지거나 주석의 줄이 내려가버리는 현상이 일어나기 떄문에  주석을 셋팅 해놓는것이 좋다

![eclipse1](/image/eclipse1.png)   영역지정을 한부분만 하게되면 더욱 깔끔해진다

이클립스의 Window > Preference > Java > CodeStyle >Formatter로 접속한다.

![eclipse2](/image/eclipse2.png)   
Formatter에서  현재 profile 이 아닌 New를 눌러 새 Profile을 만든다

![eclipse2_1](/image/eclipse2_1.png) 

Profile 이름을 원하는 이름으로 지정해준후 다시 아까의 화면으로 넘어와 Edit 눌러준다

![eclipse3](/image/eclipse3.png) 원하는 셋팅을 할수 있는 창이 나오는데 미리보기를 통해 본인이 적용한 셋팅을 볼 수 있음

위의 말한 설정을 적용할려면

![eclipse4](/image/eclipse4.png)


현재 이런환경으로 되어있을텐데 _Count width from comment's starting position_ 의 체크박스를 설정해주고
_Enable Javadoc comment formatting_ 과 _Enable block comment formatting_ 기존 설정과 안의 세부 설정 체크박스를 해제해 준다.


![eclipse4](/image/eclipse5.png)

그 창을 닫아 Apply를 해주면 위의 코드 처럼 주석이 영역 잡힌 부분만 주석 처리가 된다.
