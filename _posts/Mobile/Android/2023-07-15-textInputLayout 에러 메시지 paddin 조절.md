---
title: 안드로이드 textInputLayout 에러 메시지 padding 조절
date: 2023-07-15 7:31:00 +/-0000
categories: [Mobile, Android]
tags: [android]
toc: true
pin: true
---

# 안드로이드 textInputLayout 에러 메시지 padding 조절

안드로이드에서 textInputLayout을 통해 입력창을 구현하여 에러 메시지를 표시하다보면

<img width="330" alt="스크린샷 2023-07-15 오전 7 33 21" src="https://github.com/JangWoojun/JangWoojun/assets/102157871/efecd04d-9f86-45bd-b917-a933da892af3">

위와 같이 에러 메시지에 위치가 hint 텍스트 위치와 같게 설정 되어서 무언가 디자인 상으로
애매해지는 경우가 발생할 수 있다

그럴 땐 해당 코드를 사용해서 해결할 수 있는데

~~~kotlin
textInputLayout.apply {
    viewTreeObserver.addOnGlobalLayoutListener {
        if (childCount > 1) {
            getChildAt(1)?.setPadding(
                left,
                top,
                right,
                bottom
            )
        }
    }
}
~~~

여기서 left, top, right, bottom 값을 조절하면 원하는 대로 에러 메시지에 padding을 조절할 수 있다

예시로 나는

~~~kotlin
passwordInputLayout.apply {
    viewTreeObserver.addOnGlobalLayoutListener {
        if (childCount > 1) {
            getChildAt(1)?.setPadding(
                8,
                20,
                0,
                0
            )
        }
    }
}
~~~

위 코드를 사용하여 문제를 해결했고 결과는 아래와 같이 확인해볼 수 있다

<img width="330" alt="스크린샷 2023-07-15 오전 7 34 21" src="https://github.com/JangWoojun/JangWoojun/assets/102157871/2360944d-e9f5-4174-8312-98929c33c034">

처음에 간단히 해결할 수 있을 줄 알았던 이 문제 때문에 해결법을 찾기 위해 꽤 애를 먹었지만 [참고한 스택 오버플로우 답변](https://stackoverflow.com/questions/55744153/remove-extra-padding-margin-from-textinputlayout-seterror-text) 해당 글 덕에 겨우 해결할 수 있었다 

역시 스택오버플로우는 신이야...

참고로 에러 메시지는 

~~~kotlin
textInputLayout.error = "error text"
~~~

위와 같이 띄울 수 있다