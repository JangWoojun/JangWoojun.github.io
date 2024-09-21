---
title: 안드로이드 ScrollView 꽉차게
date: 2024-09-21 06:10:00 +/-0000
categories: [Mobile, Android]
tags: [android]
toc: true
pin: true
---

안드로이드 앱 개발을 하다 보면 ScrollView 사용하게 되는데 이럴 때 초기 데이터가 없다거나와 같은 문제로 화면을 넘치지 못하게 사용할 때가 있다 이러면 화면 이상하게 붙게 되는데 나도 초반에는 이를 해결하는 법을 몰라 꽤나 고생을 많이 했다 하지만 최근 이를 해결하는 법을 알게 되어 공유하려고 한다

# 구현 방법

해당 방법을 해결하는 방법은 매우 쉬운데

```xml
android:fillViewport="true"
```

ScrollView에 위 옵션들을 적용하면 깔끔하게 우리가 원하던 대로 화면이 나오게 된다