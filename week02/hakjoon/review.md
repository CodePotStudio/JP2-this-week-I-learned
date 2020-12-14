# 이번주 리뷰
<br>

## 공부하기 귀찮은 CSS 뿌시기
###diplay & cascading
* display <br>
block <br>
Inline : 1. 인라인의 경우 width, height 값이 적용 되지 않는다.<br>2. text를 쓸떄 사용한다.
<br>
Inline-block : block 형식으로 정확한 높이 값이나 너비값을 적용하고 싶을 때 사용
<br> 인라인 블락의 경우 카드들 세로로 정렬 등에 사용된다.
* cascading <br>
우선순위 : Inline sheet > ID 값 > class 값 > tag sheet
###reset.css
* 브라우저 마다 default로 설정되어있는 스타일들이 있음.<br>
 내가 적용한 style과 충돌나는경우 존재 따라서 초기화 시켜주는 css 파일이 존재한다.
```css
/* http://meyerweb.com/eric/tools/css/reset/ 
   v2.0 | 20110126
   License: none (public domain)
*/

html, body, div, span, applet, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,
del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,
b, u, i, center,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, embed, 
figure, figcaption, footer, header, hgroup, 
menu, nav, output, ruby, section, summary,
time, mark, audio, video {
	margin: 0;
	padding: 0;
	border: 0;
	font-size: 100%;
	font: inherit;
	vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article, aside, details, figcaption, figure, 
footer, header, hgroup, menu, nav, section {
	display: block;
}
body {
	line-height: 1;
}
ol, ul {
	list-style: none;
}
blockquote, q {
	quotes: none;
}
blockquote:before, blockquote:after,
q:before, q:after {
	content: '';
	content: none;
}
table {
	border-collapse: collapse;
	border-spacing: 0;
}
```

###box model
* margin <br>
margin은 두 item에 대한 margin top bottom이 중복돼서 적용되지 않고 max값이 적용된다.
* padding <br>
테두리 안쪽에서 item간의 top bottom left right 간격

###postion
* static : 기본값
* Relative : 자기 자신을 기준으로
* Absolute : 부모 요소를 기준으로
* Fixed : 뷰포트를 기준으로 <br>
각 content를 위 설정에서 하나 골라 세팅하고 Top, Bottom, Left, Bottom을 통해 테두리에서 세팅한다.
<br>
웹에서 각 item들의 배치에 자유도를 부여할 수 있다.
<br>
postion.fixed를 통해 상단 바 고정 or 하단 바 top 버튼 고정 등 활용
<br>
relative , absolute의 부모, 자식 관계를 활용하여 각 요소들에 대한 위치 세팅을 고려한다.
# 튜터에게 궁금한 점

