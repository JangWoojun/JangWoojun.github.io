---
title: 안드로이드 SharedPreference 값 저장
date: 2024-09-19 06:10:00 +/-0000
categories: [Mobile, Android]
tags: [android]
toc: true
pin: true
---

안드로이드 앱 개발을 하다 보면 액세스, 리프레쉬 토큰이나 이름, 특정 버튼 활성화 여부처럼 String 이나 Boolean 등과 같은 기본 타입들의 정보를 간단히 저장하여 사용하고 싶을 때가 있다 이럴 땐 Room이나 SQLite 보단 가볍게 SharedPreference를 사용하면 된다

이번 글에선 이러한 SharedPreference를 사용하는 법에 대해 쉽게 알아보겠다

# 구현 방법

## 앱 전역에서 사용

우선 앱 전역에서 사용하는 법에 대해 설명하겠다

`SharedPreference`

```kotlin
object SharedPreference {
    private const val NAME = "SharedPreference"
    private const val MODE = Context.MODE_PRIVATE
    private lateinit var preferences: SharedPreferences

    private val VALUE = Pair("value", true)

    fun init(context: Context) {
        preferences = context.getSharedPreferences(NAME, MODE)
    }

    private inline fun SharedPreferences.edit(operation: (SharedPreferences.Editor) -> Unit) {
        val editor = edit()
        operation(editor)
        editor.apply()
    }

    var value: Boolean
        get() = preferences.getBoolean(VALUE.first, VALUE.second)
        set(value) = preferences.edit {
            it.putBoolean(VALUE.first, value)
        }
}
```

우선 싱글톤으로 사용하기 위해 SharedPreference를 이런 식으로 정의해주면 되는데 여기서 NAME은 저장되는 이름이고 MODE에서 Context.MODE_PRIVATE로 설정한 것은 다른 앱이나 이런 곳에서 우리 SharedPreference 정보를 접근하지 못하게 세팅한 것이다

이번 예제에선 간단히 value라는 Boolean 값을 저장한다고 가정하겠다

`GlobalApplication`

```kotlin
class GlobalApplication : Application() {
    override fun onCreate() {
        super.onCreate()
        SharedPreference.init(this)
    }
}
```

SharedPreference를 만들었다면 그 다음에는 이렇게 GlobalApplication을 하나 만들어서 SharedPreference 초기화 시켜준다

`Manifest` 

```kotlin
<application
        android:name=".GlobalApplication"
        ...>
        
 </application>
```

마지막으로 Manifest 파일에 들어가서 이런 식으로 application name에 GlobalApplication를 추가해주면 끝이다

사용할 때는 

~~~kotlin
SharedPreference.value
~~~

이런 식으로 접근하면 된다

## 기본

~~~kotlin
val sharedPref = activity?.getSharedPreferences(
        getString(R.string.preference_file_key), Context.MODE_PRIVATE)

// 쓰기
val sharedPref = activity?.getPreferences(Context.MODE_PRIVATE) ?: return
with (sharedPref.edit()) {
    putInt(getString(R.string.saved_high_score_key), newHighScore)
    apply()
}

// 읽기

val sharedPref = activity?.getPreferences(Context.MODE_PRIVATE) ?: return
val defaultValue = resources.getInteger(R.integer.saved_high_score_default_key)
val highScore = sharedPref.getInt(getString(R.string.saved_high_score_key), defaultValue)
~~~

물론 이런 식으로도 사용이 가능하다
