---
title: 안드로이드 Kotlin-DSL local.properties 사용
date: 2023-11-09 22:00:00 +/-0000
categories: [Mobile, Android]
tags: [android]
toc: true
pin: true
---

# 안드로이드 Kotlin-DSL local.properties 사용

안드로이드에서 local.properties를 사용해서 API 키나 숨겨야 하는 것이 있을 때 일반적으로 Groovy 사용할 때는

~~~kotlin
Properties properties = new Properties() 
properties.load(project.rootProject.file('local.properties').newDataInputStream()) 

android {

	... 

	defaultConfig {
    
    	... 
        
        buildConfigField "String", "APIKEY", properties["apiKey"] 
        
        } 
 }
~~~

위와 같이 사용하면 되지만

Kotlin-DSL를 사용하는 경우라면 위와 같은 방법으론 해결할 수 없고

~~~kotlin
import com.android.build.gradle.internal.cxx.configure.gradleLocalProperties

android {

	...
    
    defaultConfig {
    
    	...
        
 		buildConfigField("String", "APIKEY", gradleLocalProperties(rootDir).getProperty("apiKey"))

    }
    
}
~~~

이런 식으로 처리해야 한다

