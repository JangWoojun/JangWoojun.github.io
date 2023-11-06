---
title: 안드로이드 Canvas trying to draw too large bitmap 오류
date: 2023-11-06 23:00:00 +/-0000
categories: [Problem, Android]
tags: [android, problem]
toc: true
pin: true
---

# 문제 상황

~~~
Canvas: trying to draw too large bitmap
~~~

안드로이드 개발 중 ImageView로 평소처럼 이미지를 넣고 빌드하니 위와 같은 메시지가 발생하였다

# 해결법

해당 문제는 사용한 이미지 사이즈가 너무 커서 일어나는 문제로 이미지의 사이즈를 줄이면 된다

또는 Glide 같은 외부 라이브러리를 사용해서 이미지를 사용할 수 있다
