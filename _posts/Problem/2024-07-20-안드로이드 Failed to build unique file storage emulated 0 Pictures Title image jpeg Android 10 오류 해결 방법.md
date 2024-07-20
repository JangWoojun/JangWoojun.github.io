---
title: 안드로이드 Failed to build unique file /storage/emulated/0/Pictures Title image/jpeg Android 10 오류 해결 방법
date: 2024-07-20 12:00:00 +/-0000
categories: [Problem, Android]
tags: [android, problem]
toc: true
pin: true
---

# 문제 상황

안드로이드에서 특정 실기기에서 카메라를 사용하던 중 오류가 발생하여 앱이 강제 종료되는 문제가 발생했다

~~~
java.lang.IllegalStateException: Failed to build unique file: /storage/emulated/0/Pictures image image/jpeg
~~~

에러 메세지는 위와 같았으며 문제가 생긴 부분은

~~~kotlin
private fun getImageUri(image: Bitmap): Uri {
    val bytes = ByteArrayOutputStream()
    image.compress(Bitmap.CompressFormat.JPEG, 100, bytes)
    val path = MediaStore.Images.Media.insertImage(this.contentResolver, image, "IMG", null)
    return Uri.parse(path)
}
~~~

위 함수였다 하지만 분명 똑같은 앱인데 어디서는 문제가 생기고 어디서는 안 생긴다는 것이 이해가 안돼서 원인을 찾아보니 해당 오류는 모든 버전이 아닌 안드로이드 10에서만 발생하며 그중에서도 일부 장치 모델에서만 발생한다는 것을 알게 되었다

# 해결법

해결방법으로는 title 부분을 중복되지 않게 바꿔주면 되는데 코드와 함께 보면

~~~kotlin
private fun getImageUri(image: Bitmap): Uri {
    val bytes = ByteArrayOutputStream()
    image.compress(Bitmap.CompressFormat.JPEG, 100, bytes)
    val path = MediaStore.Images.Media.insertImage(this.contentResolver, image, "IMG", null) // 이 부분을 중복되지 않게
    return Uri.parse(path)
}
~~~ 

이런 코드를 

~~~kotlin
private fun getImageUri(image: Bitmap): Uri {
    val bytes = ByteArrayOutputStream()
    image.compress(Bitmap.CompressFormat.JPEG, 100, bytes)
    val path = MediaStore.Images.Media.insertImage(this.contentResolver, image, "IMG_" + System.currentTimeMillis(), null)
    return Uri.parse(path)
}
~~~ 

이렇게 System.currentTimeMillis 함수등을 사용해서 중복을 방지하게 되면 문제가 해결 된다