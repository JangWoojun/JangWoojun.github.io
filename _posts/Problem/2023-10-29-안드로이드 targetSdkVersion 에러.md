---
title: 안드로이드 targetSdkVersion 에러
date: 2023-10-29 08:00:00 +/-0000
categories: [Problem, Android]
tags: [android, problem]
toc: true
pin: true
---

# 문제 상황

~~~
Not targeting the latest versions of Android; compatibility modes apply. Consider testing and updating this version. Consult the android.os.Build.VERSION_CODES javadoc for details.
~~~

안드로이드 스튜디오로 개발 중 위와 같은 메시지가 발생하였다

# 해결법

해당 문제를 쉽게 해결하기 위해서는 그냥 android:targetSdkVersion 부분을 제거해서 tagetSdkVersion을 min으로 잡히게 하면 복잡한 작업 없이 해당 오류 메시지를 간편히 사라지게 할 수 있다

