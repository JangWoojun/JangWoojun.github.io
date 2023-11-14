---
title: 안드로이드 RecyclerView item 간격 설정
date: 2023-11-14 18:00:00 +/-0000
categories: [Mobile, Android]
tags: [android]
toc: true
pin: true
---

RecyclerView는 안드로이드 앱 개발에서 리스트나 그리드 형태의 반복적인 요소를 표시할 때 listView와 함께 자주 사용되는 View로 하지만 기본적으로 아무 설정을 하지 않는다면 RecyclerView 아이템들 사이에는 간격이 없다. 그렇기에 이번 글에선 ItemDecoration을 통해 RecyclerView에 item 간격 설정을 하는 법에 대해 알아보려 한다

## ItemDecoration이란?

우선 간격 설정에 대해 알아보기 전 간격을 설정할 때 사용할 ItemDecoration에 대해 알아보면 ItemDecoration은 RecyclerView에 적용되는 데코레이션 요소로 아이템 간의 간격 설정, 구분선 추가 등의 기능을 제공한다.


## 간격 설정 방법

ItemDecoration을 통해 간격을 설정하는 방법을 순서대로 나타내면

1. 커스텀 ItemDecoration을 생성한다

2. getItemOffsets 오버라이드하여 각 아이템의 오프셋(간격)을 정의한다 참고로 Rect 객체를 사용하여 각 아이템의 상, 하, 좌, 우 간격을 설정할 수 있다

3. 생성한 ItemDecoration 클래스를 RecyclerView에 적용한다

## 코드

이제 코드로 확인해보자

~~~kotlin
// SpacesItemDecoration 파일 생성

class SpacesItemDecoration(private val space: Int) : RecyclerView.ItemDecoration() {
    override fun getItemOffsets(outRect: Rect, view: View, parent: RecyclerView, state: RecyclerView.State) {
        outRect.left = space
        outRect.right = space
        outRect.bottom = space

        // 첫 번째 아이템에만 상단 간격 추가
        if (parent.getChildAdapterPosition(view) == 0) {
            outRect.top = space
        }
    }
}
~~~

~~~kotlin
val recyclerView: RecyclerView = findViewById(R.id.my_recycler_view)
recyclerView.apply {
    layoutManager = LinearLayoutManager(this@MyActivity)
    adapter = MyAdapter()
    addItemDecoration(SpacesItemDecoration(20)) // 각 아이템 간 20dp 간격 적용
}
~~~

마치며 이외에도 itemView에 직접 마진을 설정하는 법도 있으나 개인적으로 위 방법을 유지보수, 재사용성 등등 관점에서 더 추천한다.