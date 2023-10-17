---
title: Kotlin it VS this
date: 2023-10-17 20:05:55 +/-0000
categories: [Language, Kotlin]
tags: [kotlin]
toc: true
pin: true
---

# Kotlin it VS this

코틀린은 현대적이면서도 간결한 언어 특성을 가진 언어로 많은 기능과 장점을 가지고 있는데 그 중에서도 이번엔 사람들이 많이 헷갈려하는 코틀린의 범위 지정 함수(Scope Funciton)의 it과 this에 대해서 알아보려고 한다

## it이란?

우선 it에 대해 알아보자 it은 범위 지정 함수 중 let과 also에서 사용되는 암시적 파라미터로 it은 람다 인자로 전달되는 현재 객체를 참조한다

글로만 보면 잘 이해되지 않을 수 있으니 코드와 함께 보자 

~~~kotlin
fun main(){
	val user = User("it", 1)
	user.let {
        it.name
    }
}

data class User(val name: String, val age: Int)
~~~

예를 들어 User 데이터 클래스에 있는 name을 접근하기 위해서는 it은 it.name 이런 식으로 접근해야 하며

~~~kotlin
fun main(){
	val user = User("it", 1)
	user.let { user ->
        user.name
    }
}

data class User(val name: String, val age: Int)
~~~

it 말고 'user'처럼 명시적으로 원하는 대로 바꿔서 사용할 수 있다

## this

다음으로 this에 대해 알아보자면 this는 범위 지정 함수 중 run, apply, with에서 사용되며 람다 본문 내에서 객체 자신을 참조한다 

이 또한 글로만 보면 이해가 잘 안될테니 코드와 함께 살펴보자

~~~kotlin
fun main(){
	val user = User("this", 2)
	user.apply {
        this.name
    }
}

data class User(val name: String, val age: Int)
~~~

예를 들어 User 데이터 클래스에 있는 name을 접근하기 위해서는 this.name 이런 식으로 접근하며

it과 달리 명시적으로 원하는 대로 바꿔서 사용할 수 없다

~~~kotlin
fun main(){
	val user = User("this", 2)
	user.apply {
        name
    }
}

data class User(val name: String, val age: Int)
~~~

하지만 this를 사용할 때는 this를 생략해서 사용하는 것이 가능하다

## 결론

범위 지정 함수를 사용할 때 it이나 this나 크게 다르지 않기에 둘의 차이를 크게 고려하지 않아도 되며 범위 지정 함수 선택에서 고려해야 할 것으로 중요한 것은 함수의 반환 값, 컨벤션, 코드 가독성, 사용 목적이다