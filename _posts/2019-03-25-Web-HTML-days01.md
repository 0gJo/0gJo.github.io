---
layout:     post
title:      WebClass day01 HTML
date:       2019-03-25 20:40:00
summary:    HTML이란? / 기본 문법
categories: HTML
---
### 웹환경 이해
URL에 ip, port 정보 모두 포함되어있음..
| 웹서버 | WAS     |
|-------|---------|
| 아파치 |톰캣 8.5.X|

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;default.html

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;???.jsp -> ???.class : 톰캣의 역할
             
  
Server ip를 보통 호스팅해주는 업체를 사용.. 

http는 기본적으로 80 포트사용하므로 URL에는 안나타남 

지금은 톰캣 SERVER 를 이클립스에 꽂아놨으므로..
Eclipse 실행할때만 톰캣서버가 작동함.. 끄면 x

http://[211.63.89.163 : 도메인 사서.. www.naver.com]


-------------------------------------------
### HTML 
Hyper Text Markup Language
Hyper : 시공간 초월하는
Markup : 문서의 논리적 구조와 배치양식에 대한 정보를 표현하는 언어
==> HTML은 "웹페이지"의 구조와 배치양식에 대한 정보를 표현하는 언어

html의 요소(element) : 시작태그 ~ 종료태그

``<title> HTML CLASS </title>``

[시작태그 	   Content      종료태그] =>

*****Element(요소) : 안에있는거 모두포함

브라우저가 parsing (rendering)한다

#####*html 구조(기본형식)
- ``<!DOCTYPE html>`` : HTML5 (소문자사용권장)

  '대소문자 구분안하는 HTML5 버전을 따르는 문서이다' 라고  선언한 것.
 - ! : 선언문
 -  DOCTYPE : 대소문자 구분x

- root element 인 ``<html>``
- 								``<head>``
- 필수 							``<body>  [	이 내용만 browser에 출력] </body>``
  
---------------> 여기까지가 기본.. 

[](http://koxo.com/)

``<br></br> == <br /> == <br>``

xhtml&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;html5


##### 예제코드
{% highlight html %}
<!DOCTYPE html>
<html> <!-- 주석처리 -->
	<head> <!--  Contains metadata and window title information for the document-->
	<meta charset="UTF-8"> <!--Defines metadata information for the document  -->
	<title>ex02.html</title> <!-- The document title, displayed in the browser's title bar -->
	</head>
<body> <!--The document body. Contains all the content for the page. -->
<!-- space하든, tab하든 enter하든 웹페이지 화면상에는 모두 공백 1칸-->
<!-- html의 예약문자는 [문자엔티티(개체)]로 대체된다
사용 :    &엔티티이름;
&nbsp; == non breaking sapce == 공백( space )
  -->
 김길환 &nbsp;함치영&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;          조영지<br><!-- Enter : Forces a line [br]eak -->
임재민&nbsp;&nbsp;&nbsp;	진동현
<br>
</body>
</html>
{% endhighlight %}