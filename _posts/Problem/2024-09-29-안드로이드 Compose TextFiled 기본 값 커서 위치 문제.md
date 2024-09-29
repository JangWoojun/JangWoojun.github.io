---
title: 안드로이드 Compose TextFiled 기본 값 커서 위치 문제
date: 2024-09-29 07:10:00 +/-0000
categories: [Problem, Android]
tags: [android, problem, compose]
toc: true
pin: true
---

최근 안드로이드 Compose 안드로이드 앱 개발을 시작하게 되었는데 단순 UI 구현 부분은 기존 XML보다 빨라서 좋았으나 한 번씩 생각한 것과 다르게 동작이되거나 문제가 생기면 해결하는데 오래 걸리는 문제들이 있었다

서론은 여기까지 하도록 하고 최근에 겪은 문제인 Compose TextFiled 커서 위치 문제 해결 방법애 대해 소개하겠다

# 문제 상황

보통 Compose에서 TextFile를 이런 식으로 사용하게 되는데

~~~kotlin
var value by remember { mutableStateOf("") }
TextField(
    value = value,
    onValueChange = { newValue -> value = newValue },
    modifier = modifier
)
~~~

여기서 Default 값을 지정할 일이 생겨 지정하니

~~~kotlin
var value by remember { mutableStateOf(name) }
TextField(
    value = value,
    onValueChange = { newValue -> value = newValue },
    modifier = modifier
)
~~~

클릭 했을 때 Default 값인 name 뒤에 커서가 생기는 것이 아닌 처음에 생기는 것이였다

# 해결법

해결 방법은 간단한데 value를 String이 아닌 TextFieldValue로 사용해서 TextRange를 지정해주면 되었다

~~~kotlin
var value by remember { mutableStateOf(TextFieldValue(name, TextRange(name.length))) }

TextField(
    value = value,
    onValueChange = { newValue ->
        value = newValue.copy(selection = TextRange(newValue.text.length))
    }
)
~~~