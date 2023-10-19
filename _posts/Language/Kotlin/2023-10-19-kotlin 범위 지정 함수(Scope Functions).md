---
title: Kotlin 범위 지정 함수(Scope Functions)
date: 2023-10-19 20:05:55 +/-0000
categories: [Language, Kotlin]
tags: [kotlin]
toc: true
pin: true
---

# Kotlin 범위 지정 함수(Scope Functions)

코틀린은 현대적이면서도 간결한 언어 특성을 가진 언어로 많은 기능과 장점을 가지고 있는데 그 중에서도 이번엔 사람들이 많이 헷갈려하는 코틀린의 범위 지정 함수에 대해 알아보려고 한다

## 범위 지정 함수(Scope Functions)란?

우선 범위 지정 함수(Scope Functions)란 범위특정 객체에 대한 연산을 지정된 범위(scope) 내에서 수행할 수 있게 해주는 함수로

그 종류로는 let, run, with, apply, also 이렇게 5가지가 있다 그렇다면 각각의 차이는 무엇일까?

크게 범위 지정 함수(Scope Functions)를 두 가지 기준으로 나눌 수 있는데 첫 번째는 반환 값이고 두 번째는 객체 참조 방식이다 참고로 범위 지정 함수(Scope Functions)의 객체 참조 방식에 대해서는 [이전 글](https://jangwoojun.github.io/posts/kotlin-it-VS-this/)에서 자세히 설명해놨으니 여기서 확인해보자

어쨌든 본론으로 돌아와서 각각의 기준으로 범위 지정 함수(Scope Functions)를 나누면 아래와 같다

### 반환 값에 따라 분류:
* 람다 결과를 반환하는 함수: let, run, with
* 호출한 객체를 반환하는 함수: apply, also

### 객체 참조 방식에 따라 분류:
* this를 사용해 객체를 참조하는 함수: run, with, apply
* it을 사용해 객체를 참조하는 함수: let, also

그렇다면 이제 각각의 범위 지정 함수(Scope Functions)에 대해 알아보자

## let

~~~kotlin
val name: String? = "Kotlin"
val length = name?.let { it.length } ?: 0
~~~

우선 처음으로는 let에 대해 설명하겠다 let은 주로 위 코드와 같이 널(null) 검사 및 변환 작업에 사용되며 it을 사용하여 객체를 참조하고 마지막 코드를 리턴한다

## run

~~~kotlin
val result = "Hello".run {
    this + " World"
}
~~~

다음으로 run은 위 코드와 같이 주로 객체의 멤버에 접근할 필요가 있을 때 사용되며 this를 사용하여 객체를 참조하고 마지막 코드를 리턴한다

참고로 run은 범위 지정 함수(Scope Functions)가 아닌 표준 라이브러리에서 최상위 함수로도 제공되기에 특정 코드 블럭을 실행시키기 위해 사용될 수 있지만 이번 주제와는 맞지 않기에 생략하겠다

## with

~~~kotlin
val list = mutableListOf(1, 2, 3)
with(list) {
    add(4)
    size
}
~~~

다음 소개할 범위 지정 함수(Scope Functions)는 with으로 run과 비슷하지만 첫 번째 파라미터로 객체를 받는다는 특징을 가지고 있으며 run과 마찬가지로 this를 사용하여 객체를 참조하고 마지막 코드를 리턴한다

## apply

~~~kotlin
data class Person(var name: String, var age: Int)
val person = Person("", 0).apply {
    name = "John"
    age = 25
}
~~~

네 번째로 소개할 범위 지정 함수(Scope Functions)는 apply로 객체의 초기화나 설정에 주로 사용되며 this를 사용하여 객체를 참조하고 앞에서 소개한 범위 지정 함수(Scope Functions)와 다르게 객체 자체를 반환한다

## also

~~~kotlin
val numbers = mutableListOf(1, 2, 3).also {
    it.add(4)
}
~~~

마지막으로 소개할 범위 지정 함수(Scope Functions)는 also로 let과 유사하지만 객체 자체를 반환하며 it이 기본 파라미터 이름으로 사용된다 이러한 also는 주로 추가적 연산이 필요할 때 사용된다

## 요약

<table border="1" cellpadding="5" cellspacing="0">
    <thead>
        <tr>
            <th>함수</th>
            <th>객체 참조</th>
            <th>반환값</th>
            <th>주요 사용 사례</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>let</code></td>
            <td><code>it</code></td>
            <td>람다 결과</td>
            <td>null 체크, 변환</td>
        </tr>
        <tr>
            <td><code>run</code></td>
            <td><code>this</code></td>
            <td>람다 결과</td>
            <td>객체의 멤버 접근</td>
        </tr>
        <tr>
            <td><code>with</code></td>
            <td><code>this</code></td>
            <td>람다 결과</td>
            <td>객체의 멤버 접근</td>
        </tr>
        <tr>
            <td><code>apply</code></td>
            <td><code>this</code></td>
            <td>객체 자체</td>
            <td>객체 초기화</td>
        </tr>
        <tr>
            <td><code>also</code></td>
            <td><code>it</code></td>
            <td>객체 자체</td>
            <td>추가 연산</td>
        </tr>
    </tbody>
</table>

이렇게 이번에 사람들이 많이 헷갈려하면서 쓰고 있는 코틀린의 범위 지정 함수에 대해 알아봤다 그동안 나 또한 모르고 그냥 사용하고 있던 범위 지정 함수(Scope Functions)들에 대해 정리하면서 많이 배웠다