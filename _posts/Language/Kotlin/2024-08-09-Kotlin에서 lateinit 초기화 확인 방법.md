---
title: Kotlin에서 lateinit 초기화 확인 방법
date: 2024-08-09 01:00:55 +/-0000
categories: [Language, Kotlin]
tags: [kotlin]
toc: true
pin: true
---

안드로이드 개발 중 lateinit var를 사용하다보면 초기화 되지 않았는데 실수로 접근하여 오류가 나는 경우가 있다 이럴 땐 해당 변수가 초기화 되었는지 확인하여 접근하면 되는데 이번 글에선 해당 방법을 알아보겠다

## 구현 방법

구현 방법은 매우 간단한데 방법은 아래와 같다

~~~kotlin
private lateinit var adapter: TestAdapter
~~~

위와 같은 변수가 있다고 가정했을 때

~~~kotlin
::adapter.isInitialized
~~~

이런 식으로 ::변수명.isInitialized를 하면 Boolean 형태로 초기화 되었는지 여부를 반환하는데 이걸 조건문과 결합하면 간단히 초기화 여부를 알 수 있다