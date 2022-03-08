---
layout: post
title: VScode에서 자바 컴파일시 인코딩오류
date: 2022-03-09 00:00:00+0900
category: Java
published: true
---
![인코딩오류](\images\java\encoding.png)  
위와 같이 터미널에서 javac를 사용해 컴파일시 자바 컴파일러의 인코딩방식으로 인해 한글을 읽지 못해서 오류가 발생함.  

**해결법:** javac 컴파일할때 뒤에 -encoding utf-8을 붙여서 하자.
