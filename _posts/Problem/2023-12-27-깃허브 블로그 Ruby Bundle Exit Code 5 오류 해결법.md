---
title: 깃허브 블로그 Ruby Bundle Exit Code 5 오류 해결법
date: 2023-12-27 11:05:55 +/-0000
categories: [Problem, Blog]
tags: [blog, problem]
toc: true
pin: true
---

# 문제 상황

잘 쓰던 깃허브 블로그가 어느 순간 

<img width="731" alt="스크린샷 2023-12-27 오후 1 25 39" src="https://github.com/JangWoojun/JangWoojun/assets/102157871/d3ecb83d-6bf8-4f0c-949c-687997581f82">

이러한 페이지만 뜨며 접속이 안되는 문제가 생겼다
그래서 어떤 문제가 있나 찾아보다가

<img width="1414" alt="스크린샷 2023-12-27 오전 11 02 48" src="https://github.com/JangWoojun/JangWoojun/assets/102157871/726fe221-8451-49be-8f72-c4aa6fc31b3f">

이렇게 

Error: The process '/opt/hostedtoolcache/Ruby/3.3.0/x64/bin/bundle' failed with exit code 5

라는 오류 메시지가 발생한다는 걸 알게 되었다

# 해결 방법

해당 문제를 해결하기 위해 내가 사용한 방법으로는

<img width="955" alt="스크린샷 2023-12-27 오전 10 55 48" src="https://github.com/JangWoojun/JangWoojun/assets/102157871/ac82b764-7e68-491a-a834-a4f9b3b36b1b">

.github/workflows 폴더에 있는 pages-deploy.yml에서 ruby-version이 기본 3으로 설정되어 있길래

<img width="945" alt="스크린샷 2023-12-27 오전 10 56 12" src="https://github.com/JangWoojun/JangWoojun/assets/102157871/10c026e1-600b-421f-9ee8-160ac6a92533">

3.2로 수정한 뒤 커밋 후 푸시를 하였다

그리고 확인해보면

<img width="1430" alt="스크린샷 2023-12-27 오전 11 02 05" src="https://github.com/JangWoojun/JangWoojun/assets/102157871/5cf545a5-341b-4dd0-bcc7-826cf91693f8">

이렇게 문제가 해결된 걸 볼 수 있다