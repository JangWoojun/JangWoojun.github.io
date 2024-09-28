---
title: 안드로이드 ScrollView 스크롤바 제거
date: 2024-09-28 06:10:00 +/-0000
categories: [Mobile, Android]
tags: [android]
toc: true
pin: true
---

안드로이드 앱 개발을 하다 보면 ScrollView 사용하게 되는데 이러다보면 디자인 상으로 원치 않은 스크롤바가 자동으로 생겨 불편할 수 있다

# 구현 방법

해당 방법을 해결하는 방법은 매우 쉬운데

```xml
android:scrollbars="none"
```

ScrollView에 위 옵션들을 적용하면 깔끔하게 스크롤바가 제거되게 된다