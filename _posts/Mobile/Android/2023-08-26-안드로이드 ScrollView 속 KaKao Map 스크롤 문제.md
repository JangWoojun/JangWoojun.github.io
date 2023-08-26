---
title: 안드로이드 ScrollView 속 KaKao Map 스크롤 문제 Kotlin
date: 2023-08-26 21:00:00 +/-0000
categories: [Mobile, Android]
tags: [android]
toc: true
pin: true
---

# 안드로이드 ScrollView 속 KaKao Map 스크롤 문제

안드로이드에서 ScrollView와 KaKao Map을 같이 쓰다보면 KaKao Map을 수직 스크롤하려 했으나 ScrollView가 포커스를 가져가

화면이 스크롤되어 매우 불편한데 해당 문제를 해결하기 위해서는 

~~~xml
<ScrollView
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    xmlns:android="http://schemas.android.com/apk/res/android">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical">

        <!-- 다른 뷰들 -->

        <!-- 카카오 맵 API 뷰 -->
            <RelativeLayout
        android:id="@+id/map_view"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />

    </LinearLayout>
</ScrollView>
~~~

~~~kotlin
binding.apply {
    val mapView = MapView(requireContext())
    binding.mapView.addView(mapView)

    mapView.setOnTouchListener { view, motionEvent ->
        val action = motionEvent.action
        when (action) {
            MotionEvent.ACTION_DOWN -> scrollView.requestDisallowInterceptTouchEvent(
                true
            )

            MotionEvent.ACTION_UP -> scrollView.requestDisallowInterceptTouchEvent(true)
            MotionEvent.ACTION_MOVE -> scrollView.requestDisallowInterceptTouchEvent(
                true
            )
        }
        false
    }
}
~~~

위 코드를 통해 ScrollView 속에 KaKao Map이 있더라도 KaKao Map 사용 시 ScrollView에 포커스를 빼앗기지 않을 수 있다

이 문제를 해결하려고 정말 열심히 검색했지만 계속 실패해서 좌절하다가 우연히 발견한 이 블로그 글 덕분에 해결할 수 있었다 감사합니다...! 

[출처](https://suji-choi.tistory.com/22)