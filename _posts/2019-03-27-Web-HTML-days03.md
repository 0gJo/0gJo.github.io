---
layout:     post
title:      WebClass day03 HTML
date:       2019-03-27 22:45:00
summary:    링크 / 테이블 / 리스트 / iframe / form  
categories: HTML
---

##### <xmp><a></a> 링크  - 인라인모드 (in-line)</xmp>


링크의 상태에 따른 style 적용 (css)
:link
:visited
:hover
:active


{% highlight html %}
a{
	color :  ;
	text-decoration: ;
	display : inline-block;
	width: 100px;    /*a태그는 인라인 모드 이므로 width 속성x  */
{% endhighlight %}
}


-----------------
##### <xmp><table></table> 테이블</xmp>
- 테이블 제목
- 컬럼 제목
- 내용
- foot 
- 셀병합
{% highlight html %}
table {
	margin: 0 auto; /*==가운데정렬 */
	/*위 오른쪽 아래 왼쪽 여백*/
	border-collapse: collapse; /* 붕괴하다 : 1줄 선 */
}
{% endhighlight %}


{% highlight html %}
tr:nth-child(even) {
tbody td { /*tbody 의 자식 td 에게만.. */

div#demo

#teamlayout{

.team04 {
.manager {

table, tr, td{
	margin:0;
	padding: 0;
}

ul#nav li a.active {
ul#nav li a:hover:not(.active){

{% endhighlight %}


-------------------------------------------------------------------

position: fixed; /*위로 뜬것.. Z좌표축 생긴것.. */

--------------------------------------------------------------------
##### 리스트 - 블록모드 (block)
{% highlight html %}
<ul>
<li></li>
</ul>
<ol></ol>
{% endhighlight %}
- type 속성이나 style 속성으로 리스트 모양(type)변경

{% highlight html %}
li {
	float: left; /*블럭모드 를 해당방향으로부터 float 인라인모드 */
}
{% endhighlight %}

-------------------------------------------------------------------------------
##### iframe 
- 웹페이지내의 웹페이지 (창안의 창)
- <xmp><iframe></iframe></xmp>
- src 속성값이 없으면 빈프레임

예제1
{% highlight html %}
<iframe src="http://trio.co.kr/club/public/clock.html" width="108" height="16" 
frameborder="0"
 scrolling="no"
 style="border: solid 2px gray;"></iframe>
{% endhighlight %}

예제2
{% highlight html %}
<a href="http://www.sist.co.kr" target="content">sist</a><br>
<a href="https://www.naver.com" target="content">naver</a><br>
<a href="https://www.google.com" target="content">google</a><br>


<iframe name="content" width="100%" height="200px"></iframe>
{% endhighlight %}

--------------------------------------------------------------------------------
##### form 태그
- input태그를 감싸는 태그 (클라이언트로부터 입력받(input태그)은 정보를 서버로 전달하는 역할)
`
<form method=  action= > </form>

 <input type=submit>
`
-   서버로 전송하기위해서는 type이 submit으로 설정되어야(?)
- 클라이언트로부터 정보를 전송받으면 서버에서는 action에 해당하는 .jsp를 수행하고 다시 그 결과를 html로 (WAS의 역할?) 클라이언트에게 전송







{% highlight html %}
<table>
<caption></caption> : 제목

<thead>	 : 테이블 제목  
	<tr>
	<td></td>
	<td></td>
	</tr>
</thead>	

<tbody> : 내용 테이블 
	<tr>
	<td></td>
	<td></td>
	</tr>
</tbody>

<tfoot> : 마지막
	<tr>
	<td></td>
	<td></td>
	</tr>
</tfoot>

</table>
{% endhighlight %}