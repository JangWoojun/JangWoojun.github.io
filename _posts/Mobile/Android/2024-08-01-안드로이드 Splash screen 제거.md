---
title: 안드로이드 Splash Screen API 제거
date: 2024-08-01 02:20:00 +/-0000
categories: [Mobile, Android]
tags: [android]
toc: true
pin: true
---

안드로이드 앱 개발을 하다보면 과거와 달리 안드로이드 12에서 새로 생긴 Splash Screen API 때문에 불편할 때가 있다 이번 글에선 해당 기능을 제거 법에 대해 간단히 설명하겠다

## 구현 방법

제거 방법은 매우 간단한데 res/values/styles.xml 파일에서

~~~xml
<style name="Base.Theme.Test" parent="Theme.Material3.DayNight.NoActionBar">
    <item name="android:windowIsTranslucent">true</item>
</style>
~~~

이런 식으로

~~~xml
    <item name="android:windowIsTranslucent">true</item>
~~~

windowIsTranslucent를 true로 주면 된다 이는 원래 window를 투명으로 설정하는 속성인데
Splash Screen API에도 적용이 되는 것 같다