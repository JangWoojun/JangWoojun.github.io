---
title: Python EOFError 오류와 알고리즘 풀이 시 개수가 정해지지 않은 입력 처리
date: 2023-11-21 21:40:00 +/-0000
categories: [Language, Python]
tags: [python, 알고리즘]
toc: true
pin: true
---

## Python EOFError 오류란?

Python에서 발생하는 EOFError 오류란 "End Of File Error"의 약자로 파일의 끝에 도달했을 때 더 이상 읽을 내용이 없을 때 발생하는 에러이다

## 알고리즘 풀이 시 개수가 정해지지 않은 입력 처리

그렇다면 알고리즘 풀이 시 개수가 정해지지 않은 입력을 받아야 할 때는 어떻게 처리해야 할까?

그렇 때는 try except를 이용할 수 있는데

~~~python
while True:
    try:
        a = int(input())
    except:
            break
~~~

이런 식으로 EOFError가 발생하면 break로 종료시키는 방식으로 처리하면 된다