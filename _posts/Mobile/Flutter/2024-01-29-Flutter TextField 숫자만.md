---
title: Flutter TextField 숫자만
date: 2024-01-29 20:55:55 +/-0000
categories: [Mobile, Flutter]
tags: [flutter, dart]
toc: true
pin: true
---

Flutter에서 사용자에게 무언가를 입력받을 때는 TextField를 사용하게 되는데 이러한 TextField에다가 사용자가 숫자만 넣게 하고 싶을 때가 있다

~~~dart
keyboardType: TextInputType.number,
~~~

그렇 때는 TextField keyboardType에 TextInputType.number을 넣어주면 된다
