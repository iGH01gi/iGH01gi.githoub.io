---
layout: post
title: CSS 목록 스타일
date: 2022-02-27 00:00:00+0900
category: Web
published: true
---
# 불릿 모양과 번호 스타일을 지정하는 list-style-type 속성
>
**목록 스타일의 속성값**  
**disc:** 채운 원 모양  
**circle:** 빈 원 모양  
**square:** 채운 사각형 모양  
**decimal:** 1부터 시작하는 10진수  
**decimal-leading-zero:** 앞에 0이 붙는 10진수  
**lower-roman:** 로마 숫자 소문자  
**upper-roman:** 로마 숫자 대문자  
**lower-alpha 또는 lower-latin:** 알파벳 소문자  
**upper-alpha 또는 upper-latin:** 알파벳 대문자  
**none:** 불릿이나 숫자를 없앰.  

```css
/*예시*/
.book2 {
      list-style-type: upper-alpha;  /* 알파벳 대문자 */
    } 
```  

# 불릿 대신 이미지를 사용하는 list-style-image 속성
불릿에 들어갈 이미지는 불릿 크기만큼 작아야 좋음.  
```css
/*기본형*/
list-style-image: <url(이미지 파일 경로)> | none

/*사용 예*/
ul {
      list-style-image: url('images/dot.png') /* 불릿으로 사용할 이미지 */
    }
```

# 목록을 들여 쓰는 list-style-position 속성
불릿이나 번호의 위치를 기본값으로 들여쓰느냐 아니면 더 들여쓰느냐를 결정함.  
>
**list-style-position 속성값**  
**inside:** 불릿이나 번호를 기본 위치보다 안으로 들여 씀.  
**outside:** 기본값.  

```css
/*기본형*/
list-style-position: inside | outside;

/*사용 예*/
<style>
    .inside { list-style-position: inside; }  /* 목록 들여쓰기 */
</style>
```

# 목록 속성을 한꺼번에 표시하는 list-style 속성
list-style속성을 사용하면 지금까지 설명한 list-style-type, list-style-image, list-style-position 속성을 한꺼번에 표시할 수 있음.  
```css
ol{
  list-style-type: lower-alpha;
  list-style-position: inside;
}

/* 줄여서 표시하면*/
ol{
  list-style: lower-alpha inside;
}
```