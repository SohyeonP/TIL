# 커밋 메세지 정리

생성일: 2021년 4월 23일 오후 12:43

프로젝트 내용을 한글로 작성하는경우  = 간결하게 작성

영어로 작성하는경우를 정리

커밋 메세지 규칙

[How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)

[Git Commit Message Conventions](https://docs.google.com/document/d/1QrDFcIiPjSLDn3EL15IJygNPiHORgU1_OOAqWjiDU5Y/edit)

### 동명사보다 명사를 더 많이 사용

동사를 명사화 시키보다는 그 의미를 잘 표현하는 명사를 찾아서 사용

**관사는 사용하지 않음**

꼭 필요한 경우가 아니면 a ,an,the 는 사용하지 않음

### 좋은 커밋 메세지를 위한 영어 단어 목록

---

### Fix

---

- 가장 자주 사용되는 커밋 로그 중 하나로 'Fix'가 있다. 보통 올바르지 않은 동작을 고친 경우에 사용

<aside>
🛠 Fix A = A를 수정

</aside>

<aside>
🛠 Fix A in B = B의 A를 수정합니다.

</aside>

<aside>
🛠 Fix A which B, Fix A that B = B절인 A를 수정

</aside>

<aside>
🛠 Fix A to B, Fix A to be B = B를 위해 A를 수정

</aside>

<aside>
🛠  Fix A so that B = A를 수정해서 B가 됨

</aside>

<aside>
🛠 Fix A where B = B처럼 발생하는 A를 수정

</aside>

<aside>
🛠 Fix A  when B= B 일때 발생하는 A를 수정

</aside>

### ADD

---

코드나 테스트, 예제,문서 등의 추가가 있을때 사용

<aside>
🛠 Add a = A를 추가

</aside>

<aside>
🛠 Add A for B = B를 위해 A를 추가

</aside>

<aside>
🛠 Add A to B = B에 A를 추가

</aside>

### REMOVE

---

코드의 삭제가 있을때 사용

<aside>
🛠 Remove A =A를 제거

</aside>

<aside>
🛠 Remove A from B = B에서 A를 제거

</aside>

### USE

---

특별히 무언가를 사용해 구현하는 경우

<aside>
🛠 Use A = A를 사용

</aside>

<aside>
🛠 Use A for B = B에 A를 사용

</aside>

<aside>
🛠 Use A to B = B가 되도록 A를 사용

</aside>

<aside>
🛠 Use A in B = B에서 A를 사용

</aside>

<aside>
🛠 Use A instead of  B = B 대신 A를 사용합니다.

</aside>

### REFACTOR

---

전면 수정이 있을때 사용

<aside>
🛠 Refactor A= A를 전면 수정

</aside>

### SIMPLIFY

---

복잡한 코드를 단순화 할때 사용, refactor 보다 약한 수정의 경우 이용하면 좋음

<aside>
🛠 Simplify A = A를 단순화

</aside>

### Update

---

개정이나 버전 업데이트가 있을때 사용, Fix 와 달리 정상적으로 동작하는경우의 부분에만 수정,추가,보완을 한다는 개념 코드보다는 주로 문서나 리소스, 라이브러리등에 사용

<aside>
🛠 Update A to B  = A를 B로 업데이트 합니다.

</aside>
