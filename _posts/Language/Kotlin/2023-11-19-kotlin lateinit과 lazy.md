---
title: Kotlin lateinit과 lazy
date: 2023-11-19 13:50:55 +/-0000
categories: [Language, Kotlin]
tags: [kotlin]
toc: true
pin: true
---

코틀린은 안드로이드 개발을 포함한 다양한 영역에서 널리 사용되는 현대적인 프로그래밍 언어로 현대적 언어답게 초기화 지연을 지원한다 여기서 초기화 지연은 말 그대로 객체의 초기화를 늦게 하는 것으로

~~~kotlin
var age: Int? = null
~~~

위 코드처럼 age라는 변수를 사용하는데 처음에는 age에 값을 모르고 나중에 설정할 예정일 때 만약 이 age를 나중에 꼭 초기화할 예정이라면 굳이 ?. 또는 !!.로 접근해야 하는 널러블 타입으로 설정하기 싫을 것이다

이때 사용할 수 있는 것이 초기화 지연으로 그래서 이번 글에서는 코틀린에서 초기화 지연할 때 사용되는 lateinit과 lazy에 대해 알아볼 것이다

## lateinit이란?

lateinit 키워드는 주로 의존성 주입(Dependency Injection)이나 단위 테스트에서 사용되는 키워드로 변수가 선언 시점이 아닌, 나중에 초기화될 것임을 명시한다고 한다

코드로 확인해보면

~~~kotlin
class MyClass {
    lateinit var dependency: DependencyClass

    fun initialize() {
        dependency = DependencyClass()
    }
}

fun main() {
    val myClass = MyClass()
    myClass.initialize()
}
~~~

위와 같이 lateinit 를 var 앞에 붙여서 사용하며 lateinit는 나중에 값을 꼭 변경시켜야 하기에 val로는 사용할 수 없다 또한 Int, Long 등과 같은 기본 타입에는 사용할 수 없기에 무슨 일이 있어도 꼭 Int로 사용하고 싶다 Integer 같은 참조 타입으로 사용해야 한다

그렇다면 만약에 꼭 초기화되야 하는 lateinit을 초기화 전에 접근하면 어떻게 될까?
만약 초기화 전 lateinit에 접근하면 **UninitializedPropertyAccessException** 오류가 발생하기 때문에 꼭 초기화해야 하는 변수로 초기화 하지 못해 발생할 수 있는 잠재적 오류를 방지할 수 있다

추가적으로 ::변수명.isInitialized을 사용하면 lateinit이 초기화 되었는지도 확인할 수 있다

~~~kotlin
class SampleClass {
    lateinit var sampleData: String

    fun isInitialized(): Boolean {
        return ::sampleData.isInitialized
    }
}

fun main() {
    val sample = SampleClass()

    // 초기화 전 상태 확인
    println("sampleData 초기화: ${sample.isInitialized()}") // false

    // 변수 초기화
    sample.sampleData = "Hello Kotlin"

    // 초기화 후 상태 확인
    println("sampleData 초기화: ${sample.isInitialized()}") // true
}
~~~

::변수명.isInitialized을 사용하여 초기화 여부를 파악하는 예제 코드

## lazy이란?

다음으로 lazy에 대해 알아보자 lazy는 호출 시점에 값이 초기화되고, 이후 호출될 때는 이미 저장된 값을 반환하는 기능을 제공하는 키워드로 하는 역할에서 유출할 수 있듯이 주로 자원이 많이 소모되는 객체나 계산에 사용된다

이제 코드로 확인해보자

~~~kotlin
val lazyValue: String by lazy {
    println("초기화!")
    "Hello"
}

fun main() {
    print(lazyValue) // 초기화! 이후 Hello 출력
}
~~~

위 코드에서 확인할 수 있듯이 lazy는 타입 뒤에 by lazy 람다식을 붙여 사용한다
여기서 알아야 할점은 lazy는 lateinit과 반대로 val에서만 사용 가능하며 앞에서 말했듯 lazy로 선언된 변수는 처음으로 접근하는 시점에 초기화되기에 

이전까지는 메모리에 할당되지 않는다 또한 여러 스레드에서 동시에 접근할 경우에도 한 번만 초기화되고 동기화를 보장하기에 스레드 안정성을 가지고 있다

## 결론

이렇듯 lateinit과 lazy는 둘다 기본적으로 초기화 지연을 위해 사용되는 녀석들이지만 세세히 살펴보면 차이점이 있기에 필요에 따라 잘 선택해 사용해야겠다

마지막으로 정리해보자면

| 기준           | `lazy`                                                 | `lateinit`                                       |
|--------------|--------------------------------------------------------|--------------------------------------------------|
| **변수 타입**    | `val` (변경 불가능)                                    | `var` (변경 가능)                                |
| **타입 제한**   | Nullable 및 Non-nullable 타입에 사용, 기본 타입(Primitive types)에도 사용 가능              | Non-nullable 타입의 참조에만 사용 가능, 기본 타입(Primitive types)에는 사용 불가  |
| **초기화**      | 처음 접근 시 한 번만 초기화                             | 수동으로 초기화 필요                             |
| **스레드 안전** | 기본적으로 스레드 안전 (설정 변경 가능)                 | 스레드 안전하지 않음                             |
| **기본값**      | `lazy` 블록 내에서 정의해야 함                          | 초기화 전까지 기본값 없음                       |
| **재할당**      | 재할당 불가                                            | 초기화 이후 재할당 가능                         |
| **확인 방법**   | `isInitialized` 속성으로 초기화 여부 확인 불가          | `isInitialized` 속성으로 초기화 여부 확인 가능   |
| **사용 예**     | 값이 필요할 때까지 초기화 지연 필요 시                  | 의존성 주입이나 테스트 설정에서 초기화 지연 필요 시 |
