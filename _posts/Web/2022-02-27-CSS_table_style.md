---
layout: post
title: CSS 표 스타일
date: 2022-02-27 00:00:00+0900
category: Web
published: true
---
# 표 제목의 위치를 정해 주는 caption-side 속성
캡션은 기본적으로 표 위쪽에 표시되지만 caption-side속성을 이용하면 표 아래쪽으로 옮길 수 있다.  
```css
caption-side: top | bottom
```  

# 표에 테두리를 그려 주는 border 속성 
```html
<!DOCTYPE html>
<html lang="ko">
	<head>
		<meta charset="UTF-8">
		<title>표 스타일</title>
    <style>
			table {
				caption-side: bottom;  /* 표 캡션 위치 */
				border:1px solid black;  /* 표 테두리는 검은 색 실선으로 */
			}
			td, th {
				border:1px dotted black;  /* 셀 테두리는 검은 색 점선으로 */
				padding:10px;  /* 셀 테두리와 내용 사이의 여백 */
				text-align:center;  /* 셀 내용 가운데 정렬 */
			}
		</style>
	</head>
	<body>		
		<h2>상품 구성</h2>
		<table>
			<caption>선물용과 가정용 상품 구성</caption>
			<thead>
				<tr>
					<th>용도</th>
					<th>중량</th>
					<th>갯수</t>
					<th>가격</th>
				</tr>
			</thead>
			<tbody>
				<tr>
					<td rowspan="2">선물용</td>
					<td>3kg</td>
					<td>11~16과</td>
					<td>35,000원</td>
				</tr>
				<tr>
					<td>5kg</td>
					<td>18~26과</td>
					<td>52,000원</td>
				</tr>
				<tr>
					<td rowspan="2">가정용</td>
					<td>3kg</td>
					<td>11~16과</td>
					<td>30,000원</td>
				</tr>   
				<tr>
					<td>5kg</td>
					<td>18~26과</td>
					<td>47,000원</td>
				</tr>
			</tbody>        
		</table>
	</body>
</html>
```
다음과 같이 표시됨.  
![표예시](\images\css\tableborder.png)   

# 셀 사이의 여백을 지정하는 border-spacing 속성
표와 셀에 따로 테두리르 지정하면 셀과 셀 사이에 여백이 조금 생김.  
border-spacing 속성을 사용하면 셀과 셀 사이의 여백을 조절할 수 있다.  
```html
border-spacing: 수평거리 수직거리
```  
border-spacing 속성값은 수평 거리의 값과 수직 거리의 값을 공백으로 구별해서 나타내는데, 두 값이 같다면 1개만 지정해도 됨.  

# 표와 셀 테두리를 합쳐 주는 border-collapse 속성
앞에서 설명한 ```<table>```태그와 ```<td>```태그에서 border 속성을 사용하면 셀과 셀 사이에 여백이 새익면서 두 줄로 표시됨.  
이때 두 줄로 그냥 둘 것인지 합쳐서 하나로 표시할 것인지 결정하는 것이 border-collapse 속성임.  
이 속성은 ```<table>```태그에 적용되는 스타일에만 지정하면 됨.  
>
**border-collapse의 속성값**  
**collapse:** 표와 셀의 테두리를 합쳐 하나로 표시함.  
**separate:** 표와 셀의 테두리를 따로 표시함. 기본값임.  

