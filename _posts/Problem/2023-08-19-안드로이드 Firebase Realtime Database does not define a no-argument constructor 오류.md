---
title: 안드로이드 Firebase Realtime Database does not define a no-argument constructor 오류
date: 2023-08-19 16:45:55 +/-0000
categories: [Problem, Android]
tags: [android, problem]
toc: true
pin: true
---

# 문제 상황

Firebase Realtime Database 읽기 코드를 사용하던 중 

~~~
com.google.firebase.database.DatabaseException: Class com.woojun.ai.util.UserInfo does not define a no-argument constructor. If you are using ProGuard, make sure these constructors are not stripped.
~~~

위와 같은 에러 메시지가 발생하였다


~~~kotlin
val value = snapshot.getValue(UserInfo::class.java)
~~~

문제 코드 부분

# 해결법

해결법은 생각보다 간단한데
getValue에서 사용한 DataClass를

~~~kotlin
data class UserInfo(
    val name: String = "",
    val email: String = "",
    val phoneNumber: String = "",
    val photo: String = "",
    val check: Boolean = false,
    val children: ArrayList<ChildInfo> = arrayListOf()
)
~~~

위와 같이 기본 값을 설정해주면 된다