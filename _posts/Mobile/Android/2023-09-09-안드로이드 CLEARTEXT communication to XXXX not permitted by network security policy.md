---
title: 안드로이드 CLEARTEXT communication to XXXX not permitted by network security policy
date: 2023-09-09 23:00:00 +/-0000
categories: [Mobile, Android]
tags: [android]
toc: true
pin: true
---

# 안드로이드 CLEARTEXT communication to XXXX not permitted by network security policy

~~~
CLEARTEXT communication to XXXX not permitted by network security policy
~~~

해당 문제는 안드로이드 9.0 파이에서는 https를 사용하도록 강제하기 때문에 생긴 문제로 주소가 http로 되어있기에 발생했기에 https로 바꾸면 문제가 해결된다 하지만 이 방법을 사용할 수 없을 땐

~~~xml
<application
        android:usesCleartextTraffic="true"
        tools:targetApi="31">
~~~

manifest에 있는 application에 위와 같이

~~~xml
android:usesCleartextTraffic="true"
~~~

해당 코드를 추가해주면 된다



