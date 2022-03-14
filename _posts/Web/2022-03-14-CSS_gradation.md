---
layout: post
title: CSS 그라데이션 효과로 배경 꾸미기
date: 2022-03-14 00:00:00+0900
category: Web
published: true
---
# 선형 그라데이션  
색상이 수직,수평 또는 대각선 방향으로 일정하게 변하는 그라데이션.   
linear-gradient 함수를 이용하여 색상이 어느 방향으로 바뀌는지 그리고 어떤 색상으로 바뀌는지 알려줘야 함.  
```
linear-gradient(to <방향> 또는 <각도>, <색상 중지점>, [<색상 중지점>, ...]);
```

**- 방향:** 끝 지점을 기준으로 to 예약어와 함께 사용. to 다음에는 방향을 나타내는 예약어를 최대 2개까지 사용 가능. 수평방향은 left와 right, 수직방향은 top과bottom을 사용함.  
방향이나 각도를 생략하면 to bottom으로 인식함.  

**- 각도:** 각도는 그라데이션이 끝나는 부분이고 값은 deg로 표기함. 맨 윗부분이 0deg고 시계 방향으로 회전하면서 90deg, 180deg가 됨.  
**- 색상 중지점:**  2가지 색이상의 선형 그라데이션을 만들려면 색상이 바뀌는 부분을 지정해 줘야 함. 그라데이션에서 바뀌는 색을 색상 중지점이라고 함. 색상 중지점을 지정할 때 쉼표(,)로 색상을 구분하는데 색상만 지정할 수도 있고 색상과 함께 중지점의 위치도 함께 지정할 수 있다.  
```
색상 중지점 예시
background: linear-gradient(to bottom, #06f, white 30%, #06f;)
                                      시작색상, 중지점의색과위치, 끝 색상
 ```  

# 원형 그라데이션 
```
기본형
radial-gradient(<모양><크기> at <위치>, <색상 중지점>, [<색상 중지점>,...])
```

**- 모양:** 원형(circle), 타원형(ellipse) 두 가지로 구분됨. 모양을 따로 지정안하면 타원형.  
```html
	/* 타원형 원형 그러데이션 */
		.grad1{
			background:red;
			background:radial-gradient(white, yellow, red); /* 타원형으로 흰색, 노란색, 빨간색으로 바뀌는 그러데이션 */
		}

		/* 원형 그러데이션 */
		.grad2{
			background:red;
			background:radial-gradient(circle, white, yellow, red);  /* 원형으로 흰색, 노란색, 빨간색으로 바뀌는 그러데이션 */
		}
```  
**- 크기:** 원의 모양과 크기를 나타내는 키워드 값을 함께 쓰면 됨. 사용할 수 있는 값은 다음과 같음.  
>
- closet-side  
- closet-corner  
- farthest-side  
- farthest-corner

**- 위치:** at 키워드와 함께 지정하면 그라데이션이 시작하는 원의 중심을 다르게 나타낼 수 있음. 위치 속성값은 (left,center,right 중 하나 또는 top,center,bottom중 하나) 또는 백분율임. 속성값을 생략하면 가로와 세로 모두 중앙인 center로 인식함.  

**- 색상 중지점:** 원과 같음  

# 그라데이션을 사용한 패턴 만들기 
선형 그라데이션을 반복할 때는 repeating-linear-gradient를 사용하고  
원형 그라데이션을 반복할 때는 repeating-radial-gradient를 사용함.   
다음은 사용 예시임.  
```html
.grad1 {
		background: red; 
		background: repeating-linear-gradient(yellow, yellow 20px, red 20px, red 40px); 
		}
.grad2 {
		background: #ccc; 
		background: repeating-radial-gradient(circle, white, white 10%, #ccc 10%, #ccc 20%); 
}
```
