---
layout:     post
title:      JSPClass-days09
date:       2019-05-08 23:00:00
summary:    쿠키 / 세션 / 커넥션풀 
categories: WEBClass
---





쿠키를 사용하는 로그인 상태관리 (인증과 권한)

인증 : 로그인 / 권한 : 등급

ex01

------

CHAPTER 14 데이터베이스 프로그래밍 기초 (JDBC)

08 커넥션풀

8.2.5 커넥션 풀 속성 설명

ex02

톰캣(WAS) 이 제공하는 커넥션풀 사용 

1. C:\apache-tomcat-8.5.39\lib 의 tomcat-dbcp.jar 을 이클립스의 lib 폴더에 추가

2. apache-tomcat.org에서 왼쪽탭의 10_JDBC DataSource

3. [Oracle 8i, 9i & 10g](http://tomcat.apache.org/tomcat-8.5-doc/jndi-datasource-examples-howto.html#Oracle_8i,_9i_&_10g) 의 가이드 참고

4. META-INF 폴더 에 context.xml 파일 추가(Server의 context.xml 을 복사 붙여넣기)

5. web.xml  설정추가

6. com.util에 ConnectionProvider 클래스 파일 추가 및  getConnection 메서드 추가

   p421.  커넥션 반환하는 코딩 try~catch~finally

   

   

   

--------------------------------------------

CHAPTER 10 클라이언트와의 대화 2 : 세션 

- 첫번째 접속이 발생할때 세션 생성

- 브라우저를 닫을 때 OR 세션 TIMEOUT 시간이 지나면 세션은 삭제됨

-  jsp 파일에서는 직접 session 객체에 접근 / 서블릿 java 파일에서는 request.getSession()해서 사용

- 브라우저 종류별로 다른 세션 생성

  크롬 : 세션 ID : 8BEE40D60E3FF1347AAEB938BDD62489

  IE : 세션 ID : 6AC67C89D2D87DB3986BC561F74B0F37

  

01 세션 사용하기 : session 기본 객체 

ㄱ. <@page session ="true" 기본값

ㄴ. session.set/getAtrribute("세션명","세션값")

1.4 세션 종료  (ex05)

 session.invalidate() 메소드 사용

ㄱ. session 기본 객체에 저장된 모든 속성목록도 삭제

ㄴ. session 기본 객체 그 자체도 삭제

1.5 세션 유효시간

```xml
  <session-config>
  <session-timeout>30</session-timeout>
  </session-config>
```

<session-timeout>의 값을 0이나 음수로 설정하면 유효시간을 갖지  않는다.

session.invalidate()로 강제 종료해야 삭제.

따라서, 반드시 세션 타임아웃 시간을 지정해야주어야한다.

`redirect시에는 request객체가 유지되지 않으므로, session객체를 사용하는것이 적절하다.`

request.getSession()

```java
	***
	ㄱ. request.getSession() == request.getSession(true)
	 : 세션 객체가 없으면 생성해서 반환
	ㄴ. request.getSession(false) 
	 : 세션 객체가 없으면  null
         
    따라서, null 확인 여부를 위한 코딩은 아래가 되어야한다.     
	HttpSession session = request.getSession(false);
	 if (session!=null) { }
```
02 세션을 사용한 로그인 상태 유지 



03 연관된 정보 저장을 위한 클래스 작성 

하나의 세션에 여러 속성을 저장할때 발생할 수 있는 문제점을 줄이기 위해 클래스 사용

예를 들어, 로그인 여부 뿐만 아니라 회원의 등급 등의 정보를 저장할 수 있는데, 이러한 속성이 많아 질수록 setAtrribute 코딩을 반복해야 하는 문제점이 발생한다.

04 서블릿 컨텍스트와 세션 









[   ]

쿠키를 사용하는 로그인 상태관리

세션을 사용하는 로그인 상태관리 (서블릿이용)

톰캣 커넥션풀 사용/설정 ***

[	]

목,금 :MVC

다음주 : EL JSTL ~ 