---
title: 안드로이드 EditText input 타입
date: 2024-09-19 06:10:00 +/-0000
categories: [Mobile, Android]
tags: [android]
toc: true
pin: true
---

안드로이드 앱 개발을 하다 보면 EditText에서 단순한 텍스트가 아닌 전화번호, 이메일, 비밀번호 등 자주 쓰는 특정 input을 받아야 할 상황이 자주 있다 그렇기에 안드로이드에서 이렇게 자주 쓰는 input 타입이 미리 정의되어 있는데 이번 글에선 input type들에 종류를 정리하겠다

# input 타입 리스트

## 1. 일반 텍스트 입력 (Text)

- **`text`**: 일반적인 텍스트 입력을 허용한다
- **`textCapCharacters`**: 모든 문자가 대문자로 입력된다
- **`textCapWords`**: 각 단어의 첫 글자가 대문자로 입력된다
- **`textCapSentences`**: 각 문장의 첫 글자가 대문자로 입력된다
- **`textAutoCorrect`**: 자동 교정을 허용한다
- **`textAutoComplete`**: 자동 완성을 허용한다
- **`textMultiLine`**: 여러 줄에 걸쳐 텍스트를 입력할 수 있다
- **`textImeMultiLine`**: 여러 줄의 텍스트 입력을 위한 IME(입력기)를 허용한다
- **`textNoSuggestions`**: 텍스트 입력 중 제안을 표시하지 않는다

## 2. 비밀번호 및 민감한 정보 (Password & Sensitive Information)

- **`textPassword`**: 비밀번호 입력을 위한 비공개 텍스트
- **`textVisiblePassword`**: 비밀번호 입력이지만 텍스트가 보인다
- **`textWebPassword`**: 웹용 비밀번호 입력을 위한 비공개 텍스트
- **`numberPassword`**: 비밀번호 입력을 위한 숫자만 입력 가능하다

## 3. 숫자 입력 (Number)

- **`number`**: 일반적인 숫자 입력을 허용한다
- **`numberSigned`**: 양수 및 음수 숫자 입력을 허용한다
- **`numberDecimal`**: 소수점 숫자 입력을 허용한다

## 4. 전화번호 및 특정 텍스트 입력 (Phone & Specific Text)

- **`phone`**: 전화번호 입력을 허용한다
- **`datetime`**: 날짜 및 시간 입력을 허용한다
- **`date`**: 날짜 입력을 허용한다
- **`time`**: 시간 입력을 허용한다

## 5. 이메일 및 URL 입력 (Email & URL)

- **`textEmailAddress`**: 이메일 주소 입력을 허용한다
- **`textEmailSubject`**: 이메일 제목 입력을 허용한다
- **`textWebEmailAddress`**: 웹에서 이메일 주소 입력을 허용한다
- **`textUri`**: URL 입력을 허용한다
- **`textWebEditText`**: 웹에서 일반적인 텍스트 입력을 허용한다

## 6. 기타 입력 방식

- **`textFilter`**: 필터링을 위한 텍스트 입력을 허용한다
- **`textPhonetic`**: 발음을 위한 텍스트 입력을 허용한다