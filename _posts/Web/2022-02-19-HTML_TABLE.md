---
layout: post
title: HTML 표(table) 만들기
date: 2022-02-21
category: Web
published: true
---
# 표를 만드는 &lt;table&gt; 태그와 &lt;caption&gt; 태그
```html
<table>
    <caption>표 제목</caption>
</table>
```
표의 시작과 끝을 알려주는 **＜table＞**,**＜/table＞**태그를 표시하고 그 사이에 표와 관련된 태그를 모두 넣는다.  
표에 제목을 붙이고 싶다면 ＜table＞태그 바로 아랫줄에 **＜caption＞**태그를 사용한다.  
＜caption＞태그를 사용하면 제목은 표의 위쪽 중앙에 표시된다.   

# 행을 만드는 &lt;tr&gt; 태그와 셀을 만드는 &lt;td&gt;,&lt;th&gt;태그  
＜table＞태그만 작성하면 표가 만들어지지 않는다. 그 안에 행,행 안의 셀의 갯수를 적어야함.  
**＜tr＞**태그는 **행**,**＜td＞**태그는 **행 안에 있는 셀**을 만들기 때문에 ＜table＞태그 안에 ＜tr＞,＜td＞태그가 모두 있어야함.
```html
<table>
    <tr>
        <td>1행 1열</td>
        <td>1행 2열</td>
    </tr>
    <tr>
        <td>2행 1열</td>
        <td>2행 2열</td>
    </tr>
</table>
```
![테이블예시](\images\html\table.png)  
이런 식으로 생성이 된다.  

<br>
**＜th＞**태그는 표의 제목 행에 셀을 만들때 **＜td＞**대신 사용한다.  
굵은 글씨로 중앙에 배열된다.
```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>상품 소개 페이지</title>
  <style>
    table, th, td {
      border:1px solid #ccc;
      border-collapse: collapse;
    }
    th, td { padding:10px 20px; }
  </style>
</head>
<body>
  <h1>상품 구성</h1>
  <table>
    <caption>선물용과 가정용 상품 구성</caption>
    <tr>
      <th>용도</th>
      <th>중량</th>
      <th>갯수</th>
      <th>가격</th>
    </tr>
    <tr>
      <td>선물용</td>
      <td>3kg</td>
      <td>11~16과</td>
      <td>35,000원</td>
    </tr>
    <tr>
      <td>선물용</td>
      <td>5kg</td>
      <td>18~26과</td>
      <td>52,000원</td>
    </tr>
    <tr>
      <td>가정용</td>
      <td>3kg</td>
      <td>11~16과</td>
      <td>30,000원</td>
    </tr>   
    <tr>
      <td>가정용</td>
      <td>5kg</td>
      <td>18~26과</td>
      <td>47,000원</td>
    </tr>   
  </table>
</body>
</html>
```
![테이블예시](\images\html\table2.png)   
이런식으로 생성된다.  
용도,중량,갯수,가격이 **＜th＞**태그로 표현한 것이고  
나머지가 **＜td＞**태그로 표현한 것이다.

# 표의 구조를 지정하는 &lt;thead&gt;,&lt;tbody&gt;,&lt;tfoot&gt; 태그  
표의 제목,본문,요약으로 구조를 나누고 싶을때 사용하는 태그다.  
table의 't'와 제목(head), 본문(body), 요약(foot)을 각각 합친 말이다.  
CSS를 사용해 표의 제목,본문,요약에 각각 다른 스타일을 적용 가능.  
본문이 길어 한 화면을 넘어갈 경우, 자바스크립트를 이용해 ＜thead＞,＜tfoot＞태그는 표의 위아래에 고정하고 ＜tbody＞태그만 스크롤하도록 만들기 가능.  
```html
<table>
    <caption>표 제목</caption>
    <thead>                     
      <tr>
        <th>용도</th>
        <th>중량</th>
        <th>갯수</th>
        <th>가격</th>
      </tr>
    </thead>
    <tbody>                    
      <tr>
        <td>선물용</td>
        <td>3kg</td>
        <td>11~16과</td>
        <td>35,000원</td>
      </tr>
      <tr>
        <td>선물용</td>
        <td>5kg</td>
        <td>18~26과</td>
        <td>52,000원</td>
      </tr>
      <tr>
        <td>가정용</td>
        <td>3kg</td>
        <td>11~16과</td>
        <td>30,000원</td>
      </tr>   
      <tr>
        <td>가정용</td>
        <td>5kg</td>
        <td>18~26과</td>
        <td>47,000원</td>
      </tr>
    </tbody>        
    <tfoot align="center">
        <tr>
            <td colspan="4">요약(꼬리) 부분</td>
        </tr>
    </tfoot>
  </table>
```
# 행,열을 합치는 rowspan,colspan 속성 알아보기  
행이나 열을 합치는 것은 실제로는 셀을 합치는 것이므로 ＜td＞태그나 ＜th＞태그에서 이루어짐.  
행을 합치려면 rowspan 속성을 사용하고 열을 합치려면 colspan 속성을 사용함.  
**(rowspan은 세로로 합치기, colspan은 가로로합치기)**  
```html
<td rowspan="합칠 셀의 개수">셀의 내용</td>
<td colspan="합칠 셀의 개수">셀의 내용</td>
```

# 열을 묶어 주는 &lt;col&gt;,&lt;colgroup&gt; 태그
단순히 표를 만드는것이 아닌 특정 열에 배경색을 넣거나 너비를 바꾸려면 원하는 열을 선택할 수 있어야 한다.  
그럴때 사용하는 태그가 ＜col＞과 ＜colgroup＞태그다.  
**＜col＞태그는 열을 1개만 지정할 때 사용하고**  
**＜colgroup＞태그는 ＜col＞태그를 2개 이상 묶어서 사용함.**
> ＜colgroup＞태그에는 닫는 태그＜/colgroup＞가 있지만 ＜col＞태그에는 닫는 태그가 없다.  

```html
<colgroup>
    <col>
</colgroup>
```
＜col＞,＜colgroup＞태그는 반드시 ＜caption＞태그 다음에 써야함. (caption태그 자체는 생략가능.)  
즉, 표의 내용이 시작 되기 전에 열의 상태를 설정하는 것.  
**＜col＞태그를 사용할 때는 ＜colgroup＞태그 안에 ＜col＞태그를 포함해 표 전체 열의 개수만큼 ＜col＞태그를 넣어야 함.  
즉, 스타일 속성을 지정하지 않은 열이 있더라도 ＜col＞태그를 작성해야 함.**  
아래는 그 예시임  
```html
<table>
    <caption>표 전체의 제목</caption>
    <colgroup>
        <col style="background-color:#eee;">
        <col> //2번째 열에 지정할 스타일이 없어도 4열 짜리 표이기때문에 써줘야함.
        <col style="width:150px">
        <col style="width:150px">
    </colgroup>
    <thead>
        ...생략
```  
이때 위에서 3열,4열의 스타일이 같은 것을 볼 수 있다.  
이럴 때는 span 속성을 사용해서 묶어주면 된다.  
그 예시는 다음과 같다.  
```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>상품 소개 페이지</title>
  <style>
    table, th, td {
      border:1px solid #ccc;
      border-collapse: collapse;
    }
    th, td { padding:10px 20px; }
  </style>
</head>
<body>
  <table>
    <caption>선물용과 가정용 상품 구성</caption>
    <colgroup>
      <col style="background-color:#eee;">
      <col>
      <col span="2" style="width:150px">
    </colgroup>
    <thead>
      <tr>
        <th>용도</th>
        <th>중량</th>
        <th>갯수</th>
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
![테이블예시](\images\html\table3.png)  
이런식으로 표현되게 된다.