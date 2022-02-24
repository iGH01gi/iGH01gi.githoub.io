---
layout: post
title: HTML 폼에서 사용하는 태그
date: 2022-02-24 00:00:00+0900
category: Web
published: true
---
# 여러 줄을 입력하는 텍스트 영역 &lt;textarea&gt; 태그
```html
<textarea>내용</textarea>
```
**＜textarea＞태그의 속성**  
>
**cols** : 텍스트 영역의 가로 너비를 문자 단위로 지정함.  
**rows** : 텍스트 영역의 세로 길이를 줄단위로 지정함. 지정한 숫자보다 줄 개수가 많아지면 스크롤 막대가 생김.  

```html
//사용 예
<label for="memo">메모</label>
<textarea id="memo" cols="40" rows="4"></textarea>
```

# 드롭다운 목록을 만들어 주는 &lt;select&gt; , &lt;option&gt; 태그
사용자가 내용을 직접 입력하지 않고 여러 옵션 중에서 선택하게 할때 드롭다운 목록이나 데이터 목록을 사용함.  
드롭다운 목록은 목록을 클릭했을 때 옵션이 요소 아래쪽으로 펼쳐져서 붙은 이름임.  
드롭다운 목록은 ＜select＞태그와 ＜option＞태그를 이용해 표시함.  
**<select＞**태그로 드롭다운 목록의 시작과 끝을 표시하고, 그 안에 **＜option＞**태그를 사용해 원하는 항목을 추가함.  
＜option＞태그에는 value 속성을 이용해 서버로 넘겨주는 값을 지정함.
```html
<select>
    <option value="값1">내용1</option>
    <option value="값2">내용2</option>
    ......
</select>
```
＜select＞ 태그를 사용해 만든 드롭다운 목록은 기본으로 옵션이 하나만 표시되는데, size 속성이나 multiple 속성을 이용하면 드롭다운 목록의 크기나 선택할
 항목의 개수를 조절할 수 있다.  
 **＜select＞태그의 속성**
 >
 **size** : 화면에 표시할 드롭다운 항목의 개수를 지정함.  
 **multiple** : 드롭다운 목록에서 둘 이상의 항목을 선택할 때 사용함.

 **＜option＞태그의 속성**
 >
 **value** : 해당 항목을 선택할 때 서버로 넘겨줄 값을 지정함.  
 **selected** : 드롭다운 메뉴를 삽입할 때 기본적으로 선택해서 보여 줄 항목을 지정함.  

# 데이터 목록 만들어 주는 &lt;datalist&gt; , &lt;option&gt; 태그
데이터 목록을 사용하면 텍스트 필드에 값을 직접 입력하지 않고 미리 만들어 놓은 값 중에서 선택할 수 있다.  
데이터 목록을 만들 때 **＜datalist＞**태그를 이용해 데이터 목록의 시작과 끝을 표시하고 그 사이에 **＜option＞**태그를 사용해 각 데이터의 옵션을 표시함.  
이때 value속성을 사용해서 서버로 넘겨줄 값을 지정하는데, 이 값이 텍스트 필드에도 나타남.  
그리고 데이터 목록을 사용할텍스트 필드에서 어떤 데이터 목록을 연결할지 id값을 지정하면 됨.  
```html
//기본형
<input type="text" list="데이터 목록 id">
<datalist id="데이터 목록 id">
    <option value="서버로 넘길 값1">선택 옵션1</option>
    <option value="서버로 넘길 값2">선택 옵션2</option>
</datalist>

//사용예시
<label for="prod2">포장 여부 </label>
<input type="text" id="prod2" list="pack">
<datalist id="pack">
    <option value="package">선물 포장</option>
    <option value="no_package">포장 안 함</option>
</datalist>        
```

# 버튼을 만들어 주는 &lt;button&gt; 태그
＜input＞태그의 필드를 사용하여 버튼을 삽입한 것과 비슷해보이지만 **＜button＞태그를 이용하여 폼을 전송하거나 리셋하는 버튼**을 삽입할 수 있다.  
(input태그에서의 button은 보통 자바스크립트를 실행할때 사용)
```html
//기본형
<button type="submit">내용</button>
<button type="reset">내용</button>
<button type="button">내용</button>
```  
＜button＞태그의 type속성은 버튼이 활성화되었을 때 어떤 동작을 할지 지정함.  
submit, reset, button 중에서 선택할 수 있고 만약 지정하지 않으면 submit을 선택한 것으로 간주함.  
>
**submit** : 폼을 서버로 전송함. ＜input type="submit＞과 같은 기능을 함.  
**reset** : 폼에 입력한 내용을 초기화함. ＜input type="reset"＞과 같은 기능을 함.  
**button** : 버튼 형태만 만들 뿐 자체 기능은 없다. ＜input type="button"＞과 같은 기능을 함.  

화면 낭독기로 웹 문서를 읽어줄 때 ＜button＞태그를 만나면 이 부분에 버튼이 있다는 것을 알고 정확히 전달함.  
그리고 ＜button＞태그는 폼뿐만 아니라 버튼이 필요한 웹 문서의 어디든지 다양하게 활용할 수 있음.  
＜button＞태그에는 콘텐츠를 포함할 수 있어서 아이콘을 추가하거나 CSS를 이용해 원하는 형태로 꾸밀 수도 있다.
