---
layout: post
title: "Math - Graphics"
description: ""
date: 2019-03-21 19:00:00+09:00
tags: [game, math, math]
comments: true
share: true
---

#### 컬링(culling)

###### 시야 절두체 컬링(view frustum culling)

카메라에 보이지 않는 객체를 렌더링 하지 않는다.



###### 카메라 시야에 들어오는지 판단하는 방법

시야 절두체 평면의 안쪽에 있는지 평면 방정식에 대입해본다.

결과가 양수이면 절두체 안에 있는것이므로 렌더링한다.



###### 오클루전 컬링(occlusion culling)

다른 객체에 가려져 보이지 않는 객체를 렌더링 하지 않는다.

> 예) 벽이 있을 경우 카메라에서 벽 가장자리와 만나는 평면 2개를 그리면 벽과 새로 만든 벽 안쪽의 객체는 보이지 않기 때문에 그리지 않는다.







