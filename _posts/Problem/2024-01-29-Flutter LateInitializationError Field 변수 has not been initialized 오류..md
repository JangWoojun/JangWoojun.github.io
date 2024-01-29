---
title: Flutter LateInitializationError Field 변수 has not been initialized 오류
date: 2024-01-29 21:50:55 +/-0000
categories: [Mobile, Flutter]
tags: [flutter, dart]
toc: true
pin: true
---

# 문제 상황

Flutter에서 위젯들을 이용해 화면을 구성하던 중 

~~~
LateInitializationError Field 변수 has not been initialized
~~~

위와 같은 오류가 발생하였다

# 해결법

해당 문제 해결하는 방법은 생각보다 간단한데 바로 late로 선언된 변수를 초기화하면 된다

이 문제의 원인으로는 late로 변수를 선언 후 초깃값을 셋팅 하지 않고 해당 변수에 바로 접근했기에 발생한 것이다