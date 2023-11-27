---
title: Gradle 빌드 파일 방식 Groovy와 KTS의 차이
date: 2023-11-27 22:40:00 +/-0000
categories: [Mobile, Android]
tags: [android]
toc: true
pin: true
---

안드로이드 앱 개발을 하다가 안드로이드 스튜디오를 보다 보면 Gradle의 빌드 파일은 주로 Groovy DSL (Domain-Specific Language) 과 Kotlin DSL (KTS)을 사용하여 작성되는데 이번 글에선 Gradle 빌드 파일 방식들인 Groovy와 KTS의 대해서 알아보려고 한다

## Groovy 

Groovy는 Java 플랫폼을 위한 객체 지향 프로그래밍 언어로 Java와 호환되면서도 추가적인 편의성과 간결함을 제공하는 것이 특징을 가지고 있다 Groovy는 동적 언어이기 때문에 런타임에 타입을 결정하고 문법이 더 유연하다는 특징을 가지고 있는데 이로 인해 개발자는 빠르고 간결한 스크립트 작성이 가능하다

이러한 Groovy는 Gradle 초기 버전부터 사용되어 왔으며 Gradle 스크립트 작성을 위한 기본 언어로 널리 사용되어 왔다

## Kotlin DSL (KTS)

Kotlin DSL은 Kotlin을 기반으로 한 Gradle 스크립트 언어로 우선 Kotlin은 JetBrains에서 개발한 현대적이고 정적 타입의 프로그래밍 언어이며 Java와 완벽하게 호환된다는 특징을 가지고 있다

이러한 Kotlin을 기반으로 하는 Kotlin DSL은 타입 안정성과 IDE에서의 우수한 지원을 제공하며 더 명시적이고 구조화된 방식으로 Gradle 스크립트를 작성할 수 있게 해준다 Kotlin DSL은 최신 Gradle 버전에서 사용될 수 있으며 Kotlin의 인기와 함께 점차 많이 사용되고 있다

또한 구글에서도 Kotlin이 더 읽기 쉬우며 더 나은 컴파일 시간 확인과 IDE 지원을 제공하기 때문에 KTS를 Gradle 스크립트를 작성할 때 Groovy보다 선호한다고 말하고 있다

## Groovy VS KTS

이제는 앞에서 살펴본 Groovy와 KTS에 대해 비교해볼 것이다

우선 각각 장단점에 대해 살펴보면

### Groovy의 장단점

**장점**

1. Groovy는 동적 타입 언어로서 높은 유연성을 제공하기에 빌드 스크립트를 더 간결하고 동적으로 작성할 수 있다

2. Java에 익숙한 개발자에게 Groovy는 비교적 쉽게 접근할 수 있어 학습 곡선이 낮고 기존 Java 코드를 쉽게 통합할 수 있다

3. 오랜 기간 동안 Gradle의 기본 언어였기 때문에 관련 자료와 커뮤니티 지원이 많다

**단점**

1. 동적 타입 언어의 특성상 컴파일 타임에 오류를 발견하기 어렵기에 복잡한 빌드 스크립트에서 문제를 일으킬 수 있다

2. Groovy의 동적 특성 때문에 IDE에서의 코드 완성 및 오류 탐지 기능이 Kotlin에 비해 제한적일 수 있다

### Kotlin DSL (KTS)의 장단점

**장점**

1. Kotlin은 정적 타입 언어이기에 컴파일 시점에 오류를 잡아내어 빌드 시간과 안정성을 개선됐다

2. Kotlin의 정적 타입 특성 덕분에 IDE에서 더 나은 코드 완성과 리팩토링, 오류 탐지 기능을 제공한다

3. Kotlin은 현대적인 언어 기능을 제공하기에 Kotlin 자체의 인기가 높아지면서 관련 자료가 점차 늘어나고 있다

**단점**

1. Kotlin에 익숙하지 않은 사용자에게는 Groovy에 비해 배우기 어려울 수 있다

2. Kotlin DSL은 Groovy에 비해 초기 설정과 실행이 느릴 수 있다

### Groovy와 KTS의 주요 차이점

1. 언어 특성: Groovy는 동적 타입, Kotlin은 정적 타입 언어

2. 성능과 안정성: Kotlin은 Groovy의 비해 더 높은 성능과 안정성을 제공한다

3. 코드 스타일과 구조: Kotlin은 Groovy의 비해 언어 상에서 더 구조화되고 모듈화된 코드 스타일을 장려하고 있다

## Groovy와 KTS 문법 비교

마지막으로 제일 중요하다고 할 수 있는 Groovy와 KTS의 서로 다른 문법들을 비교하자면

### 스크립트 파일 이름 지정

* Groovy로 작성된 Gradle 빌드 파일은 .gradle 파일 이름 확장자를 사용한다

* Kotlin으로 작성된 Gradle 빌드 파일은 .gradle.kts 파일 이름 확장자를 사용한다

### 메서드 호출에 괄호 추가

Groovy를 사용하면 메서드 호출에서 괄호를 생략할 수 있지만 Kotlin에서는 괄호가 필요하다

**Groovy**
~~~groovy
compileSdkVersion 30
~~~

**Kotlin**
~~~kotlin
compileSdkVersion(30)
~~~

### 할당 호출에 = 추가

Groovy DSL을 사용하면 속성을 할당할 때 할당 연산자 =을 생략할 수 있지만 Kotlin에서는 할당 연산자가 필요하다

**Groovy**
~~~groovy
java {
    sourceCompatibility JavaVersion.VERSION_17
    targetCompatibility JavaVersion.VERSION_17
}
~~~

**Kotlin**
~~~kotlin
java {
    sourceCompatibility = JavaVersion.VERSION_17
    targetCompatibility = JavaVersion.VERSION_17
}
~~~

### 문자열 변환

* 문자열의 큰따옴표: Groovy에서는 작은따옴표를 사용하여 문자열을 정의할 수 있지만 Kotlin에서는 큰따옴표가 필요하다

* 점으로 구분된 표현식의 문자열 보간 유형: Groovy에서는 점으로 구분된 표현식의 문자열 보간 유형에 $ 접두사만 사용할 수 있지만 Kotlin에서는 점으로 구분된 표현식을 중괄호로 묶어야 한다

**Groovy**
~~~groovy
myRootDirectory = "$project.rootDir/tools/proguard-rules-debug.pro"
~~~

**Kotlin**
~~~kotlin
myRootDirectory = "${project.rootDir}/tools/proguard-rules-debug.pro"
~~~

### def를 val 또는 var로 바꾸기

**Groovy**
~~~groovy
def building64Bit = false
~~~

**Kotlin**
~~~kotlin
val building64Bit = false
~~~

### 불리언 속성 앞에 is 추가

Groovy는 속성 이름을 기반으로 속성 추론 로직을 사용하기에 불리언 속성 foo의 경우 추론된 메서드는 getFoo 또는 setFoo, isFoo일 수 있다 따라서 Kotlin으로 변환되면 속성 이름을 Kotlin에서 지원하지 않는 추론 메서드로 변경해야 한다

**Groovy**
~~~groovy
android {
    buildTypes {
        release {
            minifyEnabled true
            shrinkResources true
            ...
        }
        debug {
            debuggable true
            ...
        }
    ...
~~~

**Kotlin**
~~~kotlin
android {
    buildTypes {
        getByName("release") {
            isMinifyEnabled = true
            isShrinkResources = true
            ...
        }
        getByName("debug") {
            isDebuggable = true
            ...
        }
    ...
~~~

## 목록 및 지도 변환

Groovy와 Kotlin의 목록과 지도는 다른 문법을 사용하여 정의되는데 Groovy는 []를 사용하는 반면 Kotlin은 listOf 또는 mapOf를 사용하여 컬렉션 생성 메서드를 명시적으로 호출한다

**Groovy 목록**
~~~groovy
jvmOptions += ["-Xms4000m", "-Xmx4000m", "-XX:+HeapDumpOnOutOfMemoryError</code>"]
~~~

**Kotlin 목록**
~~~kotlin
jvmOptions += listOf("-Xms4000m", "-Xmx4000m", "-XX:+HeapDumpOnOutOfMemoryError")
~~~

**Groovy 지도**
~~~groovy
def myMap = [key1: 'value1', key2: 'value2']
~~~

**Kotlin 지도**
~~~kotlin
val myMap = mapOf("key1" to "value1", "key2" to "value2")
~~~

### 빌드 유형 구성

Kotlin DSL에서는 디버그 빌드 유형과 출시 빌드 유형만 암시적으로 사용할 수 있기에 다른 모든 맞춤 빌드 유형은 수동으로 만들어야 한다

하지만 Groovy에서는 먼저 만들지 않고도 디버그 빌드 유형과 출시 빌드 유형, 기타 특정 빌드 유형을 사용할 수 있다

**Groovy**
~~~groovy
buildTypes {
 debug {
   ...
 }
 release {
   ...
 }
 benchmark {
   ...
 }
}
~~~

**Kotlin**
~~~kotlin
buildTypes {
 debug {
   ...
 }

 release {
   ...
 }
 register("benchmark") {
    ...
 }
}
~~~

### 플러그인 블록 변환

플러그를 적용하는 것은 Groovy와 KTS에서 비슷한데 KTS와 Groovy 모두에서 buildscript를 apply와 함께 사용하여 플러그인을 적용하는 대신 plugins {} 블록을 사용하는 것이 좋다

빌드 파일에서 만약 plugins {} 블록을 사용하면 Android 스튜디오는 빌드가 실패할 때도 컨텍스트를 인식한다

**Gradle 버전 카탈로그 Groovy**
~~~groovy
// Top-level build.gradle file
plugins {
   alias libs.plugins.android.application apply false
   ...
}

// Module-level build.gradle file
plugins {
   alias libs.plugins.android.application
   ...
}
~~~

**Gradle 버전 카탈로그 Kotlin**
~~~kotlin
// Top-level build.gradle.kts file
plugins {
   alias(libs.plugins.android.application) apply false
   ...
}

// Module-level build.gradle.kts file
plugins {
   alias(libs.plugins.android.application)
   ...
}
~~~

**Gradle 버전 카탈로그가 아닌 Groovy**
~~~groovy
// Top-level build.gradle file
plugins {
   id 'com.android.application' version '7.3.0' apply false
   ...
}

// Module-level build.gradle file
plugins {
   id 'com.android.application'
   ...
}
~~~

**Gradle 버전 카탈로그가 아닌 Kotlin**
~~~kotlin
// Top-level build.gradle.kts file
plugins {
   id("com.android.application") version '7.3.0' apply false
   ...
}

// Module-level build.gradle.kts file
plugins {
   id("com.android.application")
   ...
}
~~~

