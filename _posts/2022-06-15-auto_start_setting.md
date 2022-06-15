---
layout: single
title:  "Ubuntu AUTO start setting"
---
# Ubuntu AUTO start setting 정리

본 포스팅은 Ubuntu에서 부팅시에 자동으로 프로그램을 실행 시키기 위한 setting 방법을 정리한 것. 

방법은 총 5가지가 있는데 본인에게 맞는 방법을 선택하면 된다.

## 1. Crontap 

Crontap은 Cron이라는 데몬이 어떤 프로그램을 자동으로 실행시킬지 적어놓는 리스트라고 보면된다.

### Crontap 설정방법
Crontap 사용법은 매우 간단하다. 

하지만 단점이 권한설정에 조금 복잡한데 이는 아래에서 다루겠다.



```
crontab -e
```

위 명령어를 입력하면 editor를 설정하라고 뜨는데 본인이 원하는걸로 선택하면된다.   
(본인은 vim으로 기본설정 되어있었다...선택권한이없었음)

선택하고 나면 화면이 하나 뜨는데 설명이 적혀있는거니 읽어보면 좋다.

아무튼 터미널상에서 마지막줄에 

```
@reboot /your/sh/file/dir
```
을 입력하고 저장하면 된다. 

## 2. rc.local 사용법

## 3. bashrc 사용법 

## 4. init.d 사용법

## 5. systemd 사용법





