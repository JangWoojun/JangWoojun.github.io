---
title: 안드로이드 Given final block not properly padded. Such issues can arise if a bad key is used during decryption. 에러
date: 2023-09-14 11:00:00 +/-0000
categories: [Problem, Android]
tags: [android, problem]
toc: true
pin: true
---

# 문제 상황

~~~
Given final block not properly padded. Such issues can arise if a bad key is used during decryption.
~~~

안드로이드에서 apk를 배포하기 위해 apk를 생성하던 중 위와 같은 오류 메시지가 발생하였다

# 해결법

해당 문제는 간단한 문제로 apk를 만드는 탭에서 Key password나 Key store password를 잘못 입력해서 생긴 문제로

당황하지 말고 다시 제대로 password를 입력하면 해결된다