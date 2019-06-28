## Chapter16. 스프링 시큐리티

### 요약 

* 웹사이트에서의 스프링 시큐리티의 활용

스프링에서의 로그인 처리 (인증)과 권한 (관리자,일반유저, 사장님 등)은 스프링 시큐리티 모듈을 통해 쉽게 기능을 구현할 수 있다.

인증과 관련된 기능의 예시로는, 사용자가 로그인 버튼을 눌렀을때 회원인지 확인 후 브라우저를 종료할떄 까지 회원정보를 유지하는 기능이 있다.

또한, 웹사이트의 일부 기능에 대한 접근을 회원의 권한에 따라 막을 수 도 있다.

* 방법

1. Spring Security  관련 모듈을 추가한다 (pom.xml에)

spring-security-web / spring-security-config / spring-security-taglibs

cf. taglibs 는 security관련 유용한 태그들을 jsp 페이지에서 쉽게 사용하기 위한 것이므로, 필수는 아니다.

2. ~페이지 요청할 때 ~ 권한 있는지 확인할 것이다  + 요청 id의 권한을 찾아올 user-service는 ~다

   라고 정의한 security 관련 xml 파일을 만든 후 web.xml에 참조 시킨다 (서버 작동할 때 읽을 수 있도록 )

   ( + security xml 파일에서 ~페이지 요청할 때 ~ 권한 있는지 확인할 것이다  코딩 (http태그)을 할때 로그인, 로그아웃 UI와 에러 응답 설정을 변경할 수도 있다 p.705 )

   cf. jdbc-user 코딩에서,  DB에 username, password, enabled 컬럼을 가진 사용자 테이블과 권한 관련 테이블이 있어야 한다. ( 스프링 시큐리티가 요구하는 사항을 만족해야 함. 다를 시는 아래의 내용 참고)

3. jsp 페이지 에서 인증 여부와 권한에 따라 기능을 제한하는 코딩을 한다. 

* 코드

1. pom.xml

```xml
		<!-- 스프링 시큐리티 3개 p656 -->
		<dependency>
		<groupId>org.springframework.security</groupId>
		<artifactId>spring-security-web</artifactId>
		<version>3.2.4.RELEASE</version>
		</dependency>
		
		<dependency>
		<groupId>org.springframework.security</groupId>
		<artifactId>spring-security-config</artifactId>
		<version>3.2.4.RELEASE</version>
		</dependency>
	
		<!-- 로그인 사용자의 정보등을 알 수있는 tag들을 사용하기 위해 추가한 lib -->
		<dependency>
		<groupId>org.springframework.security</groupId>
		<artifactId>spring-security-taglibs</artifactId>
		<version>3.2.4.RELEASE</version>
		</dependency>
```



2. security 관련 xml

```xml
<http>
<form-login login-page="/joinus/login.htm"
				 authentication-failure-url="/joinus/login.htm?login_error"		
				 default-target-url="/customer/notice.htm"/> 
<logout logout-success-url="/customer/notice.htm"/>
    
    
<intercept-url pattern="/customer/noticeDetail.htm" access="ROLE_USER"/>
<intercept-url pattern="/customer/noticeReg.htm" access="ROLE_USER"/>
<intercept-url pattern="/customer/noticeEdit.htm" access="ROLE_ADMIN"/>
</http>

 <authentication-manager>
     <authentication-provider>
        <jdbc-user-service 
             data-source-ref="dataSource"
             users-by-username-query=
               "select  id as username, pwd as password, 1 as  enabled  from member where id = ?"
             authorities-by-username-query="select id  as username, case when id='admin' then 'ROLE_ADMIN'   else   'ROLE_USER' end   as authority from member where id = ?"  
        />
     </authentication-provider>
   </authentication-manager>

```



3.  인증과 권한을 활용하는 jsp 페이지(권한에 따라 기능 접근을 제한)

* header.jsp -- 인증

```jsp
<s:authorize ifNotGranted="ROLE_USER">
			<li><a href="${ pageContext.request.contextPath }/joinus/login.htm">로그인</a></li>
</s:authorize>
<s:authorize ifAnyGranted="ROLE_USER,ROLE_ADMIN">
			<li><a href="${ pageContext.request.contextPath }/j_spring_security_logout">
		<!-- 인증받은 계정명 이름 가져오기 -->
			[<s:authentication property="name"  var="loginUser"/>${loginUser}]
		
			로그아웃</a>
</s:authorize>			
```

* notice.jsp -- 권한

```jsp
<s:authorize ifAnyGranted="ROLE_ADMIN,ROLE_USER">
		<a class="btn-write button" href="noticeReg.htm">글쓰기</a>
</s:authorize>
```



--------------------------------------------------------------------

### 수업 내용   

1. pom.xml에 security 관련 모듈 추가 (프레임웍과 차이가 안나는 버전으로 하는 것이 좋다 )
2. web-inf - spring 폴더에 xml 관련 파일들이 위치하도록 변경및 설정 변경(web.xml init 파람으로 servlet-context 읽을 수있도록) ( 스프링 자체의 xml 관련 구조가 따로 존재하므로 맞춰주기)

( root-context의 역할 ==dispatcher-service 와 동일 )

( servlet-context의 역할 ==dispatcher-servlet 와 동일 )

3. (src/main/resources 에)  security 설정 xml을 시킨다.( classpath:// == src/main/resources) -> 후 web.xml에서 인식하도록 설정

![security](C:\Users\sist\Desktop\Spring 수업\security.PNG)

생성할때 위의 방식을 사용하면 

```xml
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xmlns:security="http://www.springframework.org/schema/security"
xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
	http://www.springframework.org/schema/security http://www.springframework.org/schema/security/spring-security.xsd" 
```
과 같은 설정을 하나하나 하지 않아도 된다.



요구사항)

notice.htm -> 인증 x 모두가 사용가능    

noticeDetail.htm -> 인증 O    

noticeEdit, noticeReg -> 관리자만 (인가)    



이러한 요구사항을 security xml에 설정한다.    



security xml 설명

\<security:http>
 : 인증 , 인가(권한) 관련 설정 태그

pattern 속성 : 권한 , 인증이 필요한 페이지 등록

access 속성 : 권한을 가진 롤을 등록 (롤의 이름은 사용자가 정한다)

```xml
<http>
<form-login login-page="/joinus/login.htm"/> 
<intercept-url pattern="/customer/noticeDetail.htm" access="ROLE_USER"/>
<intercept-url pattern="/customer/noticeReg.htm" access="ROLE_ADMIN"/>
<intercept-url pattern="/customer/noticeEdit.htm" access="ROLE_ADMIN"/>
</http>
```

spring에서 maven 구조를 사용하려면 spring이 3.2.5이상 이어야한다

스프링은 가상계정으로 인증과 인가를 확인할 수 있는 기능을 제공한다 

4. web.xml에 로그인 필터 설정  p661

05 상황별 스프링 시큐리티 설정

5.1 일부 경로 스프링 시큐리티 적용 안하기

<u>5.2 DB를 이용한 인증 처리</u> 

5.3DB를 이용한 인증 처리 구조

5.4비밀번호 암호화 처리

<u>5.5로그인로그아웃UI/에러 응답 설정 변경</u>

5.6HTTPS 및 포트 매핑 설정하기

5.7세션 대신 쿠키 사용하기



p.706 로그인 폼 관련 속성

로그인 요청을 전송하고 처리 할수 있도록 표를 참고하여 \<form-login> 의 속성 설정

( login.jsp 도 요청 제대로 되도록 변경 )

로그인에 성공했다면 로그인->로그아웃 / ~님 환영합니다 메시지를 출력해야한다

header.jsp

방법 1 로그인한 사용자의 정보는 userPrincipal 객체에서 확인 할 수 있다.

방법 2 스프링 시큐리티 태그라이브러리 사용 

```jsp
<s:authorize ifNotGranted="ROLE_USER">
			<li><a href="${ pageContext.request.contextPath }/joinus/login.htm">로그인</a></li>
</s:authorize>
<s:authorize ifAnyGranted="ROLE_USER,ROLE_ADMIN">
			<li><a href="${ pageContext.request.contextPath }/j_spring_security_logout">
		<!-- 인증받은 계정명 이름 가져오기 -->
			[<s:authentication property="name"  var="loginUser"/>${loginUser}]
		
			로그아웃</a>
</s:authorize>			
```



글쓰기 수정 권한도 notice.jsp에서 수정 



로그인한 user로 insert되도록



컨트롤러에서 사용자 정보가져오는 방법

방법 1 

```java
		UserDetails user =
				(UserDetails) SecurityContextHolder.getContext().getAuthentication().getPrincipal();
			notice.setWriter(user.getUsername());
		
```

방법2

```java
public String noticeReg(  Notice notice , HttpServletRequest request, Principal principal) {
    ...
String username = principal.getName();
}

```



DB에서 확인해서 member 확인하는 작업..

5.2 DB를 이용한 인증 처리 

(1) 사용자 및 권한 매핑 DB테이블 설정

반드시 컬럼명 username, password, enabled ---> 다를시 alias 사용

(2) 스프링 시큐리티 설정 (security xml)

 p693**** 

```xml
 <authentication-manager>
     <authentication-provider>
        <jdbc-user-service 
             data-source-ref="dataSource"
             users-by-username-query=
               "select  id as username, pwd as password, 1 as  enabled  from member where id = ?"
             authorities-by-username-query="select id  as username, case when id='admin' then 'ROLE_ADMIN'   else   'ROLE_USER' end   as authority from member where id = ?"  
        />
     </authentication-provider>
   </authentication-manager>
```

(3) 데이터 준비 및 스프링 MVC 설정

mvc xml 설정 후 web.xml에 참조시키기 (dispatcher Servlet 생성될때 참조하도로 init param으로)

(4) 사용자 권한에 따라 다른 내용을 보여주는 JSP 코드 예제

(5) DB를 이용한 인증 처리 확인





오후 : 웹소켓 채팅

다음주.. 오전수업 :  myBatis + 리눅스 

​				오후수업 : 과제 + 프로젝트 

