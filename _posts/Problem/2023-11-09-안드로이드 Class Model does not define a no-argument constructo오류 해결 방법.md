---
title: 안드로이드 Class Model does not define a no-argument constructo 오류 해결 방법
date: 2023-11-13 9:20:00 +/-0000
categories: [Problem, Android]
tags: [android, problem]
toc: true
pin: true
---

# 문제 상황

안드로이드에서 Firebase를 사용하던 중 아래와 같은 오류 메시지가 발생하였다

~~~kotlin
Class Model does not define a no-argument constructor. If you are using ProGuard, make sure these constructors are not stripped.
~~~

# 해결법

해당 문제 해결 방법은 생각보다 간단한데

~~~kotlin
data class A (
    val a: String = ""
)
~~~

위 코드처럼 사용하는 Data class에 초기 값을 지정해주면 된다