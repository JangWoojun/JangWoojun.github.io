---
title: 안드로이드 Suspension functions can be called only within coroutine body 오류 메시지
date: 2023-09-10 1:40:00 +/-0000
categories: [Mobile, Android]
tags: [android]
toc: true
pin: true
---

# 안드로이드 Suspension functions can be called only within coroutine body 오류 메시지

~~~
Android Suspension functions can be called only within coroutine body
~~~

해당 문제는 코루틴 스코프 안에서 코루틴 스코프를 또 사용해서 발생한 오류 메시지로 만약 CoroutineScope(Dispatchers.IO) 안에서 UI 작업을 위해 메인 스레드에서 실행해야 하는 코드가 필요하다면 CoroutineScope(Dispatchers.Main) 이런 식으로 사용 하는 것이 아닌

~~~kotlin
CoroutineScope(Dispatchers.IO).launch {
    withContext(Dispatchers.Main) {
        
    }
}
~~~

위와 같이 withContext(Dispatchers.Main)을 통해서 하면 Android Suspension functions can be called only within coroutine body 에러 메시지는 나오지 않게 된다



