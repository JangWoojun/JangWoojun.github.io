---
title: 안드로이드 TextInputEditText 커서, 하이라이트 색상 변경
date: 2023-07-05 15:35:00 +/-0000
categories: [Mobile, Android]
tags: [android, problem]
toc: true
pin: true
---

# 문제 상황

안드로이드에서 입력창 구현을 위해 TextInputEditText를 사용하다보니 커서 색상과
하이라이트 색상이 마음에 들지 않아, 커서 색상과 하이라이트 색상을 변경하고 싶다

# 해결법

그럴 때는 아래와 같은 방법으로 TextInputEditText 색상을 원하는대로 변경할 수 있다


## TextInputEditText 하이라이트 색상 변경

우선 TextInputEditText 하이라이트 색상 변경 방법이다

~~~xml
<!--drawable/name-->
<shape xmlns:android="http://schemas.android.com/apk/res/android">
    <solid android:color=원하는 색상/>
    <size android:width="20dp"/>
    <size android:height="20dp"/>
    <corners android:radius="10dp"/>
</shape>
~~~

위 코드를 이용하여 내가 원하는 색상을 넣어서 drawable에 파일을 생성한 뒤

~~~xml
<com.google.android.material.textfield.TextInputEditText
android:textColorHighlight=원하는 색상
android:textSelectHandle="@drawable/name"
android:textSelectHandleLeft="@drawable/이name름"
android:textSelectHandleRight="@drawable/name"
<!--생략-->
/>
~~~

TextInputEditText 위 옵션들에 아까 생성한 파일을 적용하면 하이라이트 색상 변경이 완료된다

## TextInputEditText 커서 색상 변경

다음은 TextInputEditText 커서 색상 변경 방법이다

~~~xml
<!--drawable/name-->
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android">
    <size android:width="2dp"/>
    <solid android:color=원하는 색상/>
</shape>
~~~

위 코드를 이용하여 내가 원하는 색상을 넣어서 drawable에 파일을 생성한 뒤

~~~xml
<com.google.android.material.textfield.TextInputEditText
android:textCursorDrawable="@drawable/name"
<!--생략-->
/>
~~~

TextInputEditText textCursorDrawable 옵션에 아까 생성한 파일을 적용하면 커서 색상 변경이 완료된다

[참고 블로그 글](https://kumgo1d.tistory.com/46)