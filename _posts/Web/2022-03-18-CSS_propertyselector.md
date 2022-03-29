---
layout: post
title: CSS 속성 선택자
date: 2022-03-18 00:00:00+0900
category: Web
published: true
---
# 특정 속성이 있는 요소를 선택하는 [속성] 선택자
예를들어 a 요소 중에서 href 속성이 있는 요소를 선택하려면 다음과 같이 작성함.  
```
a[href]{ ...... }
```

# 특정 속성값이 있는 요소를 선택ㅎ는 [속성=속성값] 선택자
[속성=속성값] 선택자는 주어진 속성과 속성값이 일치하는 요소를 찾아 스타일을 지정할 때 사용한다.  
이 형식은 대괄호([])안에 속성과 속성값을 넣고 그 사이에 '=' 기호를 표시함.   
예를 들어 a 요소 중에서 target 속성값이 '_blank'인 것만 선택하고 싶다면 다음과 같이 작성함.  
```html
a[target=_balnk]{......}
```

# 여러 값 중에서 특정 속성값이 포함된 속성 요소를 선택하는 [속성 ~=값]선택자 
[속성 ~= 값] 선택자는 여러 속성값 중에서 해당 속성값이 포함된 요소를 선택함.  
이 선택자는 속성이 하나면서 속성값이 여러 개일 때 특정 속성값을 찾는 데 편리함.   
예를 들어 하나의 요소에 클래스 스타일을 여러 개 적용할 수 있는데, 그중에 button 스타일이 있는 요소를 찾으려면 다음과 같이 함.  
```html
[class ~= button] { ...... }

<li><a href="#" class="button">메뉴 3</a></li>
<li><a href="#" class="flat button" >메뉴 4</a></li>
/* 아래 클래스는 flat button이지만 button을 포함하고 있으므로 적용됨. 즉 메뉴3 메뉴4 모두 적용됨*/
```

# 특정 속성값이 포함된 속성 요소를 선택하는 [속성 |=값] 선택자
[속성 |=값] 선택자는 특정 속성값이 포함된 속성에 스타일을 적용함.  
앞서 다룬 [속성~=값]선택자와 비슷해 보이지만, [속성~=값]은 하이픈(-)으로 연결한 단어에 스타일을 적용하지 않는다는 점에서
[속성|=값]선택자와 차이가 있다.  
즉, [속성|=값]선택자는 지정한 값과 정확하게 일치하거나 지정한 값을 포함해서 하이픈(-)으로 연결된 단어도 선택함.  
```html
a[title |= "us"] 
{  /* 속성값이 "us"이거나 "us-"로 시작하는 요소를 찾는 선택자 */
    background: url(images/us.png) no-repeat left center;
}

<li><a href="#" title="us-english">영어</a></li> /*속성값이 "us-"로 시작하는 한 단어이므로 스타일이 적용됨.*/
```
# 특정 속성값으로 시작하는 속성 요소를 선택하는 [속성 ^=값]
속성값이 정확하게 일치하지 않더라도 지정한 속성값으로 시작하는 요소를찾으려면 [속성^=값]선택자를 사용함.  
예를 들어 title 속성값이 eng로 시작하는 a 요소를 찾는다면 다음과 같이 작성함.  
```html
a[title ^= eng]{...}
```  

# 특정한 값으로 끝나는 속성의 요소를 선택하는 [속성 $= 값] 선택자
[속성^=값]이 지정한 속성값으로 시작하는요소를 선택했다면, [속성 $=값]선택자는 지정한 속성값으로 끝나는 요소를 선택함.  
예를 들어 링크한 파일 이름의 마지막 단어가 xls인 요소를 찾는다면 다음과 같이 작성함.  
```html
<style>
[href $= xls]{......}
```  
위는 href에 링크된 파일의 확장자, 즉 파일 이름의 마지막 속성값을 체크하는것임.  

```html
a[href$=hwp] { /* 연결한 파일의 확장자가 hwp인 링크 */
		background: url(images/hwp_icon.gif) center right no-repeat; /* 배경으로 hwp 아이콘 표시 */
		padding-right: 25px; /* 아이콘을 표시할 수 있도록 오른쪽에 25px 여백 */
	}

	a[href$=xls] { /* 연결한 파일의 확장자가 hwp인 링크 */
		background: url(images/excel_icon.gif) center right no-repeat; /* 배경으로 hwp 아이콘 표시 */
		padding-right: 25px; /* 아이콘을 표시할 수 있도록 오른쪽에 25px 여백 */
	}
</style>
</head>

<body>
	<h3>회사 소개 파일 다운 받기</h3>
	<ul>
		<li><a href="intro.hwp">hwp 파일</a></li>
		<li><a href="intro.xls">엑셀 파일</a></li>
	</ul>
</body>
```  

# 일부 속성값이 일치하는 요소를 선택하는 [속성 *= 값] 선택자
[속성 *= 값] 선택자는 속성값이 어느 위치에 있든지 지정한 속성값이 포함되어 있다면 해당 요소를 선택함.  
예시는 다음과 같다.  
```html
a[href *= "w3"] {  /* href 속성값 중에 w3가 있는 a 요소를 찾는 선택자 */ 
	 background:blue;
	 color:white;		 
	}
</style>
</head>

<body>
	<h1>HTML5 참고 사이트 </h1>
	<p>(아래 링크 중 파란색 배경의 링크는 W3C 사이트로 연결됩니다.)</p>
	<ul>
		<li><a href="https://html.spec.whatwg.org/">HTML 표준안 사이트</a></li>
		<li><a href="https://caniuse.com/">HTML 지원 여부 체크</a></li>
		<li><a href="https://www.w3.org/TR/css3-mediaqueries">미디어쿼리</a></li /*href의 속성값중에 "w3"가 일치하므로 스타일 적용*/
	</ul>
```

<br>
<br>
**지금까지 설명한것을 표로 정리하면 다음과 같다**  
![속성선택자표](\images\css\selector.png)