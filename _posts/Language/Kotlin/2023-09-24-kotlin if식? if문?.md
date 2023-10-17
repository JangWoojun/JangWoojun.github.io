---
title: Kotlin if식? if문?
date: 2023-09-24 21:05:55 +/-0000
categories: [Language, Kotlin]
tags: [kotlin]
toc: true
pin: true
---

# Kotlin if식? if문?

코틀린은 현대적이면서도 간결한 언어 특성을 가진 언어로 많은 기능과 장점을 가지고 있는데 그 중에서도 이번엔 코틀린의 if에 대해서 알아보려고 한다

전통적인 프로그래밍 언어(Java, C, C++, ETC...)에서는 if를 주로 조건부 명령문으로 사용했지만 코틀린에서는 if를 표현식으로 사용할 수 있다 

말로는 잘 이해되지 않을 수 있으니 예시 코드로 나타내면

~~~java
int a = 5;
int b = 3;
int max;

if (a > b) {
    max = a;
} else {
    max = b;
}

System.out.println(max);
~~~

위 자바 if문 코드 같이 정통적인 프로그래밍 언어에서는 해당 방식으로 if를 쓰지만


~~~kotlin
val a = 5
val b = 3
val max = if (a > b) a else b

println(max)
~~~

위처럼 코틀린은 if식을 통해 훨신 더 간결하고 읽기 쉽게 작성할 수 있으며 if식은 표현식으로서 동작하기에 값을 반환할 수 있다는 특징으로 

if의 결과를 변수에 할당하거나 다른 표현식의 일부로 사용할 수 있어, 복잡한 연산이나 로직을 간결하게 표현할 수 있다는 장점을 가진다

하지만

~~~kotlin
val a = 5;
val b = 3;
var max: Int

if (a > b) {
    max = a
} else {
    max = b
}

println(max)
~~~

코틀린 또한 정통적인 프로그래밍 언어처럼 if문도 사용할 수 있기에 사용하는 목적이나 취향에 맞게 사용하면 될 거 같다

마지막으로 if문과 if식에 대해 정리해보면

### if문 (Statement)
정의: 조건에 따라 특정 코드 블록을 실행하는 제어 구조로 값을 반환하지 않으므로 일반적으로 결과를 변수에 할당할 수 없다
목적: 코드의 실행 흐름을 제어한다
반환 값: 없음
예시:
~~~java
int a = 10, b = 20;
if (a > b) {
    System.out.println("a가 b보다 큼");
} else {
    System.out.println("b가 a보다 크거나 같음");
}
~~~

### if식 (Expression)
정의: 조건에 따라 값을 반환하는 구조로 if의 결과를 변수에 할당하거나 다른 표현식의 일부로 사용할 수 있다
목적: 코드의 실행 흐름을 제어하면서 특정 값을 평가하거나 반환한다
반환 값: 조건에 따라 평가된 값
예시:
~~~kotlin
val a = 10
val b = 20
val max = if (a > b) a else b
println(max)
~~~

### 주요 차이점:
값 반환: if문은 값을 반환하지 않지만 if식은 값을 반환하며 이 값을 다른 변수에 할당하거나 표현식 내에서 사용할 수 있다
사용 방법: if문은 주로 명령을 실행하기 위해 사용되며 if식은 값이 필요한 곳에서 사용된다
언어 지원: 모든 언어가 if식을 지원하지 않지만 Kotlin, Scala, Rust와 같은 일부 현대적인 언어에서는 이를 지원하고 있다

이번에는 나도 모르게 안드로이드 스튜디오에 코드 정리 추천으로 사용하고 코드가 if식이란 걸 알게 되고 이에 대해 공부하고 해당 내용을 정리해봤다