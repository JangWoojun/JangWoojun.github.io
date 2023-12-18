---
title: Kotlin에서 Long보다 큰 수를 연산하려면?
date: 2023-12-18 17:00:55 +/-0000
categories: [Language, Kotlin]
tags: [kotlin]
toc: true
pin: true
---

안드로이드 개발 중 초보가 처음으로 할만한 프로젝트를 고른다면 꼭 나오는 것 중 하나가 계산기 앱이다 하지만 계산기 앱을 개발하다보면 Long으로도 커버가 되지 않을 만큼 큰 숫자를 연산해야 할 일이 생기는데 이것을 계산할 수 있는 숫자를 제한하는 방법으로도 해결할 수 있지만 이는 근본적인 해결 방법이 아니기에 제외하고

뭐 이 밖에도 종종 Kotlin을 통해 개발을 하다보면 Long 보다 큰 숫자 연산이 필요할 때가 생기는데 그래서 이번 글에서는 이러한 Long 보다 큰 연산을 하는 방법에 대해 알아보려고 한다

# Long 보다 큰 숫자 연산

우선 Long 보다 큰 숫자 연산에 대해 알아보기 전에 Long에 범위 부터 살펴보면 Long 타입의 범위는 다음과 같다

* 최소값: -2^63
* 최대값: 2^63 - 1

구체적으로 숫자로 나타내면

* 최소값: -9,223,372,036,854,775,808
* 최대값: 9,223,372,036,854,775,807

그냥 딱 보기에도 어마어마 하게 크지만 이를 벗어난 크기를 가진 수를 연산하고 담아야 할 일이 반드시 존재한다 이것을 해결하기 위해 많은 방법들이 존재하지만 이번 글에선 가장 쉬운 방법이라고 생각되는 java.math 패키지의 BigInteger와 BigDecimal를 사용하는 방법을 소개하려고 한다

## BigInteger

처음으로는 BigInteger에 대해 소개해보겠다 BigInteger는 매우 큰 정수를 다룰 때 사용되는 클래스로 기본 정수 타입으로 처리할 수 없는 크기의 정수를 저장하고 연산하는 데 유용하게 사용된다

코드로 한번 살펴보면

~~~kotlin
import java.math.BigInteger

fun main() {
    val bigInt1 = BigInteger("12345678901234567890")
    val bigInt2 = BigInteger("98765432109876543210")

    // 덧셈
    val sum = bigInt1 + bigInt2

    // 뺄셈
    val difference = bigInt1 - bigInt2

    // 곱셈
    val product = bigInt1 * bigInt2

    // 나눗셈
    val quotient = bigInt1 / bigInt2

    println("덧셈: $sum")
    println("뺄셈: $difference")
    println("곱셈: $product")
    println("나눗셈: $quotient")
}
~~~

Kotlin에서는 연산자 오버로딩이 지원되기 때문에 +, -, *, /와 같은 연산자를 직접 사용할 수 있어 이런 식으로 사용할 수 있다

## BigDecimal

다음으로는 BigDecimal로 BigDecimal은 정밀한 부동 소수점 연산에 사용되는 클래스로 보통 금융 계산과 같이 정확한 소수점 연산이 필요한 경우에 매우 유용하게 사용할 수 있다

이제 도 코드로 살펴보면

~~~kotlin
import java.math.BigDecimal

fun main() {
    val bigDec1 = BigDecimal("12345.67890")
    val bigDec2 = BigDecimal("98765.43210")

    // 덧셈
    val sum = bigDec1 + bigDec2

    // 뺄셈
    val difference = bigDec1 - bigDec2

    // 곱셈
    val product = bigDec1 * bigDec2

    // 나눗셈
    val quotient1 = bigDec1.divide(bigDec2, 5, BigDecimal.ROUND_HALF_UP)
    val quotient2 = bigDec1 / bigDec2


    println("덧셈: $sum")
    println("뺄셈: $difference")
    println("곱셈: $product")
    println("나눗셈1: $quotient1")
    println("나눗셈2: $quotient2")

}
~~~

이렇게 사용할 수 있는데 눈치 챘겠지만 나눗셈의 경우 BigDecimal은 divide를 통해 나눗셈의 정확도와 반올림 모드를 지정할 수도 있다

## BigInteger와 BigDecimal 뜯어보기

그렇다면 이러한 BigInteger와 BigDecimal는 어떻게 만들어져 있을까? 이를 살펴보면


### BigInteger 뜯어보기

우선 BigInteger는 정수를 내부적으로 int 배열로 표현하는데 각 int는 정수의 일부를 나타내며 이 배열을 사용하여 아주 큰 정수를 표현한다 배열의 길이는 필요에 따라 늘어나거나 줄어들 수 있으며 이를 통해 사실상 무제한의 크기를 가진 정수를 표현하고 있다

그리고 연산에 대해 살펴보면 BigInteger는 일반 정수 연산과 유사한 방식으로 연산을 수행한다 더하기, 빼기, 곱하기, 나누기 등의 연산은 내부적인 알고리즘을 통해 수행되며 이 때 각 int 배열의 요소들을 조작하여 결과를 도출한다 예를 들면 덧셈은 배열의 각 요소를 순차적으로 더하고, 자릿수 올림을 처리하는 방식을 들 수 있겠다


### BigDecimal 뜯어보기

BigDecimal은 내부적으로 두 부분으로 구성되어 있다 하나는 정수 값을 나타내는 BigInteger 다른 하나는 소수점의 위치를 나타내는 스케일(scale)이다 여기서 스케일은 소수점 이하 몇 자리까지 표현할지를 결정하는 역할을 한다

다음으로 BigDecimal의 연산 방법을 살펴보면 BigDecimal은 정확한 소수점 계산을 보장하기 위해 표준 부동 소수점 연산에서 발생할 수 있는 반올림 오류를 방지하며 필요한 경우 사용자가 지정한 반올림 모드를 사용하여 결과를 반올림한다 예를 들면 나눗셈 연산에서는 결과의 소수점 이하 자릿수와 반올림 방식을 지정할 수 있다