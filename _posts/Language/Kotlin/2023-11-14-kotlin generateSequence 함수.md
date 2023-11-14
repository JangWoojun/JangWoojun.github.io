---
title: Kotlin generateSequence 함수
date: 2023-11-14 18:05:55 +/-0000
categories: [Language, Kotlin]
tags: [kotlin]
toc: true
pin: true
---

코틀린은 현대적이면서도 간결한 언어 특성을 가진 언어로 많은 기능과 장점을 가지고 언어 이번 글에선 이러한 코틀린에 존재하는 여러 함수 중 하나인 generateSequence 함수의 개념과 사용법 및 generateSequence 예제 코드등을 알아보려한다

## 무한 시퀀스란 무엇인가?

우선 generateSequence 대해 알기 전 무한 시쿼스가 무엇인 지 먼저 살펴보면 
무한 시퀀스는 그 이름에서 알 수 있듯이 끝이 없는 연속된 데이터의 시퀀스로 실제로 모든 요소를 메모리에 저장하지 않기 때문에 무한한 양의 데이터를 다룰 수 있다 

또한 이러한 무한 시퀀스는 lazy evaluation 방식을 사용해 실제로 해당 요소에 접근할 때만 계산을 수행하여 메모리를 효율적으로 사용해 필요에 따라 어떤 길이든지 시퀀스를 생성할 수 있는 유연성을 제공한다

## generateSequence란?

다음으로 이제 본론으로 돌아와 generateSequence에 살펴보면 generateSequence는 코틀린의 표준 라이브러리에 포함된 함수로 연속된 값을 순차적으로 생성하는 무한 시퀀스를 만드는데 사용되며 특정 규칙에 따라 값을 생성할 수 있다 물론 generateSequence 또한 lazy evaluation 방식을 사용해 효율적으로 사용한다

기본 사용법을 살펴보면 아래와 같은데

~~~kotlin
val sequence = generateSequence(초기값) { 계산식 }
~~~

여기서 초기값은 시퀀스의 첫 번째 요이고 계산식은 다음 요소를 계산하는 데 사용된다

## 예제 코드

### 간단한 무한 수열 생성

~~~kotlin
val numbers = generateSequence(1) { it + 1 }
println(numbers.take(5).toList()) // [1, 2, 3, 4, 5]
~~~

이 예제는 1부터 시작하여 계속 1씩 증가하는 무한 수열을 생성하는 코드이다

### 피보나치 수열 생성

~~~kotlin
val fibonacci = generateSequence(Pair(0, 1)) { Pair(it.second, it.first + it.second) }
    .map { it.first }
println(fibonacci.take(10).toList()) // 피보나치 수열의 첫 10개 요소
~~~
이 코드는 각 단계에서 새로운 숫자는 이전 두 숫자의 합으로 계산하는 즉, 피보나치 수열을 만드는 코드이다
