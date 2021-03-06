---
layout: single
title:  "Ubuntu AUTO start setting"
---
# Ubuntu AUTO start setting 정리

본 포스팅은 Ubuntu에서 부팅시에 자동으로 프로그램을 실행 시키기 위한 setting 방법을 정리한 것. 

방법은 총 5가지가 있는데 본인에게 맞는 방법을 선택하면 된다.
<br/><br/><br/>

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

<br/><br/><br/>
## 2. rc.local 사용법

rc.local은 부팅 후에 맨 처음 실행되는 파일이다. 

```
cd /etc

sudo gedit rc.local
```

rc.local 파일에 원하는 스크립트를 실행시키거나 원하는 프로그램을 실행시킨다. 

ex ) 

```
#! /bin/bash

sourcr ~/.bashrc

sleep 3

roslaunch your launchfile.launch
```

rc.local 권한설정
```
sudo chmod +x rc.local
```

그리고 다음 디렉토리로 가서 service를 실행한다. 

```
cd /lib/systemd/system/

sudo gedit rc-local.service
```

다음 내용을 입력한다.
```
[Unit]
Description=/etc/rc.local Compatibility
Documentation=man:systemd-rc-local-generator(8)
ConditionFileIsExecutable=/etc/rc.local
After=network.target

[Service]
Type=forking
ExecStart=/etc/rc.local start
TimeoutSec=0
RemainAfterExit=yes
GuessMainPID=no

[Install]
WantedBy=multi-user.target
```
이후 해당 service를 활성화 해주고 실행을 해서 잘 작동하는지 확인한다.
```
sudo systemctl enable rc-local.service

sudo systemctl start rc-local.service
```

잘되는걸 확인하면 reboot 시켜본다.

```
sudo reboot
```
<br/><br/><br/>

## 3. bashrc 사용법 

## 4. init.d 사용법

## 5. systemd 사용법





