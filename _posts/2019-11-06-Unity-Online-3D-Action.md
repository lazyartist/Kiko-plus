---
layout: post
title: "Unity - Online 3D Action"
description: ""
date: 2019-11-06 19:00:00+09:00
tags: [Unity]
comments: true
share: true
---

[TOC]



## 머티리얼

- 머티리얼은 오브젝트의 표면의 색상을 결정한다.
- 따라서 텍스쳐와 노멀맵 그리고 쉐이더에 대한 정보를 가지고 있어야한다.



## SkyBox 설정

- Window > Rendering > Lighting Setting > Lighting(window) > Skybox Material 항목에 머티리얼을 설정
  - 머티리얼은 Shader가 Skybox/6 Sided 등의 스카이박스 머티리얼이어야 한다.



## 안개 설정

- Lighting(window) > Other Setting > Fog
  - Color
    - 안개의 색
  - Density
    - 안개의 농도



## 지형에 레이어 설정

- Terrain 오브젝트 선택하여 Inspector 표시
- Layer 클릭 > Add Layer 선택
- Tags & Layers에서 User Layer 8에 Ground 텍스트 입력
- Terrain 오브젝트를 다시 선택하여 Layer를 Ground로 변경





## 영어

- shininess
  - 미국: 시니니스, 영국: 샤이니니스
  - 번쩍번쩍 빛남
- warg
  - 와르그
  - 톨킨의 작품 세계관에서 바르그에서 따온 와르그라는 존재가 등장
  - 늑대처럼 생긴 사악한 생명체