---
title: 안드로이드 ScrollView 안에 RecyclerView
date: 2024-09-21 06:15:00 +/-0000
categories: [Mobile, Android]
tags: [android]
toc: true
pin: true
---

안드로이드 앱 개발을 하다 보면 ScrollView 안에 RecyclerView를 위치해야 하는 경우가 자주 생기는데 여기서 그냥 썼다간 스크롤이 꼬여서 동작이 이상한 문제가 발생한다 그렇다면 어떻게 해야 우리가 원하는 동작을 구현할 수 있을까?

# 구현 방법

해당 방법을 구현하는 방법은 매우 쉬운데

```xml
android:overScrollMode="never"
android:nestedScrollingEnabled="false"
```

RecyclerView에 위 옵션들을 적용하면 깔끔하게 우리가 원하는 동작대로 움직이게 된다