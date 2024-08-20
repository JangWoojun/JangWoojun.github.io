---
title: VSCode macOS 업데이트 오류
date: 2024-08-20 11:30:00 +/-0000
categories: [Problem, Web]
tags: [web, problem]
toc: true
pin: true
---

# 문제 상황

VSCode를 사용하던 중 버전 업데이트가 필요하여 설정에 업데이트 확인을 클릭했지만
업데이트가 계속 실패하여 VSCode를 업데이트 할 수 없는 현상이 발생했다

# 해결법

해결방법으로는 터미널에

~~~kotlin
sudo chown -R $USER ~/Library/Caches/com.microsoft.VSCode.ShipIt
xattr -dr com.apple.quarantine /Applications/Visual\ Studio\ Code.app
~~~

해당 명령어를 입력하면 되는데 만약

~~~
Operation not permitted: '/Applications/Visual Studio Code.app/Contents/CodeResources'
~~~

이러한 메세지가 발생한다면 당황하지 말고 설정에 개인정보 보호 및 보안에 들어가서
전체 디스크 권한을 터미널에 허용하면 된다