---
title: Android Unable to add window 오류
date: 2023-06-15 23:10:55 +/-0000
categories: [Problem, Android]
tags: [android, problem]
toc: true
pin: true
---

# 문제 상황

안드로이드에서 Dialog를 사용하던 도중 Unable to add window -- token null is not valid; is your activity running?라는 메시지가 발생하며 앱이 강제 종료되게 되었다

문제 코드 

~~~kotlin
val dialog = Dialog(baseContext)
dialog.setContentView(R.layout.webview_dialog)
dialog.window?.setBackgroundDrawableResource(R.drawable.dialog_background)
val windowWidth = resources.displayMetrics.widthPixels * 0.9
val windowHeight = resources.displayMetrics.heightPixels * 0.7
dialog.window?.setLayout(windowWidth.toInt(), windowHeight.toInt())

val ok = dialog.findViewById<CheckBox>(R.id.yes_button)
val x = dialog.findViewById<CheckBox>(R.id.no_button)
val webView = dialog.findViewById<WebView>(R.id.webview)

webView.loadUrl("https://sch10719.neocities.org/codingvocaprivacypolicy")

ok.setOnClickListener {
    dialog.dismiss()
    consentCheckBox2.isChecked = true
}

x.setOnClickListener {
    dialog.dismiss()
    consentCheckBox2.isChecked = false
}

dialog.show()
~~~

# 해결법

해당 코드에서 발생한 문제를 해결하기 위해 여러 시도를 하던 끝에 해결 방법을 찾게 되었는데
해당 오류가 발생하는 원인은 바로 val dialog = Dialog(baseContext) 부분에 context를 baseContext로 준 것이 문제로

~~~kotlin
val dialog = Dialog(this@AgreementActivity)
dialog.setContentView(R.layout.webview_dialog)
// 코드 생략
dialog.show()
~~~

위 코드에서 Dialog에 baseContext가 아닌 this@액티비티 이름으로 바꿔서 넣은 뒤 다시
앱을 실행하면 위 오류 메시지가 뜨지 않고 잘 실행되는 것을 볼 수 있다