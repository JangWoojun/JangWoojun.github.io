---
title: 안드로이드 Firebase Realtime Database Permission denied Error
date: 2023-08-20 21:00:00 +/-0000
categories: [Problem, Android]
tags: [android, problem]
toc: true
pin: true
---

# 문제 상황

Firebase Realtime Database 읽기 코드를 사용하던 중 

~~~
Permission denied
~~~

위와 같은 에러 메시지가 발생하였다

# 해결법

해결법은 생각보다 간단한데
Firebase 콘솔에서 Realtime Database 규칙을 읽기를 허용으로 바꿔준다