---
title: 안드로이드 registerForActivityResult IllegalStateException 오류 해결 방법
date: 2024-08-10 1:50:00 +/-0000
categories: [Problem, Android]
tags: [android, problem]
toc: true
pin: true
---

# 문제 상황

안드로이드에서 registerForActivityResult를 사용하던 중 오류가 발생하여 앱이 강제 종료되는 문제가 발생했다

~~~
java.lang.IllegalStateException: LifecycleOwner X is attempting to register while current state is STARTED. LifecycleOwners must call register before they are STARTED.
~~~

에러 메세지는 위와 같았으며 문제가 생긴 부분은

~~~kotlin
private lateinit var pickMedia: ActivityResultLauncher<PickVisualMediaRequest>

override fun onResume() {
    super.onResume()

    pickMedia = registerForActivityResult(ActivityResultContracts.PickVisualMedia()) { uri ->
        
    }
}
~~~

위와 같이 pickMedia를 초기화 시킨 부분이다

# 해결법

해결방법으로는 에러 메세지를 해석하면 간단하다 

~~~kotlin
private lateinit var pickMedia: ActivityResultLauncher<PickVisualMediaRequest>

override fun onResume() {
    super.onResume()

    pickMedia = registerForActivityResult(ActivityResultContracts.PickVisualMedia()) { uri ->
        
    }
}
~~~ 

이렇게 onResume에서 초기화 시킨 코드를

~~~kotlin
private lateinit var pickMedia: ActivityResultLauncher<PickVisualMediaRequest>

override fun onStart() {
    super.onStart()

    pickMedia = registerForActivityResult(ActivityResultContracts.PickVisualMedia()) { uri ->
        
    }
}
~~~ 

이렇게 또는

~~~kotlin
private lateinit var pickMedia: ActivityResultLauncher<PickVisualMediaRequest>

override fun onCreate() {
    super.onCreate()

    pickMedia = registerForActivityResult(ActivityResultContracts.PickVisualMedia()) { uri ->
        
    }
}
~~~ 

이렇게 초기화 시점을 생명주기에서 onResume보다 빠른 onCreate나 onStart로 하면 오류가 해결된다