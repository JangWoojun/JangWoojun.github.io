---
title: 안드로이드 Android Module-Level Build.gradle 오류 해결 방법
date: 2023-11-09 22:00:00 +/-0000
categories: [Problem, Android]
tags: [android, problem]
toc: true
pin: true
---

# 문제 상황

안드로이드에서 local.properties를 사용해서 API 키를 숨기려던 중 아래와 같은 오류 메시지가 발생했다

~~~kotlin
Cause: defaultConfig contains custom BuildConfig fields, but the feature is disabled. To enable the feature, add the following to your module-level build.gradle: `android.buildFeatures.buildConfig true`
~~~

# 해결법

해당 문제 해결 방법은 생각보다 간단한데

~~~kotlin
android {
    buildFeatures {
        buildConfig = true
    }
}
~~~

위 코드를 적어주면 해당 오류 메시지는 사라지게 된다