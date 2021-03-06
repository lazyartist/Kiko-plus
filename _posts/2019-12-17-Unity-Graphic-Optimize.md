---
layout: post
title: "Unity - Graphic Optimize"
description: ""
date: 2019-12-17 19:00:00+09:00
tags: [Unity]
comments: true
share: true
---

[TOC]



## 그래픽 최적화

### 최적화 시기
- 개발 초반부 기간을 제외한 모든 개발 기간

## 렌더링
- 컴퓨터가 주어진 데이터를 기반으로 이미지를 만들어 내는 과정
- 컴퓨터가 그림을 그리는 행위



## 그래픽스 API

-  다양한 제조사에서 제작된 GPU는 각각의 펌웨어 및 드라이버를 제공한다.
- 소프트웨어 개발자가 각 OS별로 모든 GPU들의 프로토콜에 맞추거 렌더링 소프트웨어를 만들어내는 것은 불가능에 가깝다.
- 따라서 그래픽스 API라는 것이 GPU의 드라이버를 이용하는 라이브러리들을 만들고 이를 API의 형태로 제공해서 소프트웨어 개발자들이 각각의 GPU 및 OS별로 따러 신경 쓰지 않고 렌더링 소프트웨어를 만들 수 있도록 해준다.

### 그래픽스 API 종류

- DirectX
  - 마이크로소프트에서 제작
  - Windows에서만 작동
  - 최신버전 DirectX12
- OpenGL
  - Windows, macOS, Linux 에서 작동
- OpenGL ES
  - 안드로이드, iOS 등 휴대용 기기의 OS에서 작동
  - WebGL을 통해 데스크톱의 웹브라우저에서도 OpenGL ES가 수행됨
- Metal
  - iOS에서 작동하는 차세대 그래픽스 API
- Vulkan
  - 안드로이드에서 작동하는 차세대 그래픽스 API


### 게임 엔진의 역할

- 게임 엔진을 통해 게임을 만들면 엔진이 알아서 각 플랫폼에 맞는 그래픽 API로 렌더링 처리를 해준다.
- 화면 렌더링 뿐만 아니라 게임 개발에 필수적인 시스템을 제공한다.
  - 씬의 하이어라키 구조
  - 애니메이션 시스템
  - 에셋 관리

### OpenGL(Open Graphics Library)
- 1992년 초에 컴퓨터 그래픽스 표준 규격을 기반으로 발표된 2D, 3D 그래픽스 표준 API 규격
- 크로스 플랫폼
- 크로노스 그룹에서 관리
  - 여러 미디어 기업들이 참여한 비영리 기관
  - 회원사가 납부한 회비로 운영됨
    - AMD, 엔비디아, 구글, 인텔, 유니티
- 게임을 제외한 렌더링 소프트웨어들에서는 멜티플랫폼을 지원해야 하므로 OpenGL이 널리 쓰임

###  OpenGL ES(Embedded System)

- 모바일 환경에서 2D, 3D 그래픽스를 위해 OpenGL 보다 더 작고 가벼운 별도의 표준
- 크로스 플랫폼
- 상위 표준인 OpenGL에서 잘 사용되지 않거나 대체 방법이 있는 것을 제외하고 축소하여 만든 서브셋(Subset)
- 모바일 환경을 위한 OpenGL의 경량화 버전
- 대부분의 모바일 기기에서 OpenGL ES로 그래픽스를 표현
- 버전
  - 1.0~1.1
    - 2003년 1.0 발표, 2004년 1.1 발표
    - 고정 기능 파이프라인(fixed function pipeline)을 사용
    - 쉐이처 프로그래밍이 불가능하고 한정된 방법으로만 라이팅이 가능
    - 현재는 사용되지 않음
  - 2.0
    - 2007 발표
    - 현재까지 널리 쓰임
    - 버텍스와 프레그먼트 쉐이더(vertex and fragment shader) 프로그래밍 가능
  - 3.x
    - 2012년 3.0 발표, 2014년 3.1 발표, 2015년 3.2 발표
    - 3.0에서 멀티 렌더 타깃 지원
    - 3.2에서 실수형(부동소수점, floating point) 렌더 타깃 지원으로 HDR 가능하므로 OpenGL ES를 최대한 최신 버전을 사용하는 것이 성능면에서 좋음
      - ?



### Metal

- iOS 전용 그래픽스 API
- OpenGL ES와 같이 크로스 플랫폼을 지원하려면 성능상 오버헤드(간접 처리 시간)가 늘어나기 때문에 iOS 전용 그래픽스 API를 만들어 오버헤드를 줄임
- 범용성을 보장하지 않지만 특정 하드웨어에서 성능을 보장
- iOS8, OSX 10.11 이상부터 지원
- 상태 변경과 드로우콜의 오버헤드를 대폭 줄일 수 있음
- 멀티쓰레드로 렌더링 관련 리소스를 생성하고 드로우콜을 보냄으로써 드로우콜에 대한 오버헤드가 줄어듦
- CPU 메모리의 데이터를 GPU 메모리로 전송하는 과정을 거치지 않고 사용하기 때문에 메모리를 효율적으로 관리할 수있음
  - 일반적으로 CPU와 GPU 메모리는 물리적으로 분리되어 있기 때문에 OpenGL은 이에 맞춰 비디오 메모리 영역이 따로 존재하는 기준으로 만들어져 있다.
  - 하지만 모바일 기기는 CPU, GPU 메모리가 분리되지 않고 하나로 존재하고 논리적으로 나누어 사용되기 때문에 이에 맞는 Metal이 더 좋은 성능을 낼 수있다.



## 드로우콜(DrawCall)

- CPU가 GPU에게 무언가를 그리라는 명령을 전송하는 것



## 상태변경

- 드로우콜 명령을 전송하기 전에 무엇을 어떻게 그려야 하는지 등의 명령을 전송하는 것



## 용어

- 쓰로틀링(throttling)
  - 기기의 발열이 심해져서 온도가 일정 이상 높아지면 발열을 낮추기 위해 자동으로 기기 성능을 낮추는 기능
- 


# 참고
- 유니티 그래픽스 최적화 스타트업