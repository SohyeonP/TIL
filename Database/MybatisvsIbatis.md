# Mybatis VS ibatis

구분: JAVA, SPRING
난이도: 어려움
링크: https://sjh836.tistory.com/127

스프링 관련 프로젝트를 하다 보니  mybatis 하나만 있는줄 알았는데 ibatis 가 있다는것에 놀랐다 하지만 둘이 비슷한 구조를 가지고 있고 간단한 차이점만 있기 때문에 간단하게 짚고 넘아가자

### Mybatis?

객체지향 언어인 자바의 관계형 데이터베이스 프로그래밍을 쉽게 도외주는 개발 프레임워크

자바는 jdbc api 제공하지만 1개의 클래스에 반복되는 코드가 존재하기 때문에 자바 언어와 sql언어가 같이 있게되어 재사용성이 안좋아 진다. 그런 단점들을 개선 한것이다.

 

**특징**

- 한 두줄의 자바 코드로 DB 연동을 처리

→ 밑의 그림처럼 
![MybatisvsIbatis1](/image/MybatisvsIbatis1.png)

간단하게 이렇게 몇줄의 코드로 작성을 할수 있다.

spring에 dependency로 쉽게 추가 가능

```java
<dependency>

    <groupId>org.mybatis</groupId>

   <artifactId>mybatis</artifactId>

   <version>3.2.2</version>

</dependency>
<dependency>

   <groupId>org.mybatis</groupId>

   <artifactId>mybatis-spring</artifactId>

    <version>1.2.0</version>

</dependency>
```

---

### Ibatis VS Mybatis

Ibatis는 아파치 프로젝트였을때 이야기 하는것이고, 구글로 넘어가게 되면서 이름만 바뀐것 차의점을 보면

![MybatisvsIbatis1](/image/MybatisvsIbatis2.png)

이런식으로만 차이가 있다. 

---

### 마이바티스 구조

![MybatisvsIbatis1](/image/MybatisvsIbatis3.png)

mybatis-config 는 mybatis의 메인 환경설정 파일 DBMS 설정 어떤 맵퍼 파일들이 있는지 알수 있음

맵퍼에 있는 SQL명령어는 Map 에담아 저장및 관리 찾을때는 고유 아이디로 찾을수 있음

---

### API

SqlSessionFactoryBuilder클래스: build()메소드를 통해 mybatis-config를 로딩하여 SqlSessionFactory 객체를 생성

SqlSessionFactoryzmffotm: Sqlsession객체에 대한 팩토리 객체, openSession()이라는 메소드를 통해

Sqlsession을 얻을 수 있음

```java
public class SqlSessionFactoryBean { 
	private static SqlSessionFactory sessionFactory = null; 
static { 
	try { 
		if (sessionFactory == null) { 
				Reader reader = Resources.getResourceAsReader("mybatis-config.xml"); 
				sessionFactory = new SqlSessionFactoryBuilder().build(reader);
 }
	 } catch (Exception e) {
		 e.printStackTrace(); 
	} 
} 
public static SqlSession getSqlSessionInstance() { 
		return sessionFactory.openSession(); 
		} 
}
```