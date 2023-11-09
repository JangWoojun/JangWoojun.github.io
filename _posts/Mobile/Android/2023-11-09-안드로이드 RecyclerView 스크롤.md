---
title: 안드로이드 RecyclerView 스크롤
date: 2023-11-09 22:00:00 +/-0000
categories: [Mobile, Android]
tags: [android]
toc: true
pin: true
---

# 안드로이드 RecyclerView 스크롤

안드로이드에서 RecyclerView를 사용하다보면 화면을 스크롤 시켜서 특정 위치에 있는 item을 보여주고 싶을 때가 있는데

해당 방법을 구현하는 방법은 매우 간단하다

~~~kotlin
RecyclerView이름.scrollToPosition(아이템 위치)
~~~

위와 같이 RecyclerView를 스크롤 시킬 수 있다

잘 이해가 안될 수도 있으니 예제 코드와 함께 본다면

**마지막 아이템으로 스크롤**
~~~kotlin
recyclerView.scrollToPosition(getAdapter().getItemCount()-1);
~~~

**첫 번째 아이템으로 스크롤**
~~~kotlin
recyclerView.scrollToPosition(0);
~~~

이런식으로 사용하면 된다