---
title: 안드로이드 DataBindingComponent 관련 오류 해결 방법
date: 2024-06-04 22:00:00 +/-0000
categories: [Problem, Android]
tags: [android, problem]
toc: true
pin: true
---

# 문제 상황

안드로이드에서 DataBinding을 추가하여 사용하던 중 오류가 발생하였다 오류 메세지는 대충

~~~
cannot access DataBindingComponent
super(_bindingComponent, _root, _localFieldCount);
^ class file for androidx.databinding.DataBindingComponent not found
~~~

위와 같았다

# 해결법

해당 문제 해결하는 방법은 생각보다 간단한데
gradle.properties 파일에 단 한 줄만 추가하면 된다

~~~xml
android.enableJetifier=true
~~~

이렇게 하면 문제가 해결 된다!

[해당 내용 출처](https://github.com/google/iosched/issues/280)