---
layout: post
title: CSS 웹 문서의 레이아웃 만들기
date: 2022-03-04 00:00:00+0900
category: Web
published: true
---

# 배치 방법 결정하는 display 속성 
display속성을 사용하면 블록 레벨 요소와 인라인 레벨 요소를 서로 바꿔서 사용할 수 있음.  
display속성은 주로 웹 문서의 내비게이션을 만들면서 메뉴 항목을 가로로 배치할 때 많이 사용하고, 이미지를 표 형태로 배치할 수도 있다.(웹사이트에서 내비게이션은 메뉴를 의미하며, ```<nav>```와 ```</nav>```태그로 묶어서 나타냄)  
자주 사용하는 속성은 다음과 같다.  
>
**[display 속성값(주로 쓰는)]**  
**- block:** 인라인 레벨 요소를 블록 레벨 요소로 만들음.  
**- inline:** 블록 레벨 요소를 인라인 레벨 요소로 만들음.  
**- inline-block:** 인라인 레벨 요소와 블록 레벨 요소의 속성을 모두 가지고 있으며 마진과 패딩을 지정할 수 있다.inline 엘리먼트처럼 전후 줄바꿈 없이 한 줄에 다른 엘리먼트들과 나란히 배치됩니다.   
**- none:** 해당 요소를 화면에 표시하지 않음.  

# 왼쪽이나 오른쪽으로 배치하는 float 속성
```<p>```태그처럼 문단의 왼쪽이나 오른쪽에 이미지를 나란히 표시해야 할때 사용.  
원래는 ```<p>```태그는 블록 레벨 요소이므로 이미지와 나란히 한 줄에 배치할 수 없지만 이럴 때 float속성을 사용하여 이미지를 표시하고 그 주변에 텍스트가 둘러싸도록 할 수 있다.  
>
**[float 속성값]**  
**left:** 해당 요소를 문서의 왼쪽에 배치함.  
**right:** 해당 요소를 문서의 오른쪽에 배치함.  
**none:** 좌우 어느 쪽에도 배치하지 않음. 기본값임.  

float속성은 웹 요소를 문서 위에 떠 있게 함. 여기서 '떠 있다'라는 의미는 요소가 왼쪽 구석이나 오른쪽 구석에 배치된다는 것을 말함.  
```html
/*사용예시*/
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>CSS float 속성</title>
  <style>
    img {
      float:left;  /* 왼쪽에 떠 있게 */
      margin-right:40px;
    }
    body{
        background-color:black
    }
  </style>
</head>
<body>
  <img src="images/tree.png">
   <p>Ex et adipisicing voluptate aliqua cupidatat nulla. Laboris est sint sit aliqua enim. Aute Lorem eu sint aute sunt proident. Do culpa consectetur elit duis laboris reprehenderit incididunt nulla. Irure exercitation tempor aliqua laboris cupidatat anim in non officia aliquip excepteur fugiat labore.</p>
   <p>Lorem ipsum reprehenderit adipisicing exercitation enim velit veniam incididunt sit consectetur elit exercitation. Commodo veniam sit quis nisi ea. Ipsum do aliqua nostrud laboris elit duis adipisicing id Lorem qui. Labore dolor ipsum enim incididunt. Velit qui cillum sunt labore incididunt duis aute Lorem nulla et. Sint commodo aute amet laboris ullamco exercitation Lorem dolore veniam ut reprehenderit incididunt. Laborum nulla eiusmod cillum irure anim aute.</p>
   <p>Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.</p>
   <p>Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.</p>
   <p>Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.</p>
   <p>Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.</p>
   <p>Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.</p>
   <p>Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.</p>
   <p>Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.Excepteur volup.</p>
</body>
</html>
```
![float예시](\images\css\float.png)  
이런식으로 나오게 된다.

# float속성을 해제하는 clear 속성
float 속성을 사용해 웹의 요소를 왼쪽이나 오른쪽에 배치하면 그다음에 넣는 다른 요소에도 똑같은 속성이 전달됨.(붙게 된다는 뜻)  
따라서 float 속성이 더 이상 유용하지 않다고 알려주는 속성이 필요한데, 그것이 따로 clear 속성이다.  
>
**[clear 속성값]**  
**left:** float: left를 해제함.  
**right:** float: right를 해제함.  
**both:** float: left와 float: right를 해제함.  

---
>
**display: inline-block과 float:left속성은 어떻게 다른가?**  
결과 화면은 똑같지만 차이가 있다.  
display:inline-block은 가로로 배치하면서도 기본 마진과 패딩을 가지고 있지만, float:left로 배치하면 가로로 배치될 때 요소에 기본 마진과 패딩이 없다.  
그래서 필요하다면 요소마다 마진과 패딩을 지정해야함. 그리고 float: left를 사용하면 clear 속성으로 플로팅을 해제해야 함.  


