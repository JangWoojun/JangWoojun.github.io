---
title: Dart에서 mixin 다이아몬드 문제 처리
date: 2023-10-05 12:20:55 +/-0000
categories: [Language, DART]
tags: [dart]
toc: true
pin: true
---

## 다중 상속에서 다이아몬드 문제란?

여러 언어에서 다중 상속을 직접적으로 제공하지 않거나 특별한 규칙 또는 알고리즘을 적용하는데 이는 다중 상속으로 나타날 수 있는 다이아몬드 문제 때문인데

여기서 다이아몬드 문제란 아래 설명을 보면 이해하기 쉽다

~~~
    A
   / \
  B   C
   \ /
    D
~~~


위 구조와 같이 두 개의 클래스 B와 C가 A 클래스를 상속받고 D 클래스가 B와 C를 동시에 상속받는 구조에서

A 클래스에 정의된 메서드나 변수에 접근하려고 할 때 B와 C 중 어느 경로를 통해 접근해야 하는지 모호하다는 문제이다 만약 자세히 다이아몬드 문제에 대해 알고 싶다면

[해당 글 참고](https://jangwoojun.github.io/posts/%EB%8B%A4%EC%A4%91-%EC%83%81%EC%86%8D%EC%97%90%EC%84%9C-%EB%8B%A4%EC%9D%B4%EC%95%84%EB%AA%AC%EB%93%9C-%EB%AC%B8%EC%A0%9C%EB%9E%80/)

## Dart에서 다이아몬드 문제를 방지하는 법

Dart에서는 직접적으로 다중상속을 지원하지 않고 mixin를 통해 다중 상속과 비슷한 방식으로 코드 재사용을 가능하게 하지만, 명확한 규칙과 제한사항으로 다중 상속이 갖는 문제점을 회피하고 있다

그렇다면 Dart에서 다이아몬드 문제가 발생할 수 있는 코드를 사용하면 어떻게 될까?

코드로 함께 확인해보자

~~~dart
mixin Walk1 {
  void walk() {
    print("걷기1");
  }
}

mixin Walk2 {
  void walk() {
    print("걷기2");
  }
}

mixin Walk3 {
  void walk() {
    print("걷기3");
  }
}

class Human with Walk1, Walk2, Walk3 {}

void main() {
  Human human = Human();
  human.walk();
}
~~~

위 코드를 보면 다이아몬드 문제가 일어난다고 생각할 수 있으나 Dart에서는 위에서 말했던 것과 같이 명확한 규칙과 제한사항으로 다중 상속이 갖는 문제점을 회피하는데

Dart에선 마지막으로 포함된 mixin의 구현을 우선시 하는 방식으로 다이아몬드 문제를 방지하기에 위 코드에선 Walk3에 walk가 사용되어 걷기3가 출력된다 