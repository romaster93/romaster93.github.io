---
layout: single
title:  "Nvidia Xavier 초기 세팅"
---

# Xavier setting List

본 포스팅은 xavier를 드론에 탑재하기전에 해야할 기본적인 내용을 정리한 것. 

## 1. SDK manager for xavier format

```
$ sdkmanager
```
여기서 SDKmanager에서 시키는대로 하면된다.    
tip. recovery mode -> 가운데 버튼을 누른상태에서 전원버튼을 눌러주면된다.   

## 2. ROS install in xavier 
```
cd /go/to/your/home/dir   

git clone https://github.com/jetsonhacks/installROSXavier   

sudo apt update   
sudo apt upgrade   

cd installROSXavier  

./installROS.sh -p ros-melodic-desktop-full

./setupCatkinWorkspace.sh 

```

위의 명령어를 통해 ros는 모두 설치가 완료된다.

(Option)

위 코드를 통해서 ros 설치와 ros 개발환경을 설정할 경우 catkin_make를 통해서 설치되게 된다. 따라서 catkin build를 이용하려면 catkin clean을 통해서 기존 build 폴더들을 지워주고 새로 catkin build 해주면 된다. 

## 3. Mavros build
    
mavros build하는 방법은 2가지로 나뉜다. 

3-1) Using apt 

apt를 이용하는 방법은 매우 간단하다. 

```
sudo apt-get install ros-kinetic-mavros ros-kinetic-mavros-extras

wget https://raw.githubusercontent.com/mavlink/mavros/master/mavros/scripts/install_geographiclib_datasets.sh
   
./install_geographiclib_datasets.sh
```

3-2) Source installation
</br>
</br>
이 방법은 mavros source파일들을 직접 빌드하는 방법이다.   

```
sudo apt-get install python-catkin-tools python-rosinstall-generator -y

```

만약 catkin workspace 생성을 안했다면 다음을 따른다.

```
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws
catkin init
wstool init src
```
catkin workspace로 이동후 아래 절차를 진행

Install mavlink
```
rosinstall_generator --rosdistro melodic mavlink | tee /tmp/mavros.rosinstall
```

Install mavros 
```
rosinstall_generator --upstream mavros | tee -a /tmp/mavros.rosinstall
wstool merge -t src /tmp/mavros.rosinstall
wstool update -t src -j4
rosdep install --from-paths src --ignore-src -y
```

Install GeographicLib datasets

```
./src/mavros/mavros/scripts/install_geographiclib_datasets.sh

catkin build

source devel/setup.bash
```



   
   







   



