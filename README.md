# Gstreamer_python

## Gstreamer 설치방법

### 만약 Virtual Machine 사용중이라면 아래 설치.
```
$ sudo apt-get install build-essential

$ sudo apt-get install bison

$ sudo apt-get install flex

$ sudo apt-get install libglib2.0-dev
```

### gstreamer 가 기본 설치되어있는지 확인
```
$ which gst-launch-1.0

아래와 같이 나오면 설치가 되어있는 것입니다.

/usr/bin/gst-launch-1.0
```
Ubuntu 18.04 에서는 위까지 기본 설치되어있었습니다.


```
기본적인 Gstreamer 라이브러리 설치

$ sudo apt-get install libgstreamer1.0-0 sudo apt-get install gstreamer1.0-plugins-base gstreamer1.0-plugins-good
```

```
추가 Gstreamer 라이브러리 설치 

$ sudo apt-get install gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly 

$ sudo apt-get install gstreamer1.0-libav gstreamer1.0-doc gstreamer1.0-tools

$ sudo apt-get install python-gst-1.0 python3-gst-1.0 

$ sudo apt-get install gir1.2-gst-rtsp-server-1.0
```

gstreamer 가 제대로 설치되었다면 아래가 잘 실행되어야한다.

```
$ gst-launch-1.0 videotestsrc ! autovideosink
```

ls /dev/video* 하면 연결된 video 출력 장치 목록이 뜬다.

## python rtsp server 실행방법.

해당 python 은 3.69 로 실행되었다.

### python script 를 편집기로 실행
```
self.server.set_address("192.168.10.142")
->해당 컴퓨터의 ip 주소를 입력하거나  local 인 127.0.0.1 을 입력해야된다. 아예 해당 줄을 지워주면 local 로 된다.
self.server.set_service("15000")
m.add_factory("/test", f)

위 세줄로 ip address, port, name 을 정해준다.

pipeline_str = "(v4l2src device=/dev/video2 ~~~) 으로 되어있는데 video2 를 실행하려는 것의 번호에 맞게 바꾸어준다. 

참고로 video2 는 반드시 usb 에 연결된 카메라여야된다. 

아니면 pipeline 형식에 맞지않아 작동하지 않는다. 카메라번호는 ls /dev/video* 로 확인한다.
```

### python script 가 있는 폴더로 터미널로 들어가서 python3 gst_rtsp_server.py 실행
```
VLC 에서 잘 작동하면 아래 Gstreamer 로 돌려보기

gst-launch-1.0 -v rtspsrc location=rtsp://192.168.10.54:15000/test latency=0 buffer-mode=auto ! decodebin ! videoconvert ! autovideosink sync=false
```

## 실행실패시 고려해야될 사항들
```
1. Virtual Machine 에서 gi 모듈이 import 되지않으므로 따로 설정해줘야 가능하다.

2. Virtual Machine 에서 samsung USB 웹캠을 사용하는 경우, 화면이 깨져서 나온다.

3. h264가 안되서 안되는 경우일 수도 있다. apt-get install gstreamer0.10-ffmpeg 로 설치해보자.

4. video 가 여러개인 경우 잘못된 video 를 틀고 있을 수 있다. ls /dev/video* 한 뒤 여러개이면, VLC 로 video0 부터 틀어보자.
```
## 추후 개발 및 공부 내용

```
1. Gstreamer pipeline 연구하며 다양한 동영상 포멧을 시도하며 그리고 latency 를 최대한 더 낮춰본다.

2. rtp sender 를 살펴본다.
```
