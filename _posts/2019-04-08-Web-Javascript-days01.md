---
layout:     post
title:      WebClass-days01-JavaScript
date:       2019-04-08 23:00:00
summary:    js 기본 / 변수, 함수, 데이터타입, 객체
categories: JavaScript
---
#### js 변수, 함수, 데이터타입, 객체

###### 변수(variable)
<small>
- 형식 : [ var ] 변수명
- 종류 : 전역변수 / 지역변수
- var를 붙이나 안붙이나 상관없으나,
(붙이는 것을 권장)
if문이나,function의 {}블럭에서
{ var n // 지역변수}
{     n  // 전역변수}

</small>



###### js의 데이터타입(data type)
1. string
2. number
3. boolean
4. function
5. object


###### js의 객체 (클래스)
1. Object
2. Date
3. Array
4. String
5. Number
6. Boolean

###### 함수(function)
- data type 1종 류

- 함수 : 반복적인 코딩 + 재사용 + 코드블럭

- 형식
`[var] 변수명;
   function 함수명([파명, 매명...]){  ㅍ//인자, 인수  - 지역변수
	   
	   [return 리턴값;]
   } 
`



- 사용
1) 이벤트 처리    onclick="함수명();"
   2) js  코드에서 함수 호출
   3) 자동 함수 호출


###### js 객체 
java에서의 객체 
: 클래스를 자료형으로 선언된 참조 변수
Class Student{
//fields

//methods

}
생성
Student s1 = new Student();
호출
s1.name = "홍길동";
s1.method();

js 에서의 객체 
- 생성 + 초기화
 멤버변수명 : 값
var s1 = {
		name : "홍길동'
        , age : 12
        , toString : function(){
		return this.name+"/"+this.age;
        }
}

- 호출
s1.name;
s1.toString();



- - -
#### js 기본

javascript
script : 클라이언트 단에서 사용되는 웹 언어 (서버에서 실행되지 x)
            '브라우저'가 언어를 시행
ㄱ. html 내용을 동적으로 변경할 수 있다.
ㄴ. html 속성값을 변경할 수 있다.
ㄷ. html 스타일(css)을 변경할 수 있다.
ㄹ. html 요소를 숨길 / 표시 할 수 도 있다.
등등..


- type 속성은 필수가 아니다 (html 의 유일한 스크립트 언어 = javascript)

- javascript 함수 + 이벤트
<- 
호출
function 함수명 ( 	){

}

- 일반적으로 head 태그 or body 태그안에 선언
( ready로 로딩 )   ( 로딩 후 ) 
( but, 어디있어도 상관 없음 )

외부 js 파일 - 해당 페이지 뿐만 아니라, 공통적으로 적용할 스크립트 코딩.. 

- `<script src="/ex01.js"></script>`
: 여러개 있어도 상관없다.
- 장점
ㄱ. html과 js 코드 분리 -> 유지, 보수 용이
ㄴ. 캐시(메모리에 로드)된 javascript 파일로 인해 처리 성능 향상


- 디버깅 - F12 ***



- js에서 문자열 -> " ", ' ' 둘다 가능
( html과 js에서 겹치지 않도록 혼용..)

- 
event : 이벤트가 발생할때 자동생성되는 객체
window : 최상위 객체 , 생략가능



- js로 data 출력하는 방법
1 innerText, innerHTML : html 요소에 출력
2 document.write() :html 출력
3 window.alert() 		경고창 출력( 디버깅용도)
4 console.log()        f12 console 창에 출력 (디버깅용도)








