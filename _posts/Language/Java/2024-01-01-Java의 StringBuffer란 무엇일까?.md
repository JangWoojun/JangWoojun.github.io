---
title: Java의 StringBuffer란 무엇일까?
date: 2024-01-01 09:50:00 +/-0000
categories: [Language, JAVA]
tags: [java]
toc: true
pin: true
---

Java나 Kotlin 등을 사용하는 안드로이드 앱 개발에서 성능과 효율성을 고려해야 할 때는 StringBuilder나 StringBuffer 클래스를 사용해야 하는데 이번 글에서는 이러한 클래스 중 아직 다루지 않은 StringBuffer에 대해 자세히 알아보겠다

# StringBuffer란?

StringBuffer는 Java에서 변경 가능한 문자열을 표현하는 클래스로 java.lang 패키지에 속해 있다 StringBuilder와 비슷하지만 아주 중요하고 핵심적인 차이점이 있다 StringBuffer는 StringBuilder와 마찬가지로 문자열을 추가, 수정, 삭제하는 작업을 빈번하게 수행할 때 사용되지만 StringBuilder와 다르게 멀티스레드 환경에서 안전하게 사용할 수 있다

## 문자열 처리의 문제점과 StringBuffer의 해결

일반적으로 자바에서 문자열을 다룰 때는 String 클래스를 사용하지만 String 객체는 불변(immutable)이기 때문에 문자열을 변경할 때마다 새로운 String 객체가 생성된다 이는 메모리 사용량과 성능 저하의 문제를 야기할 수 있기에 주의를 해야한다 반면 StringBuffer는 내부적으로 가변적인 문자 배열을 사용하여 문자열 변경 시 새로운 객체 생성 없이 기존 데이터를 직접 수정하기에 메모리 효율성과 성능 향상 측면에서 기존 String 보다 좋다

## StringBuffer와 StringBuilder의 차이점

앞에서 이미 설명하고 넘어갔지만 중요한 부분이니 다시 한번 말하자면 StringBuffer와 StringBuilder는 둘다 유사해 보이지만 가장 둘은 스레드 안전성(thread-safety)측면에서 다르다고 보면 쉽다

StringBuffer는 스레드 안전한 반면 StringBuilder는 그렇지 않기에 멀티스레드 환경에서 문자열 처리가 필요할 때는 StringBuffer를 사용해야 한다

## 주요 메서드

StringBuffer 또한 StringBuilder와 마찬가지로 문자열 조작에 유용한 다양한 메서드를 제공하는데 주요 메서드로는 append(), insert(), delete(), reverse() 등이 있다 

~~~java
public class Main {
    public static void main(String[] args) {
        StringBuffer sb = new StringBuffer();
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

StringBuffer 또한 StringBuilder와 마찬가지로 너무 큰 초기 용량은 메모리 낭비를 반면 너무 작은 용량은 내부 버퍼의 빈번한 확장으로 성능 저하를 초래할 수 있기에 사용 시 불필요하게 큰 초기 용량을 설정하지 않도록 주의해야 한다

## 결론

짧게 요약하자면 StringBuffer는 StringBuilder와 비슷하지만 멀티스레드 환경에서 문자열을 효율적으로 처리할 수 있는 강력한 도구란 걸 기억하자 라고 할 수 있겠다

마치며 이 글이 Java의 StringBuilder에 대해 이해하는데 도움이 되었기를 바라며 Happy coding!