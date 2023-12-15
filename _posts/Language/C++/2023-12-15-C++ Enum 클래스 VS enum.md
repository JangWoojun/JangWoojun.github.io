---
title: C++ Enum 클래스 VS enum
date: 2023-12-15 22:09:55 +/-0000
categories: [Language, CPP]
tags: [cpp]
toc: true
pin: true
---

C++을 사용하더보면 Enum 클래스를 만나게 되는데 Enum 클래스는 열거형 타입을 더욱 편하게 다룰 수 있게 해주는 C++의 기능이라고 생각하면 쉽다 이번 글에서는 이러한 Enum 클래스에 대해 소개해보겠다

## Enum 클래스란?

앞서 말했다시피 Enum 클래스는 기존의 C나 C++의 열거형보다 더 편하고로 열거형을 정의할 수 있게 해주는 기능으로 기존의 열거형은 주로 int 기반으로만 동작하지만 Enum 클래스는 이러한 제약을 벗어나 타입 안정성과 명확한 스코프를 가지고 있어 다양하게 사용이 가능하다

## 열거형 vs Enum 클래스

Enum 클래스에 대해 더 잘 알기 위해 기존 열거형과 비교하자면

우선 열거형은

~~~cpp
enum Color { RED, GREEN, BLUE };

void printColor(Color color) {
    if (color == RED) {
        // ...
    }
}
~~~

이렇게 선언하고 사용한다 이러한 열거형의 문제로는 대표적으로 열거형 멤버들이 전역 네임스페이스에 속한다는 점과 암시적 타입 변환으로 인한 타입 안전성 문제가 존재한다

하지만 Enum 클래스는

~~~cpp
enum class Color { RED, GREEN, BLUE };

void printColor(Color color) {
    if (color == Color::RED) {
        // ...
    }
}

int main() {
    Color color = Color::GREEN;
    printColor(color);
}
~~~

이렇게 선언하고 사용할 수 있으며 Enum 클래스는 각 열거형 값에 대해 

~~~cpp
enum class Color { Red, Green, Blue };
enum class Size { Small, Medium, Large };
~~~

별도의 네임스페이스를 제공하여 충돌을 방지하고 타입 안전성을 강화하며 

~~~cpp
enum class State { Idle, Running, Paused, Stopped };
State currentState = State::Running;
~~~

각 열거형 값에 명시적인 스코프를 제공하여 코드의 가독성을 향상시킨다

~~~cpp
enum class MyEnum : char { A, B, C };
~~~

또한 앞서 말했듯 Enum 클래스는 기본적으로 int 기반으로 동작하지만 필요에 따라 다른 기본 타임으로도 지정할 수 있고 

~~~cpp
enum class Fruit { APPLE, BANANA };
enum class Color { RED, GREEN };

void example() {
    Fruit fruit = Fruit::APPLE;
    Color color = Color::RED;

    // 컴파일 에러: fruit과 color는 서로 다른 타입
    // if (fruit == color) {
    //     // ...
    // }
}
~~~

암시적 타입 변환 방지하기에 예상치 못한 오류를 막을 수 있다

## Enum 클래스 활용

다음으로 Enum 클래스가 좋다는 건 알겠는데 Enum 클래스는 어떨 때 활용해야 하며 기존 enum은 언제 사용해야 할까?

### Enum Class 사용

1. 타입 안전성이 중요할 때: enum class는 열거형 값이 다른 타입으로 암시적으로 변환되는 것을 방지하기에 타입 안정성이 중요한 상황에서 사용한다

2. 명확한 스코프가 필요할 때: enum class는 네이스페이스를 오염시키지 않기에 이름 충돌이 일어날 수 있다면 Enum 클래스를 사용한다

### 기존 enum 사용

1. 간단한 열거가 필요할 때: 기존 enum은 작성이 Enum 클랫에 비해 간단하고 열거형 값에 직접 접근할 수 있기에 간단히 사용하다면 enum을 사용하는게 낫다

2. 레거시 코드와의 호환성이 필요할 때: 기존의 레거시 시스템이나 라이브러리들은 대부분 기존 enum을 사용하고 있을 수 있기에 이들과의 호환을 고려해야 할 때는 기존 enum을 사용해야 한다

3. 퍼포먼스에 민감한 상황: 일반적으로 enum class와 enum 사이에는 성능 차이가 거의 없지만 매우 성능에 민감한 상황에서는 더 단순한 enum을 사용하는 것이 미세하게 낫다 하지만 이럴 경우는 드물다

### 종합

대부분의 상황에서는 새로 추가된 Enum 클래스를 사용하는 것이 기존 enum과 비해 타입 안전성, 명확한 스코핑, 강화된 형 검사가 있어 더 안정적이고 유지보수하기 쉬운 코드를 작성할 수 있다

하지만 특정 상황(간단한 열거, 레거시 코드 호환성, 미세한 퍼포먼스 최적화)에서는 기존의 enum이 더 적합할 수 있기에 상황에 맞게 써야 한다 

## 결론

Enum 클래스는 C++11 이후로 도입된 기능으로 기존 enum에 비해 기능적으로 상위호환 (더 나은 타입 안전성과 명확한 스코프)을 제공하기에 개발 중 열거형이 필요할 때는 기존의 enum과 새로운 Enum 클래스 중 뭘 써야 할 지 잘 모르겠다면 Enum 클래스를 쓰면 된다



