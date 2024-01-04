---
title: 안드로이드 No type arguments expected for class Call 에러
date: 2024-01-04 19:20:00 +/-0000
categories: [Problem, Android]
tags: [android, problem]
toc: true
pin: true
---

# 문제 상황

안드로이드에서 Retrofit2를 사용해서 RetrofitAPI interface를 생성하던 중 Call 부분에서 자꾸만 오류가 발생하였다

~~~kotlin
import android.telecom.Call 
import retrofit2.http.GET
import retrofit2.http.Query

interface RetrofitAPI {
    @GET("")
    fun GeT(
        
    ): Call<GET> // 에러

}
~~~

# 해결법

해당 문제 해결하는 방법은 생각보다 간단한데

~~~kotlin
import retrofit2.Call // 이 부분
import retrofit2.http.GET
import retrofit2.http.Query

interface RetrofitAPI {
    @GET("mealServiceDietInfo")
    fun GetLunch(
        @Query("KEY") KEY: String,
        @Query("Type") Type: String,
        @Query("ATPT_OFCDC_SC_CODE") ATPT_OFCDC_SC_CODE: String,
        @Query("SD_SCHUL_CODE") SD_SCHUL_CODE: String,
    ): Call<FoodInfoList>

}
~~~

이 문제의 원인으로는 주로 Call import가 잘못된 것으로 retrofit2.Call로 해야 하는데 빠르게 하다보니 telecom로 되어 오류가 발생한 경우가 많다