## Spring **@Profile** 이란

spring 3.1 부터 포함된 기능, 환경에 맞게 적합한 profile을 사용할수 있게 하는 기능
 maven profile 과 비슷한 역할을 함

 처음 알게된 계기는 테스트 환경과 운영 환경의 설정이 다르기 떄문에 properties와  Security 환경을 다르게 구성할 필요가 있다고 생각하여 환경을 바꾸어서 적용하자라고 결론을 내렸다. 

## 설정 방법

Spring 과 SpringBoot 모두 설정을 할수 있지만 Spring 같은경우 web.xml 파일로 설정이 가능

```
<context-param>
    <param-name>contextConfigLocation</param-name>
    <param-value>/WEB-INF/app-config.xml</param-value>
</context-param>
<context-param>
    <param-name>spring.profiles.active</param-name>
    <param-value>dev</param-value>
</context-param>
```

 SpringBoot 같은경우

![Spring](/image/Spring_Profile1.png)

위와같이 properties 파일에 dev 환경과 prod 파일로 나누어 설정했다.

이런 설정 말고고 WebApplicationInitializer를 사용하여 Servlet-Context로 구성하는 방법도 있다. 

```
@Configuration
public class MyWebApplicationInitializer 
  implements WebApplicationInitializer {

    @Override
    public void onStartup(ServletContext servletContext) throws ServletException {
 
        servletContext.setInitParameter(
          "spring.profiles.active", "dev");
    }
}
```

활성프로필로 사용하기 때문에 서버실행시 셋팅이 같이 올라 오기 때문에 적용이 바로바로 가능

원래 Spring Profile 이 나오기 전에는 pom.xml에 설정을 하여 사용하는경우가 많았는데 
이러는경우에는 maven의 상태를 계속 바꿔줘야했기 때문에 설정이 잘 안된다
(maven update 를 계속 해줘야 하는상황)

 ```
 mvn clean package -Pprod
 ```
 이런설정보다는 위의 설정이 더 나은듯


위의 설정이 다 끝났다면 설정 해주고 싶은 부분에

![SpringProfile](/image/Spring_Profile2.png)

이런식으로 위에 **@Profile** 을 달아주면 된다.

설정을 확인하기위해 서버를 실행시켜주면

![Spring_Profile](/image/Spring_Profile3.png)

profiles active 가 dev라고 되어있는것을 볼수 있음
