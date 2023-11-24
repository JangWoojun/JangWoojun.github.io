---
title: 안드로이드 ItemDecoration이란?
date: 2023-11-24 1:40:00 +/-0000
categories: [Mobile, Android]
tags: [android]
toc: true
pin: true
---

안드로이드 앱 개발에서 RecyclerView는 데이터 목록을 효율적으로 표시하는데 자주 사용되는 뷰로 이러한 RecyclerView의 사용자 인터페이스를 바꾸는데 사용할 수 있는 ItemDecoration에 대해 Kotlin 언어를 사용하여 알아보려고 한다

## ItemDecoration이란?

우선 ItemDecoration에 대해 자세히 알아보자 

기존의 사용하던 ListView의 경우에는 아이템들을 구분하기 위한 구분선을 넣는 기능이 자체적으로 존재했지만 RecyclerView는 존재하지 않아 ItemDecoration을 통해 구현해야한다 

이러한 ItemDecoration은 RecyclerView의 각 아이템에 장식을 추가할 수 있는 클래스로 이를 통해 아이템 간의 구분선을 추가하거나 간격을 조절하는 등의 작업을 할 수 있는 등 ItemDecoration은 RecyclerView의 확장성과 유연성을 증가시킬 수 있는데

## ItemDecoration의 주요 기능 및 구현 방법

다음으로 ItemDecoration을 통해 할 수 있는 작업을 알아보면

* onDraw() 또는 onDrawOver() 메서드를 오버라이드하여 아이템 사이에 선이나 기타 그래픽을 그려 아이템 사이의 구분선 추가하는 작업이 가능하다
* getItemOffsets() 메서드를 사용하여 각 아이템의 여백을 조정할 수 있다

위와 같고 이러한 ItemDecoration을 구현하기 위해선

1. RecyclerView.ItemDecoration을 확장하여 새로운 클래스를 만든다

2. onDraw()와 onDrawOver() 메서드들을 오버라이드하여 아이템 사이에 선이나 기타 그래픽을 그립니다

3. getItemOffsets() 메서드를 오버라이드하여 항목의 여백을 설정한다

이러한 방식을 따를 수 있다 

## 구분선 추가 방법

백문이 불여일견이라고 이제 구분선 추가 방법 예제 코드를 통해 직접 확인해보자

~~~kotlin
class SimpleDividerItemDecoration(context: Context) : RecyclerView.ItemDecoration() {
    private val mDivider: Drawable = ContextCompat.getDrawable(context, R.drawable.line_divider)!!

    override fun onDrawOver(c: Canvas, parent: RecyclerView, state: RecyclerView.State) {
        val left = parent.paddingLeft
        val right = parent.width - parent.paddingRight

        val childCount = parent.childCount
        for (i in 0 until childCount) {
            val child = parent.getChildAt(i)
            val params = child.layoutParams as RecyclerView.LayoutParams

            val top = child.bottom + params.bottomMargin
            val bottom = top + mDivider.intrinsicHeight

            mDivider.setBounds(left, top, right, bottom)
            mDivider.draw(c)
        }
    }
}
~~~

해당 코드는 onDrawOver() 메서드를 사용하여 각 항목의 아래쪽에 구분선을 그리는 코드로 Drawable line_divider를 사용하여 선을 그리고 있다

사용법은

~~~kotlin
val recyclerView = findViewById<RecyclerView>(R.id.my_recycler_view)
recyclerView.addItemDecoration(SimpleDividerItemDecoration(this))
~~~

간단히 위와 같이 사용할 수 있다

## 간격 설정 방법

다음으로는 간격 설정 방법인데 해당 내용을 과거 블로그 글인 [안드로이드 RecyclerView item 간격 설정](https://jangwoojun.github.io/posts/%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C-RecyclerView-item-%EA%B0%84%EA%B2%A9-%EC%84%A4%EC%A0%95/)에서 잘 정리해두었으니 해당 글을 참고하자