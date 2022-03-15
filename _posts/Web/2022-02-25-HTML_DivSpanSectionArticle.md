---
layout: post
title: HTML <div>,<span>,<article>,<section> 태그 차이
date: 2022-02-25 00:00:00+0900
category: Web
published: true
---
# &lt;article&gt; 태그
＜article＞요소는 내용이 각기 독립적이고,홀로 설 수 있는 내용을 담는다.  
주로 블로그 글, 뉴스 기사 등...
```html
<article>
    <h1>블록체인이란?</h1>
    <p>분산형 시스템...</p>
    ...
</article>
```

# &lt;section&gt; 태그
＜section＞ 요소는 서로 관계 있는 문서를 분리하는 역할을 함.  
주로, 문서를 다른 주제로 구분짓기 위해 사용됨  
```html
<section>
    <h1>HTML의 2번째 이야기</h1>
    <p>웹 문서를 만들때 ~~</p>
    ...
</section>
```

# &lt;div&gt; 태그와 &lt;span&gt; 태그
＜div＞는 의미적으로 관계가 없을때 주로 사용하고, 오직 내용을 묶는 역할이라고 보면 된다.
＜span＞과 비슷한 역할을 하는데 차이가 있다.  
1. ＜div＞는 줄바꿈이 되지만 ＜span＞태그는 옆으로 붙는다.  
2.  텍스트를 표현할 때 ＜div＞는 사각형 박스로 구역을 정하지만 ＜span＞은 문장 단위로 지정함.


```html
<!DOCTYPE HTML>
<html>
<head>
<meta charset="euc-kr">
<title>CSS 속성</title>
<style type="text/css">
	#div1 {
		background-color: #F9F249;
		padding: 10px;
	}
	#span1 {
		background-color: #36FFFF;
	}
</style> 
</head>
<body>
	<div id="div1">
		div 테스트  div 테스트  div 테스트  div 테스트  div 테스트  div 테스트  
        div 테스트  div 테스트  div 테스트  div 테스트  div 테스트  div 테스트  
        div 테스트  div 테스트  div 테스트  div 테스트  div 테스트  div 테스트  
	</div><br/>
	<span id="span1">
		span 테스트 span 테스트 span 테스트 span 테스트 span 테스트 span 테스트 
        span 테스트 span 테스트 span 테스트 span 테스트 span 테스트 span 테스트 
        span 테스트 span 테스트 span 테스트 span 테스트 span 테스트 span 테스트 
	</span>
</body>
</html>
```

<html>
<head>
<meta charset="euc-kr">
<title>CSS 속성</title>
<style type="text/css">
	#div1 {
		background-color: #F9F249;
		padding: 10px;
	}
	#span1 {
		background-color: #36FFFF;
	}
</style> 
</head>
<body>
	<div id="div1">
		div 테스트  div 테스트  div 테스트  div 테스트  div 테스트  div 테스트  
        div 테스트  div 테스트  div 테스트  div 테스트  div 테스트  div 테스트  
        div 테스트  div 테스트  div 테스트  div 테스트  div 테스트  div 테스트 
        div 테스트  div 테스트 
	</div><br/>
	<span id="span1">
		span 테스트 span 테스트 span 테스트 span 테스트 span 테스트 span 테스트 
        span 테스트 span 테스트 span 테스트 span 테스트 span 테스트 span 테스트 
        span 테스트 span 테스트 span 테스트 span 테스트 span 테스트 
	</span>
</body>
</html>

**위의 노란색은 div태그를 사용한 것이고 아래는 span태그를 사용한 것.**  
div는 박스 형태로 영역이 설정되고 그 안에 정렬됨. 그러나 span은 줄단위로 영역이 설정되기 때문에 배경색의 길이가 다름.  
그리고 div는 width, height 크기 지정이 가능하지만 span은 inline속성을 가지기 때문에 정해 줄 수 없다.  

#### ([article,section차이](https://aboooks.tistory.com/346) 해당 포스트를 참고함.)    
#### ([div span차이](https://mainia.tistory.com/3289) 해당 포스트를 참고함.)  