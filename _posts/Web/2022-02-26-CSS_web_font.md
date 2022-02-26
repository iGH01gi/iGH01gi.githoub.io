---
layout: post
title: CSS 웹 폰트 사용
date: 2022-02-26 00:00:00+0900
category: Web
published: true
---
# 웹 폰트란
웹 폰트를 사용하려면 웹 문서를 작성할 때 글꼴 정보를 함께 저장해야 함.  
즉, 기존에 가지고 있던 웹 폰트를 사용했다면 웹 문서를 서버에 올릴 때 웹 폰트 파일도 함께 업로드해야함.  
웹 폰트를 사용한 사이트에 사용자가 접속하면 웹 문서를 내려받으면서 웹 폰트도 사용자 시스템으로 다운로드됨.  
결국 사용자 시스템에 없는 글꼴이라도 웹 문서를 만들때 사용한 글꼴을 내려받은 후 표시하므로 웹 제작자가 의도한 대로 텍스트를 보여줄 수 있다.  

# 웹 폰트 업로드 및 사용
구글 웹 폰트처럼 인터넷 사이트에서 제공해 주는 경우에는 링크해서 사용할 수도 있고  
그렇지 않은 글꼴이거나 자신이 가지고 있는 TTF 폰트를 변환해서 사용한다면 직접 업로드해서 사용해야 함.   
컴퓨터에서 사용하는 글꼴은 트루타임(TrueType)이고 파일 확장자는 *.ttf임.  
하지만 트루타입 글꼴은 파일 크기가 크기때문에 웹에 적합한 여러 글꼴이 등장했는데 그 중에서  
EOT(embeded open type)와 WOFF(web open font format),그리고 최근에는 WOFF2파일도 많이 사용함.  
>
웹 폰트를 변환하는 사이트중 Transfonter(https://transfonter.org)에서는 영문뿐만 아니라 한글 글꼴까지 변환할 수 있음.  

웹 폰트가 준비되었다면 **@font-face속성**을 사용하여 다음과 같이 웹 폰트를 정의함  
```css
@font-face
{
    font-family: <글꼴 이름>;
    src: <글꼴 파일>[<글꼴 파일>, <글꼴 파일>, ......];
}
```   
사용 예시는 다음과 같다
```html
<head>
    <meta charset="UTF-8">
    <title>웹 폰트 사용하기</title>
    <style>
      @font-face {
        font-family: 'Ostrich';  /* 폰트 이름 */
        src: local('Ostrich Sans'), 
              url('fonts/ostrich-sans-bold.woff') format('woff'), 
              url('fonts/ostrich-sans-bold.ttf') format('truetype'), 
              url('fonts/ostrich-sans-bold.svg') format('svg');
      }
      .wfont {
        font-family:'Ostrich', sans-serif; /* 웹 폰트 지정 */
      }
      p {
        font-size:30px; /* 글자 크기 */
      }
    </style>
</head>
```  
가장 먼저 font-family속성을 사용해 글꼴 이름을 만든다. 보통 글꼴 파일 이름과 같은 이름을 사용한다.  
src 속성에서는 사용할 글꼴 파일의 경로를 지정함.  
글꼴 파일의 경로를 지정하기 전에 local()문을 사용해서 사용자 시스템에 해당 글꼴이 있는지 먼저 확인해야 함.  
사용자 시스템에 글꼴이 있다면 그 글꼴을 사용하면 되지만, 없다면 WOFF포맷으로 된 글꼴을 내려받아야 함.  
>
이때 인터넷 익스플로러8 이하 버전에서는 EOT파일만 지원하므로 WOFF파일보다 먼저 선언하는데 EOT파일에서는 포맷을 따로 지정하지 않음. 참고로 여기에서는 EOT파일은 고려X

그리고 TTF 포맷은 다른 파일 형식보다 용량이 커서 대부분의 모던 브라우저에서 지원하는 WOFF포맷을 먼저 선언하고 TTF 포맷은 그 후에 선언함.  

<br>
<br>

### 인터넷에서 무료로 제공하는 웹 폰트를 간단히 링크하여 사용하는 방법 
(구글 폰트를 기준으로 설명)

<br>
**1. 구글 폰트 사이트에서 원하는 웹 폰트 찾기**  
[구글폰츠](https://fonts.google.com/?subset=korean)  
![구글폰츠1](\images\css\googlefonts1.png)  
예를 들어 Nanum Gothic(나눔고딕)을 골랐다고 하자.  

<br>

**2. 웹 폰트 스타일 복사하기**  
![구글폰츠2](\images\css\googlefonts2.png)   
+Select this style을 누른다.  
![구글폰츠2](\images\css\googlefonts3.png) 
@import를 누른후 그 속성이 보이도록 한다.  

<br>

**3. 웹 문서에 스타일 소스 넣기**  
전에 확인한 @import속성 2개를 복사하여 다음과 같이 쓴다.  
```html
<style>
    @import url('https://fonts.googleapis.com/css2?family=Nanum+Gothic&display=swap');

    h1
    {
        font-family: 'Nanum Gothic', sans-serif;
    }
    ///이렇게 하면 h1 제목텍스트에는 기본 글꼴대신 나눔고딕이 적용된다.
</style>
```