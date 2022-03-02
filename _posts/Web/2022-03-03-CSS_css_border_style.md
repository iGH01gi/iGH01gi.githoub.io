---
layout: post
title: CSS 테두리 스타일 지정하기
date: 2022-03-03 00:00:00+0900
category: Web
published: true
---
# 박스 모델의 방향 살펴보기 
박스 모델의 방향의 순서는  **top->right->bottom->left**  

# 테두리 스타일을 지정하는 border-style 속성 
border-style 속성의 기본값은 none이므로 속성값을 따로 지정하지 않으면 테두리 색상이나 두께를 지정하더라도 화면에 표시되지 않음.  
>
**border-style 속성값**  
**none:** 테두리가 없음. 기본값  
**hidden:** 테두리를 감춤. 표에서 border-collapse일 경우 다른 테두리도 표시되지 않음.  
**solid:** 실선 테두리  
**dotted:** 점선 테두리  
**dashed:** 짧은 직선 테두리(점선)  
**double:** 테두리를 이중선으로 표시. 두 선 사이의 간격이 border-width값임.  
**groove:** 테두리를 창에 조각한 것처럼 표시. 홈이 파인 듯 입체 느낌이 남.  
**inset:** 표에서 border-collapse: seperate일 경우 전체 박스 테두리가 창에 박혀 있는 것처럼 표시되고, 표에서 border-collapse: collapse일 경우 groove와 똑같이 표시됨.  
**outset:** 표에서 border-collapse: seperate일 경우 전체 박스 테두리가 창에서 튀어나온 것처럼 표시되고, 표에서 border-collapse: collapse일 경우 ridge와 똑같이 표시됨.  
**ridge:** 테두리를 창에서 튀어나온 것처럼 표시함.  

```html
<style>
		div {
			width:200px;
			height:100px;
			display:inline-block;
			margin:15px;	
			text-align: center;
			font-size:20px;
			line-height:100px;		
			border-width:5px;  /* 테두리 굵기 */
		}
		#box1 { border-style:solid; }  /* 실선 */  
        /*만일 테두리 스타일을 4개 방향 모두 다르게 지정하고 싶다면 border-top-style,border-right-style,border-bottom-style,border-left-style처럼
        border와 style 사이에 상하좌우 방향을 넣고 하이픈(-)으로 연결함.*/
	</style>
```

# 테두리 두께를 지정하는 border-width 속성
테두리 두께를 지정할 때는 1px처럼 크기를 직접 입력할 수도 있고 thin이나 medium,thick같은 예약어 중에서 선택할 수도 있음.  
```css
border-width: <크기> | thin | medium | thick
/*만일 테두리 4개 방향 모두 두께를 다르게 하고 싶다면 border-top-width처럼 border와 width사이에 상하좌우 방향을 넣고 하이픈(-)으로 연결함.*/
```

```css
#box1 {
      border-width:2px;  /* 네 방향 모두 2px */ 
    }
    #box2 {
      border-width:thick thin;  /* 속성값이 2개면 첫번째값이 위아래(top,bottom), 두번째값이 좌우(left,right)값이 됨. */
    }
    #box3 {
      border-width:thick thin thin;  /* 순서대로 top->right->bottom의 속성값인데 left는 마주보는 right 속성값과 똑같이 적용됨. */ 
    }
    #box4 {
      border-width:10px 5px 5px 10px;  /* top->right->bottom->left 순으로 적용*/
    }
```


# 테두리 색상을 지정하는 border-color 속성
4개 방향의 테두리 색상을 한꺼번에 지정할 수도 있고, border-top-color 처럼 border와 color사이에 테두리 방향을 넣어 주면 색상을 하나씩 지정할 수도 있다.  

# 테두리 스타일을 묶어 지정하는 border 속성
테두리 스타일,두께,색상을 한꺼번에 표현하기 위한 방법.  
4개 방향의 테두리 스타일을 다르게 지정하고 싶다면 border-top이나 border-right 처럼 속성 이름에 방향을 함께 써서 따로 지정할 수도 있고,  
4개 방향의 테두리 스타일이 같다면 간단히 border 속성만 사용하면 됨.  
이때 테두리의 두께와 색상,스타일의 속성값 순서는 상관 없다.  

```css
p 
{
	padding: 10px;
	border: 3px dotted blue; /* 모든 테두리를 3px짜리 파란 점선 */
}
```

# 둥근 테두리를 만드는 border-radius 속성
사각형의 꼭짓점 부분에 원이 있다고 가정해서 둥글게 처리함.  
```css
border-radius: <크기> | <백분율>
```  
**[border-radius의 속성값]**  
>
**```<크기>```:** 반지름 크기를 px,em의 단위와 함께 수치로 표시함.  
**```<백분율>```:** 현재 요소의 크기를 기준으로 비율(%)으로 지정함.  

border-radius 속성을 사용하여 이미지를 원 형태로 만들 수 있다.  
이미지 요소의 너비와 높이를 똑같이 만든 후 border-radius의 반지름값을 너비나 높이의 50%로 지정하면 원이 됨.

# 꼭짓점마다 따로 둥글게 처리하기 
박스 모델에서 꼭짓점 4개를 모두 다르게 지정하고 싶다면 border와 radius 사이에 위치를 나타내는 예약어를 넣어 사용함.  
ex) border-top-left-radius  

# 꼭짓점을 타원으로 만들기
border-radius 속성을 사용해서 꼭짓점을 타원 형태로 만들 수 있다.  
이 경우에는 꼭짓점에 원 대신 타원이 있다고 생각함.  
그래서 반지름 대신 타원의 가로 반지름값과 세로 반지름값을 넣어 주는데, 이때 가로 반지름과 세로 반지름 사이에 슬래시(/)를 너헝서 구분함.  
```css
border-radius: <가로 반지름> / <세로 반지름>;
```  
그리고 특정한 꼭짓점만 타원 형태로 만들겠다면 슬래시 없이 가로 반지름과 세로 반지름을 지정함.  
```css
border-위치-radius: <가로 반지름> <세로 반지름>;
```