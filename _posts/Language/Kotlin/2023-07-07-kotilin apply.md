---
title: Kotlin apply
date: 2023-07-07 11:55:55 +/-0000
categories: [Language, Kotlin]
tags: [kotlin]
toc: true
pin: true
---

# Kotlin apply

코틀린에서 사용되는 apply 함수란? 객체 초기화 블록을 실행하는 데 사용되는 표준 함수로 apply를 사용하면 객체의 속성을 초기화하거나 설정하는 작업을 간결하게 수행할 수 있다

~~~kotlin
apply {
    // 객체 초기화 코드
}
~~~

위 코드처럼 apply 함수를 사용하며 apply 블록 내에서는 주어진 객체의 속성을 직접 참조하여 수정할 수 있다 apply 함수가 실행되면 해당 객체가 블록 내에서 this로 참조된다는 특징이 있다

apply 함수를 사용하는 큰 이유는 apply 함수를 사용하면 중간 단계 없이 객체를 초기화할 수 있다는 점으로 코드의 가독성을 향상된다는 장점을 가지고 있다

코드로 예시를 들어보자면

~~~kotlin
data class Person(var name: String, var age: Int, var city: String)

val person = Person("Woojun Jang", 17, "Seoul").apply {
    name = "Jang Woojun"
    age = 18
    city = "Seoul Eunpyeong"
}
~~~

위와 같이 apply 함수를 사용하여 객체를 초기화할 수 있다

안드로이드에서 findViewById 대신 viewbinding을 사용할 때 

~~~kotlin
binding.textviewA.text = "a"
binding.textviewB.text = "b"
~~~

위와 같은 방식으로 사용하는게 귀찮아

~~~kotlin
binding.apply {
    textviewA.text = "a"
    textviewB.text = "b"
}
~~~

첫 번째 방법을 간편하게 사용할 방법을 찾다가 위와 같이 apply로 단순화 시키는 방법을 알게 되어 
그 이후 쭉 이런식으로 사용하고 있었는데 

문득 apply가 뭐길래 binding을 여러 번 쓰지 않아도 되는 걸까?라는 생각에 apply에 대해 알아 보았다