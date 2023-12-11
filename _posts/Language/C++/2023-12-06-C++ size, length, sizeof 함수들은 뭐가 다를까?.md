---
title: C++ size, length, sizeof 함수들은 뭐가 다를까?
date: 2023-12-06 23:00:55 +/-0000
categories: [Language, CPP]
tags: [cpp]
toc: true
pin: true
---

C++을 사용하다 보면 배열이나 백터, 문자열 등등에 사이즈를 알기 위해 여러 함수들을 사용하게 되는데 이 중 size(), sizeof(), length() 함수들이 데이터들의 크기를 다루는데 자주 사용되지만

비슷해 보이는 이 함수들도 그 용도와 반환 값이 상이하다 나 또한 함수들을 헷갈려 해서 이번 글에서 이러한 함수들에 대해 알아보고 차이점을 비교해보면서 정리하려고 한다

## size() 함수

size() 함수는 STL(Standard Template Library) 컨테이너의 요소 개수를 반환하는 함수로 아래와 같이 사용하는데

~~~cpp
#include <iostream>
#include <vector>
#include <string>

int main() {
    std::vector<int> v = {1, 2, 3, 4, 5};
    std::string str = "Hello World";

    std::cout << "vector size: " << v.size() << std::endl;
    std::cout << "String size: " << str.size() << std::endl;

    return 0;
}
~~~

위 코드에선 v.size()는 벡터 v의 요소 수를 str.size()는 문자열 str의 길이를 반환하고 있다

주요 특징으로는 
* 컨테이너의 요소 수를 반환한다
* 반환 타입은 size_type이다

이 정도로 정리할 수 있겠다

## sizeof() 연산자

다음으로 sizeof() 함수이다 sizeof()는 변수, 자료형, 또는 표현식의 메모리 크기를 바이트 단위로 반환하는 함수로

~~~cpp
#include <iostream>

int main() {
    int a;
    double b;

    std::cout << "size of int: " << sizeof(a) << " bytes" << std::endl;
    std::cout << "size of double: " << sizeof(b) << " bytes" << std::endl;

    return 0;
}
~~~

위 코드에선 sizeof(a)는 int 타입 변수 a의 메모리 크기를 sizeof(b)는 double 타입 변수 b의 메모리 크기를 반환하고 있다

주요 특징으로는

* 메모리 크기를 바이트 단위로 반환한다
* 컴파일 타임에 결정되며 실행 시간에는 변경되지 않는다
* 반환 타입은 std::size_t이다

이렇게 정리할 수 있다

## length() 함수

마지막으로 length() 함수는 주로 std::string에서 사용되며 문자열의 길이(문자 개수)를 반환한다

~~~cpp
#include <iostream>
#include <string>

int main() {
    std::string str = "Hello World";

    std::cout << "String length: " << str.length() << std::endl;

    return 0;
}
~~~

이 코드에선 str.length()는 문자열 str의 길이를 반환하고 있다

주요 특징으로는

* 문자열의 길이(문자 개수)를 반환한다
* std::string에서 주로 사용된다
* 반환 타입이 size_type이다

## 결론 및 비교

결론적으로 표로 요약해보자면

| 함수       | 설명                                       | 사용 예시                              | 반환 타입            | 반환 값                              | 사용 컨텍스트                         |
|------------|--------------------------------------------|----------------------------------------|---------------------|--------------------------------------|---------------------------------------|
| `size()`   | 컨테이너 내 요소의 개수를 반환             | `std::vector<int> v; v.size();`        | `size_type`         | 컨테이너 내 요소의 개수              | STL 컨테이너 (`vector`, `string` 등)  |
| `sizeof()` | 변수나 자료형의 메모리 크기를 바이트 단위로 반환 | `sizeof(int)`                          | `std::size_t`       | 지정된 타입 또는 변수의 메모리 크기 | 모든 변수 및 데이터 타입             |
| `length()` | 문자열의 길이(문자 개수)를 반환             | `std::string str = "hello"; str.length();` | `size_type`         | 문자열의 길이                        | `std::string` 문자열                 |

이렇게 정리할 수 있겠다

쉽게 말하자면 STL 컨테이너에서는 size를 STL 컨테이너가 아닌 것에 사이즈는 sizeof를 문자열은 length를 사용하면 된다