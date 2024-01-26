---
title: Flutter the constructor being called isn't a const constructor 오류
date: 2024-01-26 18:30:55 +/-0000
categories: [Mobile, Flutter]
tags: [flutter, dart]
toc: true
pin: true
---

# 문제 상황

Flutter에서 위젯들을 이용해 화면을 구성하던 중 

~~~
the constructor being called isn't a const constructor
~~~

위와 같은 오류가 발생하였다

# 해결법

해당 문제 해결하는 방법은 생각보다 간단한데 바로 잘못된 const를 제거하면 된다

이 문제의 원인으로는 const는 컴파일 타임에 결정하지만 컴파일 타임에 결정되지 않은 것에 const를 붙여 에러가 발생한 것이다