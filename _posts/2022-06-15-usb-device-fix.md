---
layout: single
title:  "USB device fix"
---

# USB device fix in Ubuntu

본 포스팅은 우분투에서 USB 장치를 항상 고정시키는 방법을 정리한 것.

USB device를 사용하다보면 다시 꼽을때 마다 장치번호가 바뀌어서 설정을 다시 해줘야 하는 경우가 생긴다. 


이때 이 방법을 사용하면 설정할 필요가 없다. 

## 1. device information check

장치를 연결하고 USB에 부여된 정보를 확인한다. 

```
ls -al /dev/serial/by-id
```

(인식된 사진 첨부 예정)

그다음 기기의 Vender ID, Product ID를 확인한다.
```
lsusb
```

(이미지 첨부 예정)

기기의 Serial Number를 확인한다. 아래의 ttyUSB는 본인의 device에 맞게 수정한다.

```
udevadm info -a /dev/ttyUSB | grep '{serial}'
```

(이미지 첨부 예정)

## 2. rule file 생성

우리가 알아낸 device의 정보를 통해 고정 시킬 rule을 만들어준다. 이때 파일 name은 본인 원하는대로!

```
cd /etc/udev/rules.d
sudo gedit 99-stereo.rules
```

rule 파일 안에 내용은 다음과 같이 입력한다. 

```
SUBSYSTEM=="tty", ATTRS{idVendor}=="your_number", ATTRS{idProduct}=="your_number", ATTRS{serial}=="your_number", SYMLINK+="ttyIMU"
```

만약 여러개의 장치를 고정하려면 다음줄에 똑같은 양식으로 입력하면 된다. 



