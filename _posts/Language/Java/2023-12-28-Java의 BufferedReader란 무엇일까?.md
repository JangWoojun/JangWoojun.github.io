---
title: Java의 BufferedReader란 무엇일까?
date: 2023-12-28 19:40:00 +/-0000
categories: [Language, JAVA]
tags: [java]
toc: true
pin: true
---

안드로이드 개발 중 큰 용량을 가진 파일 읽기를 구현하다보면 필연적으로 문제가 발생하고 이를 해결하다가 BufferedReader에 대해 알게 될 것이다 이렇듯 큰 용량을 가진 파일 읽기에서 BufferedReader는 중요한 역할을 하는데 이번 글에선 이러한 BufferedReader에 대해 알아보겠다

# BufferedReader란?

BufferedReader란? 자바(Java)에서 문자 입력 스트림을 버퍼링하는데 사용되는 클래스로 java.io 패키지에 포함되어 있다

이러한 BufferedReader의 기능으로는 데이터를 직접 읽는 대신 버퍼를 사용하여 효율적으로 데이터를 읽을 수 있게 해주며 데이터를 라인 단위로 쉽게 읽을 수 있어 대량의 데이터를 처리할 때 성능이 향상된다

## 비유

일반 Reader와 BufferedReader를 이해하기 쉽게 실생활에서 예를 들어 설명해보면 카페에서 커피를 주문한다고 했을 때 커피를 한 모금씩 주문할 때마다 바리스타가 만들어서 주는 상황과 한 잔의 커피를 주문해 한 번에 모든 커피를 받는 상황 중 어떤 게 더 효율적일까?

딱 봐도 후자가 앞도적으로 효율적일 것이다 여기서 전자가 일반 Reader, 후자가 BufferedReader와 같은 방식으로 작동한다고 이해하면 쉽다

## 주요 특징

BufferedReader는 내부적으로 문자 데이터를 저장하기 위한 버퍼를 가지고 있는데 이를 통해 데이터를 한 번에 큰 덩어리로 읽어들여 입출력(I/O) 횟수를 줄임으로써 성능을 향상시키고 있다

이렇게 앞에서 여러 번 말했듯 파일이나 네트워크 소스로부터 직접 읽는 것보다 버퍼를 통해 읽는 것이 훨씬 효율적인데 특히 큰 파일을 다룰 때는 이 성능 차이가 크게 체감되기에 큰 파일에서는 일반 Reader가 아닌 BufferedReader를 사용해야 한다

## 예제 코드

~~~java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class Main {
    public static void main(String[] args) {
        BufferedReader reader = new BufferedReader(new FileReader("example.txt"));
        String line;
        while ((line = reader.readLine()) != null) {
            // 각 줄을 처리하는 코드
        }
        reader.close();
    }
}
~~~

## 주의 사항

하지만 이렇게 좋기만 할 거 같은 BufferedReader를를 사용할 때도 꼭 지켜야 할 주의 사항이 있는데 사용이 끝났다면 항상 리소스를 닫아주어야 한다 참고로 try-with-resources 구문을 사용하면 자동으로 리소스가 닫히므로 특별한 경우가 아니라면 이를 사용하도록 하자

추가적으로 버퍼의 크기를 조절하여 성능을 더 최적화할 수 있는데 BufferedReader는 기본적으로 적절한 크기의 버퍼를 제공하지만 필요에 따라서는 생성자에서 버퍼 크기를 지정할 수도 있다