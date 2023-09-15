---
title: 맥북 Ventura 안드로이드 스튜디오, 인텔리제이 화면 깜빡거림 오류
date: 2023-09-15 22:00:00 +/-0000
categories: [Problem, Android]
tags: [android, problem, android studio, intellij]
toc: true
pin: true
---

# 문제 상황

현재 내 맥북에서는 Ventura OS 버전 업그레이드 이후 언제부턴가 안드로이드 스튜디오, 인텔리제이 등등 프로그램에서 간헐적으로 화면이 깜빡거리는 오류가 발생하고 있다

물론 깜빡거림 정도는 신경 안쓰고 그냥 코딩하는 상남자들도 있겠지만 본인은 조금의 불편함이라도 참을 수 없는 **최강 MZ**이기에 해결법을 정리해서 올리려고 한다

여기 [젯브레인 문제 게시글](https://youtrack.jetbrains.com/issue/JBR-4959/Screen-flickering-when-IDE-is-full-screen-with-metal-rendering-enabled)를 보면 나만 해당 문제를 겪는게 아닌 거 같기도 하고

# 해결법

해당 문제는 사람마다 해결 방법이 모두 다르기에 한 가지 방법을 시도했는데 안됐다고 포기하지말고 그 방법들을 모두 시도해보길 바란다

## 해결 방법1 

![0915-1](https://github.com/JangWoojun/JangWoojun/assets/102157871/f12638f2-cb6a-4b87-b731-27dca9de6573)

해당 해결 방법은 본인이 사용하고 실제로 효과를 얻은 방법으로 우선 시스템 설정으로 들어가서

![스크린샷 2023-09-15 오후 10 29 20](https://github.com/JangWoojun/JangWoojun/assets/102157871/eec82408-ec74-4ba1-ac29-074344881ffa)

데스크탑 및 Dock에서 자동으로 메뉴 막대 가리기 및 보기 옵션을 안함으로 설정하면 된다

## 해결 방법2

![스크린샷 2023-09-15 오후 10 42 24](https://github.com/JangWoojun/JangWoojun/assets/102157871/0b5859d2-3070-4549-ad8a-bb5c0748dc4a)

해당 방법은 우선 인텔리제이나 안드로이드 스튜디오에서 도움말(Help)에서 사용자 지정 VM 옵션 편집(Edit Custom VM Options)을 들어간 뒤 

![스크린샷 2023-09-15 오후 10 30 28](https://github.com/JangWoojun/JangWoojun/assets/102157871/66f7204b-e4e6-4b53-abc2-03432fcf3e56)

~~~
-Dsun.java2d.metal=false
~~~

해당 코드를 붙여넣으면 된다

## 해결 방법3

![스크린샷 2023-09-15 오후 10 33 33](https://github.com/JangWoojun/JangWoojun/assets/102157871/068eef3d-21a9-444f-b6df-183dfbc9e184)

해당 방법은 간단한 방법으로 시스템 설정에 디스플레이에서 True Tone 옵션을 끄면 된다

## 해결 방법4

![스크린샷 2023-09-15 오후 10 32 12](https://github.com/JangWoojun/JangWoojun/assets/102157871/4675f342-559b-489a-bcb8-b46229ec6e52)

마지막 방법은 조금 극단적인 방법으로 Ventura OS를 버리고 이전 버전에 Mac OS로 다운그레이드 하여 문제를 회피하는 방법이다 물론 나는 이 방법까지는 안 갔지만 위에 설명한 방법들을 모두 시도 해본 후 

[젯브레인 문제 게시글](https://youtrack.jetbrains.com/issue/JBR-4959/Screen-flickering-when-IDE-is-full-screen-with-metal-rendering-enabled) 속 답변들도 모두 시도했지만 오류가 고쳐지지 않았다면 최후의 수단으로 쓰면 될 거 같다

처음에 해당 문제를 해결하려고 구글링 했지만 해당 문제 해결 방법들을 명확히 정리한 글이 거의 없길래 해당 내용을 정리하여 블로그로 작성하였다

이상으로 오류를 해결하여 모두 행복한 코딩을 하길 바란다!