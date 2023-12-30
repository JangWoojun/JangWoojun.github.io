---
title: Python의 pass란 무엇일까?
date: 2023-12-30 19:00:00 +/-0000
categories: [Language, Python]
tags: [python]
toc: true
pin: true
---

만약 Python을 간단하게 사용하거나 아직 기초만 배우는 중이라면 모르겠지만 Python에서는 pass라는 키워드가 있다 pass는 Python에서 사용되는 특별한 키워드로 이번 글은 이러한 pass에 대해 알아보려고 한다

## pass란?

Python에서 pass는 **아무것도 수행하지 않음**을 의미하는 키워드로 코드 블록 내에서 어떠한 동작도 하지 않을 때 사용된다 해당 키워드가 존재하는 가장 큰 이유로는 Python이 다른 언어와 달리 빈 코드 블록을 허용하지 않기 때문인데

주로 pass는 구조적으로 필요하지만 아직 구현할 내용이 없는 경우나 임시 코드, 미구현 기능 표시를 위해서, 또 추상 클래스에서 추상 메서드를 구현할 때나 프로그램이 에러로 죽지 않게 하기 위해서도 사용된다

이처럼 pass는 많은 사례에서 사용할 수 있다

## pass 사용 예시

앞에서 pass가 무엇인지 개념을 살펴봤으니 코드와 함께 pass를 실제로 어떻게 사용하는지 알아보자

1. 빈 함수

아직 구현하지 않은 함수의 경우 함수의 본문에 pass를 사용할 수 있다

~~~python
def not_implemented_function():
    pass
~~~

이 함수는 호출되어도 아무런 동작을 하지 않는다

2. 빈 클래스

클래스를 설계하는 초기 단계에서 멤버 함수나 속성 없이 클래스의 구조만 잡고 싶을 때 pass를 사용한다

~~~python
class EmptyClass:
    pass
~~~

이 클래스는 아무런 속성이나 메서드를 가지고 있지 않는다


pass를 사용하는 두 가지 중요한 상황인 에러 핸들링과 추상 클래스 내의 추상 메서드에서의 사용에 대해 설명하겠습니다.

1. 에러 핸들링에서의 pass
Python에서 예외 처리를 할 때 try-except 블록을 사용합니다. 때로는 특정 예외를 잡아내지만, 그 예외에 대해 아무런 조치를 취하지 않고 넘어가고 싶을 때가 있습니다. 이럴 때 pass를 사용합니다.

python
Copy code
try:
    # 오류가 발생할 수 있는 코드
    risky_operation()
except SomeSpecificError:
    pass  # 오류가 발생해도 아무 조치를 취하지 않음
이 예제에서 SomeSpecificError 예외가 발생하면, 프로그램은 pass 구문을 만나고 아무런 동작도 수행하지 않은 채로 계속 진행합니다. 이는 로깅, 디버깅, 또는 특정 오류를 무시하는 경우에 유용합니다.

3. 추상 클래스의 추상 메서드에서의 pass

~~~python
from abc import ABC, abstractmethod

class MyAbstractClass(ABC):
    
    @abstractmethod
    def my_abstract_method(self):
        pass
~~~

이 코드에서 MyAbstractClass는 추상 클래스이며,my_abstract_method는 추상 메서드이다 이 클래스를 상속하는 모든 서브클래스는 my_abstract_method를 구현해야 한다

4. 조건문에서의 사용

특정 조건에 대한 코드를 아직 작성하지 않았을 때 pass를 활용할 수 있다

~~~python
if condition:
    pass
else:
    print("조건에 맞지 않습니다.")
~~~

여기서 condition이 참이면 아무 일도 일어나지 않는다

5. 에러 핸들링에서의 pass

보통 try except을 사용해서 오류를 캐치할 때 pass를 통해 무시하고 프로그램을 살릴 수 있다

~~~python
try:
    # 오류가 발생할 수 있는 코드
    risky_operation()
except SomeSpecificError:
    pass  # 오류가 발생해도 아무 조치를 취하지 않음
~~~

## 결론

이처럼 Python의 pass는 간단하지만 다양하게 사용할 수 있는 중요한 키워드로 간단하게 Python을 사용할 예정이라면 모르고 넘기기 쉬우나 제대로 Python을 사용하려면 꼭 알아야 한다

이 글이 Python의 pass에 대해 이해하는데 도움이 되었기를 바라며 Happy coding!