---
title: Kotlin의 Array에 대해 알아보자
date: 2023-12-01 21:20:55 +/-0000
categories: [Language, Kotlin]
tags: [kotlin]
toc: true
pin: true
---

안드로이드 개발이나 서버 개발 등 다양한 곳에서 코틀린을 사용하여 개발을 하다보면 다른 언어와 달리 코틀린에선 Array와 List는 딱히 구분 없이 사용하는 것 같고 특별히 다른 점도 모르겠는데? 하며 구분 없이 사용하는 사람들이 있을 것이다

나 또한 그랬기에 이번 글을 시작으로 코틀린의 Array와 List, MutableList와 ArrayList에 대해 자세히 알아보고 최종적으로는 어떤 점이 다른 지 정리하려고 한다

이번 글을 Array를 다루겠다

# Array

Array는 크기가 고정된 자료 구조로 동일한 타입의 요소를 연속적으로 저장하며 Kotlin에서는 arrayOf() 함수를 사용하여 array를 생성할 수 있다 

코틀린에서 Array를 생성하기 위해서는

~~~kotlin
val numbers = arrayOf(1, 2, 3)
~~~

위와 같이 arrayOf를 통해 선언할 수 있다

## Array의 특징

다음으로 그렇다면 Array는 어떤 특징이 있을까? Array의 대표적 특징으로는 고정된 크기, 인덱스에 인한 빠른 접근, 효율적 메모리 사용이 있는데

각 특징에 대해 조금 더 설명을 덧 붙이자면

* 고정된 크기: 한 번 생성되면 크기를 변경할 수 없다
* 인덱스에 의한 빠른 접근: 요소에 대한 빠른 접근이 가능하다
* 효율적 메모리 사용: 연속된 메모리 할당으로 인해 메모리 사용이 
효율적이다

이렇게 정리할 수 있다

추가적으로 몇 가지만 더 알아보자면 위에서 살펴본 것처럼 Array 는 생성한 순간 크기가 고정되기에 원소 삭제나 추가 등을 사용할 수 없지만 대신 그 안에서 원소 값 변경은 자유롭다

그렇기에 나중에 살펴볼 List와 달리 MutableArray가 존재하지 않고 Array만 존재한다

설명이 말로만 했을 때 잘 이해가 안될 수 있으니 코드로 살펴보면

~~~kotlin
val a = arrayOf(1, 2, 3, 4, 5)
// a.add() 추가 X
// a.remove() 삭제 X
a[0] = 0 // 변경 O
~~~

라고 보면 된다

또한 코틀린에서 Array는 서로 다른 타입이 공존할 수 있으며 그냥 print를 사용해 출력하면 주소만을 출력한다

## Array의 뜯어보기

다음으로 코틀린에서 Array가 어떻게 구현되었는지 살펴보자 우선 코틀린이 JVM(Java Virtual Machine) 위에서 실행된다는 것은 웬만한 코틀린 유저들이면 알 것이다 이러한 JVM을 사용하는 코틀린에서 Array는 자바의 배열로 컴파일 되는 방식을 가지고 있는데

예를 들어 코틀린의 

~~~kotlin
Array<Int>
~~~
는 Java의 Integer[]로 컴파일 된다 하지만 코틀린의 기본 타입 배열(예: IntArray, FloatArray)은 자바의 기본 타입 배열(예: int[], float[])로 직접 매핑되는 방식을 지녔다

또한 자바와 다르게 코틀린에서는 Array 클래스에 대해 다양한 확장 함수를 제공한다 (예: filter, map, forEach)

~~~kotlin
public class Array<T> {

    public inline constructor(size: Int, init: (Int) -> T)

    public operator fun get(index: Int): T

    public operator fun set(index: Int, value: T): Unit

    public val size: Int

    public operator fun iterator(): Iterator<T>
}
~~~

코드로 Array를 뜯어보면 이렇게 구현되어 있다

## Primitive Type Array

Primitive Type Array 그럼 이건 뭘까? Primitive Type Array는 기본 타입에 Array로 

코틀린은 자바와 달리 모든 것이 객체이지만 성능을 위해 프리미티브 타입 배열을 별도로 제공하며 이는 자바의 Primitive 배열과 비슷하게 동작한다

코틀린의 Primitive Type Array의 종류로는

* ByteArray: Byte 타입의 데이터를 저장한다
* ShortArray: Short 타입의 데이터를 저장한다
* IntArray: Int 타입의 데이터를 저장한다
* LongArray: Long 타입의 데이터를 저장한다
* FloatArray: Float 타입의 데이터를 저장한다
* DoubleArray: Double 타입의 데이터를 저장한다
* CharArray: Char 타입의 데이터를 저장한다
* BooleanArray: Boolean 타입의 데이터를 저장한다

가 있다

그렇다면 Primitive Type Array는 기존의 코틀린 Array와 뭐가 다를까?

Primitive Type Array는 각각의 타입에 최적화된 메모리 구조를 가지기에 박싱(Boxing) 오버헤드 없이 기본 자료형 값을 저장할 수 있어 성능상에서 이점을 가지며 앞에서 설명했듯이 자바의 int[], float[] 등의 배열로 매칭되며 객체 참조 대신 실제 값들을 메모리에 직접 저장한다

이러한 Primitive Type Array를 선언하는 방법은 아래와 같다

~~~kotlin
val intArray = IntArray(5) // 크기가 5인 Int 배열 생성
val byteArray = ByteArray(10) // 크기가 10인 Byte 배열 생성
~~~

또한 

~~~kotlin
val intArray = IntArray(5) { i -> i * i } // 각 요소를 제곱수로 초기화
~~~

이렇게 초기화 식을 사용하여 초기화할 수도 있다

### Array vs Primitive Type Array

Array와 Primitive Type Array를 비교해서 정리해보면 아래와 같다

| 특성              | Array                                  | Primitive Type Array                    |
|-------------------|----------------------------------------|-----------------------------------------|
| **타입**          | 제네릭 타입                            | 특정 프리미티브 타입                     |
| **저장 데이터**   | 객체 또는 객체 참조                    | 프리미티브 타입 값                      |
| **박싱/언박싱**   | 필요 (각 요소가 객체로 박싱됨)         | 필요 없음 (직접적인 값 저장)             |
| **메모리 효율성** | 낮음 (추가 메모리 사용)                | 높음 (박싱 오버헤드 없음)                |
| **성능**          | 박싱/언박싱으로 인해 상대적으로 느림   | 박싱/언박싱이 없어 빠름                 |
| **사용 예**       | `Array<Int>`, `Array<String>`          | `IntArray`, `ByteArray`, `CharArray` 등 |
| **생성 방법**     | `arrayOf`, `Array(size) { ... }` 사용  | 예: `IntArray(size)`, `BooleanArray(size)` |
| **접근 방식**     | 인덱스를 통한 접근, 반복 가능          | 인덱스를 통한 접근, 반복 가능           |
| **변경 가능성**   | 변경 가능 (가변적)                     | 변경 가능 (가변적)                      |
| **사용 시나리오** | 다양한 객체를 저장하거나 클래스 타입 배열 필요 시 | 성능이 중요하고 타입이 명확한 숫자 데이터를 다룰 때 |
| **특별한 기능**   | `Array` 클래스 내장 함수 사용 가능     | 각 타입별 특화된 기능과 연산 제공        |
| **크기 조정**     | 불가능 (고정된 크기)                   | 불가능 (고정된 크기)                    |

## Array 장단점

마지막으로 Array의 장단점을 살펴보고 끝내보자

### Array 장점

* 요소들을 실행 중에 변경할 수 있기에 동적인 데이터 조작이 가능하다

* 연속된 메모리 공간을 사용하여 메모리 관리가 편리하며 빠르다

### Array 단점

* 배열의 크기를 변경 불가하기에 크기 변경이 필요할 시 다른 컬렉션을 사용해야 한다

* 요소들을 삭제해도 크기가 줄어들지 않기 때문에 메모리가 낭비될 수도 있다

* List나 Set과 같은 다른 컬렉션 타입에 비해 어느 정도 기능이 제한적인 부분이 있다
