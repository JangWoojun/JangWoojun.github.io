---
title: 안드로이드 Use JsonReader.setLenient(true) to accept malformed JSON at line 1 column 1 path $ 에러
date: 2023-09-12 13:00:00 +/-0000
categories: [Problem, Android]
tags: [android, problem]
toc: true
pin: true
---

# 문제 상황

~~~
Use JsonReader.setLenient(true) to accept malformed JSON at line 1 column 1 path $
~~~

안드로이드에서 레트로핏2로 GET 요청을 하던 중 위와 같은 오류 메시지가 발생했다

~~~
instance = Retrofit.Builder()
    .baseUrl(BuildConfig.BASEURL)
    .addConverterFactory(GsonConverterFactory.create())
    .build()
~~~

# 해결법

해당 문제는 GET 요청으로 받은 Json을 GSON을 통해 사용하다가 발생한 문제로 코드를 아래와 같이 바꿔주면 된다

~~~
val gson = GsonBuilder().setLenient().create()

instance = Retrofit.Builder()
    .baseUrl(BuildConfig.BASEURL)
    .addConverterFactory(GsonConverterFactory.create(gson))
    .build()
~~~