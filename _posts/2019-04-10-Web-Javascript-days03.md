---
layout:     post
title:      WebClass-days03-JavaScript
date:       2019-04-10 23:00:00
summary:    배열 객체 / 날짜 객체
categories: JavaScript
---
이벤트 발생순서 **

down - press - up
						length
rrn7_keydown() 0
rrn7_keypress() 0
rrn7_keyup() 1

ex02 js 배열
-  배열크기 필요 x
- push , pop 
- shift : 0번째 요소를 제거하고 1번째~ 요소  -1 위치 이동 / 리턴 값 :첫번쨰
 <-> unshift : 새로운 변수를 0번째에 추가하고 한칸씩 +1 밀기 / 리턴 값 : 배열크기
 
 slice
 
 ex08.html 
 
-  sum() 
 
-  arguments 컬렉션 
: 현재 실행 중인 기능함수와 그 기능함수를 호출한 기능함수에 대한 인수를 나타내는 개체이다.
: 전달되는 인자값을 담고있는 객체 ( 함수 매개변수 정의 부분에 선언할 필요 x)

- options 컬렉션 
--------
ex09 - js 날짜, 시간 (내장객체)
 Date 
- month - 1.. 
- milliseconds <-> date ***
<- parse
-> new Date()
					


					

[		]

ex08 eventListener...
// 동적 코딩 으로  option (태그) 만들기
// 선택된 option (색상) 으로 배경색 바꾸기



ex12  연도, 월에 맞춰서 date 채워넣기 
onchange.. 


ex01 rrn  *
배열
ex02 잘라내기 + 오름차순 정렬 -> p 태그에 출력..
.split / .sort  / .join
ex03
배열 요소 추가
push, pop, delete , unshift, shift
//delete points[1];
//points.splice(pos, amount, newelt)
두배열을 병합 : concat()
배열 자르기 (필요한 portion 가져오기..) : slice 
//slice(start, end ) : end - 1 위치값 까지 

ex05 
배열 정렬(sort) - 내림차순,..특정기준.. 
	 Max, Min - Math.max.apply(null, m)
	6
배열명.filter()
  var n = m.filter(  function (value, index, array){
	   return value > 30;
  } );
	7
m.forEach( function(항목값, 항목첨자값, 배열자체 ) { })

Array.map() : 배열의 각 요소에 대해 처리하는 함수 
					 ["새 배열 반환"]
 m.map(function(value, index, array)