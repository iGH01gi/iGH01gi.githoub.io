---
layout: post
title: HTML 다양한 파일 삽입
date: 2022-02-21 00:00:00+0900
category: Web
published: true
---
# 다양한 멀티미디어 파일 삽입 : &lt;object&gt; &lt;embed&gt; 태그
**＜object＞**태그는 오디오,비디오,자바 애플릿,PDF 등 다양한 멀티미디어 파일을 삽입할 때 사용.  
웹 문서 안에 다른 문서를 삽입할 때도 사용할 수 있다.  
```html
<object width="너비" height="높이" data="파일"></object>  //기본형
```  

<br>
**＜embed＞**태그는 HTML초기 버전부터 사용해서 대부분 브라우저에서 사용 가능.  
src속성을 사용해 멀티미디어 파일을 지정.  필요할 경우 width,height 속성으로 플레이어 크기 조절 가능.  
닫는 태그가 없음.  
```html
<embed src="파일 경로" width="너비" height="높이">
```  
찾아보니 ＜embed＞태그는 ＜video＞,＜audio＞,＜object＞태그를 지원하지 않는 웹 브라우저를 고려해야할 때만 사용하는것이 좋다고 함.  
플러그인 문제로 인한 것 같음.  권장되지 않는듯?  

# 오디오와 비디오 파일을 삽입하는 &lt;audio&gt;,&lt;video&gt; 태그
HTML4까지는 웹 브라우저에 멀티미디어 파일을 삽입 후 재생하려면 플러그인이 필요했음.  
HTML5에서는 웹 브라우저 안에서 멀티미디어 파일을 삽입하고 바로 재생 가능.  
따라서 웹 브라우저마다 플레이어가 다름.  다음 내용은 크롬부라우저가 기준임.  
```html
<audio src="오디오 파일 경로"></audio>
<video src="비디오 파일 경로"></video>

<audio src="medias/spring.mp3" controls></audio>
<video src="medias/salad.mp4" controls width="700"></video> //비디어파일의 너비값을 지정하지 않으면 웹브라우저에 가득차게 나타나므로 적절히 설정하는 것이 좋음.
```
>**＜audio＞** **＜video＞**태그의 속성  
>>**controls** : 플레이어 화면에 컨트롤 바를 표시함.  
**autoplay** : 오디오나 비디오를 자동으로 실행.  
**loop** : 오디오나 비디오를 반복 재생함.  
**muted** : 오디오나 비디오의 소리를 제거함.  
**preload** : 페이지를 불러올 때 오디오나 비디오 파일을 어떻게 로딩할 것인지 지정함. 사용할 수 있는 값은 auto,metadata,none 임. 기본값은 preload="auto"임.  
**width, height** : 비디오 플레이어의 너비와 높이를 지정함. 둘 중 하나만 지정할 경우 나머지는 자동으로 계산해서 표시함.  
**poster="파일이름"** : ＜video＞ 태그에서 사용하는 속성으로 비디오가 재생되기 전까지 화면에 표시될 포스터 이미지를 지정함.  

대부분의 웹 브라우저에서는 오디오나 소리가 있는 비디오 파일의 자동 재생을 금지하고 있다고 함.

