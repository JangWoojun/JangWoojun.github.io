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

위와 같이 사용하면 되고

Kotlin-DSL를 사용하는 경우라면 

~~~kotlin
android {
	...
    val localProperties = Properties()
    val localPropertiesFile = rootProject.file("local.properties")
    if (localPropertiesFile.exists()) {
        localPropertiesFile.inputStream().use { localProperties.load(it) }
    }	

    val API_KEY = localProperties.getProperty("API_KEY") ?: ""

    defaultConfig {
        ...
		
        buildConfigField("String", "MAPS_API_KEY", "\"$MAPS_API_KEY\"")
        resValue("string", "MAPS_API_KEY", MAPS_API_KEY)
    }
}
~~~

이런 식으로 하면 되는데 참고로 이제는 buildConfig를 true로 주지 않으면 오류가 나기에
꼭 true로 설정하자

~~~kotlin
buildFeatures {
	buildConfig = true
}
~~~