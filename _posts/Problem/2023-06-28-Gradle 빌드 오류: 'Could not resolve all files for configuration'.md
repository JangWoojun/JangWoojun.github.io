---
title: Gradle 빌드 오류 - 'Could not resolve all files for configuration' 해결 방법
date: 2023-06-28 20:05:55 +/-0000
categories: [Problem, Android]
tags: [android, problem]
toc: true
pin: true
---

# 문제 상황

<img width="1808" alt="스크린샷 2023-06-27 오후 11 20 30" src="https://github.com/JangWoojun/JangWoojun.github.io/assets/102157871/0a262f9e-1d75-4975-84bb-1e05fea3e607">

안드로이드에서 라이브러리를 추가하려고 하던 중 앱을 빌드하니 위와 같이

~~~
Caused by: org.gradle.api.internal.artifacts.ivyservice.DefaultLenientConfiguration$ArtifactResolveException:Could not resolve all files for configuration : app: debuqCompileClasspath
~~~

이러한 오류 메세지가 발생하였다

# 해결법

<img width="797" alt="스크린샷 2023-06-28 오후 10 19 32" src="https://github.com/JangWoojun/JangWoojun.github.io/assets/102157871/0c53758b-a1b9-4785-be2d-32dd5f0fa534">

자세히 문제가 되는 부분을 확인해보니 초록색 부분으로 표시 된 것과 같이 잘못된 코드로 라이브러리를 추가하려고 하여서 발생한 문제였다

