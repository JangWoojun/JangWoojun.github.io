---
title: Java의 StringBuilder란 무엇일까?
date: 2023-12-31 20:00:00 +/-0000
categories: [Language, JAVA]
tags: [java]
toc: true
pin: true
---

안드로이드 앱을 개발하거나 자바나 Kotlin 개발을 하다 보면 문자열을 다루는 경우가 많은데 이때 성능과 효율성을 고려해야 할 때가 있을 것이다 이러한 상황에서 자주 사용되는 클래스 중 하나가 바로 StringBuilder라는 녀석인데 이번 글에서는 이러한 StringBuilder에 대해 자세히 알아보도록 하겠다

# StringBuilder란?

StringBuilder란? StringBuilder는 자바(Java)에서 변경 가능한 문자열을 표현하는 클래스로 java.lang 패키지에 포함되어 있다 이 클래스는 문자열을 추가, 수정, 삭제하는 등의 작업을 빈번하게 수행할 때 사용하면 매우 유용한데 우선 기본 String 클래스의 문제부터 천천히 살펴보자

## 문자열 처리의 문제점

자바에서 문자열을 다룰 때는 String 클래스를 사용하는 것이 일반적이다 하지만 String 객체는 불변(immutable)이기 때문에 문자열을 변경할 때마다 새로운 String 객체가 생성되게 된다 이는 메모리 사용량 증가와 성능 저하를 가져올 수 있기에 빈번하게 수행하게 되면 문제가 될 수 있다

## StringBuilder의 역할

StringBuilder는 이러한 문제를 해결하기 위해 등장한 클래스로 StringBuilder 내부적으로 가변적인 문자 배열을 사용하여 문자열을 표현하기에 따라서 문자열을 변경할 때 새로운 객체를 생성하지 않고 기존 데이터를 직접 수정할 수 있다 그렇기에 빈번하게 문자열을 추가하고 수정하는 이러한 작업에서 StringBuilder를 이용하면 메모리 효율성과 성능을 크게 향상시킬 수 있다

## 비유

일반 String과 StringBuilder를 이해하기 쉽게 실생활에서 예를 들어 설명해보면 그림을 그린다고 생각해보자 그림을 완성하기 위해 크레파스를 사용하는데 한 크래파스를 다 써서 새로 추가할 때마다 기존의 클레파스 통을 버리고 새 크래파스를 쓰는 것과 기존의 크래파스 통에서 다 쓴 크레파스만 새로 추가하는 것 뭐가 더 효율적일까?

100% 들어맞는 설명은 아니지만 딱 봐도 후자가 앞도적으로 효율적일 것이다 여기서 전자가 일반 String, 후자가 StringBuilder라고 이해하면 쉽다

## 주요 메서드

이와 같은 StringBuilder는 문자열을 조작하는 다양한 메서드를 제공하는데 주요 메서드로는 append(), insert(), delete(), reverse() 등이 있다 이 메서드들을 사용하면 문자열을 쉽고 효율적으로 변경할 수 있는데 아래 예제와 함께 실제로 어떻게 사용하는지 알아보자

~~~java
public class Main {
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder();
        sb.append("Hello ");
        sb.append("World!");

        System.out.println(sb.toString()); // 출력: Hello World!

        sb.insert(6, "Java ");
        System.out.println(sb.toString()); // 출력: Hello Java World!

        sb.delete(6, 11);
        System.out.println(sb.toString()); // 출력: Hello World!

        sb.reverse();
        System.out.println(sb.toString()); // 출력: !dlroW olleH
    }
}
~~~

## 주의 사항

이렇게 완벽해보이는 StringBuilder에도 사용할 때 주의해야 할 사항들이 존재하는 우선 StringBuilder는 스레드 안전(thread-safe)하지 않다 따라서 멀티스레드 환경에서는 StringBuilder 대신 StringBuffer 클래스를 사용하는 것이 좋다 또한

StringBuilder를 사용할 때 불필요하게 큰 초기 용량을 설정하면 메모리 낭비가 발생할 수 있고 너무 작게 설정하면 내부 버퍼가 자주 확장되어 성능이 저하될 수 있다는 점을 명심해야 한다

## 결론

이상으로 StringBuilder에 대한 설명을 마치며 문자열을 효율적으로 처리해야 하는 상황에서 StringBuilder의 사용에서는 멀티스레드 환경에서는 StringBuffer를 사용해야 한다는 것을 기억하자!

마치며 이 글이 Java의 StringBuilder에 대해 이해하는데 도움이 되었기를 바라며 Happy coding!