---
layout:     post
title:      WebClass-days02-JavaScript
date:       2019-04-09 23:00:00
summary:    이벤트 처리 / 문자열 함수 / 숫자 함수
categories: JavaScript
---

###### js에서의 이벤트 처리

1. 
`<em onXXX="js 코딩, 함수"></em>`

2.  onclick = javascript 
`document.getElementById("btn2").onclick=function(){alert("무명메서드")};`
3. EventListener 사용
- 형식
element.addEventListener(event,function,useCapture);
이벤트 유형 : click / 2. 함수 / 3. 이벤트 버블링 or 캡처를 사용할 지 여부 boolean
- 예시
document.getElementById("btn3").addEventListener("click", function(){alert("동적으로 등록된 2번째 함수")});
document.getElementById("btn3").removeEventListener("click", test );

- 
IE 8.0 이전에는 사용 X
element.addEventListener /removeEventListener
IE 8.0 이전에는 사용 O
element.attachEvent()
element.detachEvent() 

- 호환성을 고려한 코딩 (8.0 이전, 이후 모두)
if (btn.addEventListener) {
	btn.addEventListener("click",test)	
}else {
	btn.attachEvent("onclick",test)
}

- 이벤트 전파
이벤트 버블링 : false: in(자식) -> out(부모)
이벤트 캡처링 : true : out(부모) -> in(자식) 

###### js 의 문자열 관련 함수

~기본사항~
- 
		//' '   , " " 
		var x = "hello 'World!' ";
		var x = 'hello "World!" ';
		// 문자열 길이
		document.write(x.length);
		// 제어문자 사용가능 \n \t
		var x = "hello \"world\" ";
		var x = 'hello\n World! ';
		alert(x);
		//
		var name1 = "admin"; // string
		var name2 = new String("admin");//object
		// 문자열 의 값 비교 : 같다
		if (name1 == name2)
			alert("같다");
		else
			alert("다르다");
		// 문자열의 값 & 타입 비교 : 다르다
		if (name1 === name2)
			alert("같다");
		else
			alert("다르다");
		// js 객체 비교 -- 항상 false
		var name3 = new String("admin"); //object
		alert(name2 == name3); //false
		alert(name2 === name3); //false

~관련함수~
- indexOf
- String.fromCharCode
- toUpperCase() / toLowerCase()
- concat( , )
- trim()
- charAt() / charCodeAt()
- split
- toString()				
		number.toString( ) : 숫자 -> 문자
		number.toString(n) : 10진수 숫자 -> n진수 숫자

###### js의 숫자 관련 함수

- 
0x : 16진수
var n = 0xFF; // 255
0 : 8진수
var n = 010; // 8

- Number()
Number( new Date() )
: 1970년 1월 1일부터 카운팅한 ms값<br>
Number.MAX_VALUE/ MIN_VALUE

- parseInt(), parseFloat()
- eval()
- toPrecision(n)
: n 길이로 문자열 반환

- toFixed 
: return 타입이  string

- toExponencial
