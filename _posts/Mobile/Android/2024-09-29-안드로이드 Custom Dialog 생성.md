---
title: 안드로이드 Custom Dialog 생성
date: 2024-09-29 06:10:00 +/-0000
categories: [Mobile, Android]
tags: [android]
toc: true
pin: true
---

안드로이드 앱 개발을 하다 보면 기본 Dialog 대신 디자인 적으로 예쁘고 특정 기능을 넣은 Custom Dialog를 만들고 싶을 때가 있다 이번 글에서는 이러한 Custom Dialog를 만드는 법에 대해 알아보려고 한다

## 1. Dialog 레이아웃 설정

우선은 Custom Dialog에 쓰일 layout을 만들어야 한다 이번 예제에서는 로그아웃 Dialog를 만들다고 가정하겠다

`dialog_logout`

~~~xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.cardview.widget.CardView
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    app:cardBackgroundColor="@color/background"
    app:cardCornerRadius="16dp"
    app:cardElevation="0dp"
    android:layout_width="match_parent"
    android:layout_marginHorizontal="8dp"
    android:layout_height="wrap_content">

    <androidx.constraintlayout.widget.ConstraintLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <TextView
            android:layout_marginTop="20dp"
            app:layout_constraintTop_toTopOf="parent"
            android:layout_marginHorizontal="20dp"
            style="@style/heading_accent"
            android:textColor="@color/Text_Default_Primary"
            android:id="@+id/title_text"
            android:text="계정에서 로그아웃하시겠어요?"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"/>

        <TextView
            android:id="@+id/content_text"
            android:layout_marginTop="4dp"
            android:layout_marginHorizontal="20dp"
            app:layout_constraintTop_toBottomOf="@id/title_text"
            style="@style/body_default"
            android:text="계정에서 로그아웃 할 시,\n로그인 할 때까지 사용하지 못해요"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"/>

        <androidx.cardview.widget.CardView
            android:id="@+id/main_button"
            android:layout_marginTop="16dp"
            android:layout_marginEnd="20dp"
            android:layout_marginBottom="20dp"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            app:cardBackgroundColor="@color/background_negative_Default"
            app:cardCornerRadius="8dp"
            app:cardElevation="0dp"
            app:layout_constraintBottom_toBottomOf="parent"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintTop_toBottomOf="@+id/content_text">

            <TextView
                style="@style/caption_accent"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_marginHorizontal="20dp"
                android:layout_marginVertical="8dp"
                android:text="확인"
                android:textColor="@color/white" />

        </androidx.cardview.widget.CardView>

        <com.google.android.material.card.MaterialCardView
            android:id="@+id/cancel_button"
            android:layout_marginTop="16dp"
            android:layout_marginEnd="8dp"
            android:layout_marginBottom="20dp"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            app:cardBackgroundColor="@color/background_gray_Default"
            app:cardCornerRadius="8dp"
            app:strokeColor="@color/background_gray_Border"
            app:strokeWidth="1dp"
            app:cardElevation="0dp"
            app:layout_constraintBottom_toBottomOf="parent"
            app:layout_constraintEnd_toStartOf="@id/main_button"
            app:layout_constraintTop_toBottomOf="@+id/content_text">

            <TextView
                style="@style/caption_accent"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_marginHorizontal="20dp"
                android:layout_marginVertical="8dp"
                android:text="취소"
                android:textColor="@color/Text_Default_Primary" />

        </com.google.android.material.card.MaterialCardView>

    </androidx.constraintlayout.widget.ConstraintLayout>

</androidx.cardview.widget.CardView>
~~~

## 2. Custom Dialog 코드

이제 해당 레이아웃을 사용하여 Dialog를 생성하는 함수를 만들겠다

~~~kotlin
private fun createDialog(context: Context, action: () -> Unit) {
    val customDialog = Dialog(context)
    customDialog.window?.setBackgroundDrawable(ColorDrawable(Color.TRANSPARENT))
    customDialog.window?.requestFeature(Window.FEATURE_NO_TITLE)
    customDialog.window?.setGravity(Gravity.CENTER)

    customDialog.setContentView(R.layout.dialog_setting)
    customDialog.window?.setLayout(
        WindowManager.LayoutParams.MATCH_PARENT,
        WindowManager.LayoutParams.WRAP_CONTENT
    )

    // 확인 버튼 클릭
    customDialog.findViewById<CardView>(R.id.main_button).setOnClickListener {
        action()  // 버튼 클릭 시 수행할 작업 실행
        customDialog.cancel()
    }

    // 취소 버튼 클릭
    customDialog.findViewById<MaterialCardView>(R.id.cancel_button).setOnClickListener {
        customDialog.cancel()
    }

    customDialog.show()
}
~~~

여기서 현재 상황에 따라 해당 함수를커스텀하며 사용하면 되는데 

~~~kotlin
customDialog.findViewById<TextView>(R.id.title_text).text = title
customDialog.findViewById<TextView>(R.id.content_text).text = content
~~~

이런 식으로 동적으로 dialog 내부 텍스트를 바꾸거나

~~~kotlin
customDialog.window?.setLayout(
    WindowManager.LayoutParams.MATCH_PARENT,
    WindowManager.LayoutParams.MATCH_PARENT
)
~~~

dialog 크기나

~~~kotlin
customDialog.window?.setBackgroundDrawable(ColorDrawable(Color.BLACK))
~~~

배경을 바꾸고

~~~kotlin
customDialog.window?.setGravity(Gravity.BOTTOM)
~~~

등장하는 위치를 가운데가 아닌 다른 위치로도 바꿀 수 있다