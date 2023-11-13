---
title: 안드로이드 java RuntimeException과 Kotlin lateinit 프로퍼티 초기화 오류 해결 방법
date: 2023-11-08 20:00:00 +/-0000
categories: [Problem, Android]
tags: [android, problem]
toc: true
pin: true
---

# 문제 상황

~~~
java.lang.RuntimeException: Unable to start activity 
~~~

안드로이드 개발 중 위와 같은 메시지가 발생하면서 앱이 종료되는 문제가 발생하였다

# 해결법

해당 문제는 오류 메시지와 제목에서도 알 수 있듯이 lateinit 프로퍼티를 초기화 하지 않고 사용하여 발생하는 간단한 문제로 해당 프로퍼티를 사용하기 전에 초기화하여서 사용하는 것으로 해당 문제를 간단히 해결 할 수 있다