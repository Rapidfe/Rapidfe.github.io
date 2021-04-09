---
title: 임베디드 프로젝트 - 할리갈리 게임 모듈
author: rapidfe
date: 2021-01-10 09:44:00 +0900
categories: [Projects]
tags: [linux, raspberry pi]
math: true
---



# **내용**

---

디바이스 드라이버, 소켓통신, 멀티스레드, HTML의 기초를 실습하기 위해 고안한 할리갈리 게임 모듈 제작 프로젝트다.

#### **환경**

Windows Terminal(Ubuntu 20.04) 　←SSH→　 Raspberry pi 4 Model B(Raspbian)

#### **구현 내용**

1. Client간 채팅
2. 할리갈리 게임
3. 할리갈리에서의 종을 구현한 스위치 동작
4. 게임 진행을 시각적으로 보이기 위한 Sensor Hat 동작
5. 게임 진행을 실시간으로 보여주는 웹 페이지

![cap1](/assets/img/holli1.png)

![cap2](/assets/img/holli2.png)

![cap3](/assets/img/holli3.png)

![cap3](/assets/img/holli4.png)

#### **라즈베리파이 사용 정리**

1. 라즈베리파이에 라즈비안을 설치하고 와이파이를 설정한다.

   /etc/wpa_supplicant/wpa_supplicant.conf 에서 설정 파일을 볼 수 있다.

2. Windows Terminal에 우분투를 설정한다.

   Terminal에서 [Ctrl + ,]키로 settings.json을 열어 우분투를 설정할 수 있다.

   > [[참고 블로그]](https://noooop.tistory.com/entry/Windows-Terminal-%EC%9C%88%EB%8F%84%EC%9A%B0-%ED%84%B0%EB%AF%B8%EB%84%90%EC%97%90-%EC%9A%B0%EB%B6%84%ED%88%AC-%ED%83%AD-%EC%B6%94%EA%B0%80-%ED%95%98%EA%B8%B0)

3. Terminal에서 SSH로 라즈베리파이에 접속한다.

   ~/.ssh/config 에서 Host별 설정을 해두면 SSH 접속을 쉽게 할 수 있다.
   
   > [[참고 블로그]](http://taewan.kim/post/ssh_config/)

# **구현**

---

> [[소스 코드 Github]](https://github.com/Rapidfe/MyFiles/tree/master/term)
>
> [[채팅 구현 참고 블로그]](https://good-coding.tistory.com/17)
>
> [[WiringPi 참고 블로그]](https://hoho325.tistory.com/212)