---
layout: post
title: CSS 웹 요소의 위치 지정하기
date: 2022-03-06 00:00:00+0900
category: Web
published: true
---
# 웹 요소의 위치를 정하는 left,right,top,bottom 속성
position 속성으로 기준 위치를 정한 뒤 요소의 위치를 left, right, top, bottom 속성에서 선택하고 속성값을 지정하면 됨.   
>
**[left, right, top, bottom 속성]**  
**left:** 기준 위치와 요소 사이에 왼쪽으로 얼마나 떨어져 있는지 지정  
**right:** 기준 위치와 요소 사이에 오른쪽으로 얼마나 떨어져 있는지 지정  
**top:** 기준 위치와 요소 사이에 위쪽으로 얼마나 떨어져 있는지 지정  
**bottom:** 기준 위치와 요소 사이에 아래쪽으로 얼마나 떨어져 있는지 지정


# 배치 방법을 지정하는 position 속성  
position 속성은 웹 문서 안의 요소를 자유자재로 배치해 주므로 HTML과 CSS를 이용해 웹 문서를 만들 때 중요함.  
텍스트나 이미지 요소를 나란히 배치할 수도 있고 원하는 위치를 선택할 수도 있다.   
>
**[position 속성값]**  
**static:** 문서의 흐름에 맞춰 배치함. 기본값  
**relative:** 위칫값을 지정할 수 있다는 점을 제외하면 static과 같다.  
**absolute:** relative값을 사용한 상위 요소를 기준으로 위치를 지정해 배치함.  
**fixed:** 브라우저 창을 기준으로 위치를 지정해 배치함.  


```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>CSS position 속성</title>
  <style>
    p {
      width:500px;
      height:200px;
      background-color:#eee;
      border:1px solid #ccc;
      line-height:2;
    }
    #static {
      position:static;
    }
    #relative-1{
      position:relative;
    }
    #relative-2 {
      position:relative;   /* 포지셔닝 - relative */
      left:300px;  /* 왼쪽에서 100px 떨어지게 */
      top:-50px;   /* 위쪽에서 -50px 떨어지게 (위로 이동) */
    }
    #fixed {
      width:100px;
      height:100px;
      background-color:#222;
      position:fixed;  /* 포지셔닝 - fixed */
      right:30px;  /* 오른쪽에서 30px 떨어지게 */
      top:10px;  /* 위쪽에서 30px 떨어지게 */
    }
  </style>
</head>
<body>
   <p id="static">Ex et adipisicing voluptate aliqua cupidatat nulla. Laboris est sint sit aliqua enim. Aute Lorem eu sint aute sunt proident. Do culpa consectetur elit duis laboris reprehenderit incididunt nulla. Pariatur fugiat voluptate ea non amet cupidatat. </p>
   <p id="relative-1">Lorem ipsum reprehenderit adipisicing exercitation enim velit veniam incididunt sit consectetur elit exercitation. Magna Lorem excepteur occaecat cupidatat sunt proident tempor do nostrud labore cillum non exercitation voluptate. </p>
   <p id="relative-2">Excepteur voluptate ad irure ipsum duis. Deserunt cupidatat commodo proident eu mollit cillum commodo quis quis et ad. Velit id duis enim reprehenderit eu dolor Lorem excepteur excepteur. </p>
   <p id="fixed"></p>
</body>
</html>
```