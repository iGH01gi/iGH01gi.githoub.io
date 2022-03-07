---
layout: post
title: CSS 배경관련
date: 2022-03-07 00:00:00+0900
category: Web
published: true
---
# 배경색을 지정하는 background-color 속성
background-color에는 16진수나 rgb값 또는 색상 이름을 사용해서 지정함.  
색상을 세밀히 조절하고 싶다면 16진숫값을, 투명도도 함께 조절하고 싶다면 rgba표기법을 사용함.  
```html
background-color: #008000;
background-color: rgb(0,128,0);
background-color: green;
```
스타일 상속에 따르면 글꼴이나 글자 크기 등은 ```<body>```태그 선택자에서지정하면 문서 전체에 상속됐음.  
하지만 예외로 background-color값은 상속되지 않음.  
기본적으로 모든 웹 문서 요소의 배경은 투명하므로 body 스타일로 지정한 문서 배경이 그대로 비치는 것일 뿐 웹 요소에 배경색이 상속된 것은 아님.  

# 배경색의 적용 범위를 조절하는 background-clip 속성
박스 모델 관점에서 배경의 적용 범위를 조절할 수도 있다.  
즉, 박스 모델의 가장 외곽인 테두리까지 적용할지, 테두리를 빼고 패딩 범위까지 적용할지, 아니면 내용 부분에만 적용할지 선택할 수 있다.  
>
**[background-clip의 속성값]**  
**border-box:** 박스 모델의 가장 외곽인 테두리까지 적용함. 기본값임.  
**padding-box:** 박스 모델에서 테두리를 뺀 패딩 범위까지 적용함.  
**content-box:** 박스 모델에서 내용(콘텐츠) 부분에만 적용함.  

