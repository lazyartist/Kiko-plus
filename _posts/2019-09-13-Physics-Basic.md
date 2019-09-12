---
layout: post
title: "Physics - Basic"
description: ""
date: 2019-09-13 19:00:00+09:00
tags: [physics]
comments: true
share: true
---

[TOC]



## 물리량

### 크기

- 스칼라(scalar)
- 길이(length), 질량(mass), 시간(time), 속력(speed,velocity), 에너지(Energy), 일(Work)

$$
l, m,t,v,E,W
$$



### 크기, 방향

- 벡터(vector)
- 위치(), 변위(delta), 속도(velocity), 가속도(accelation), 힘(Force), 운동량()
  - 위치가 왜 s인지는 모르겠다.
  - 운동량은 P가 맞나?

$$
\vec{s},\vec{\Delta},\vec{v},\vec{a},\vec{F},\vec{P}
$$



### '양'적인 개념

- 크기만 따지는 것



### '질'적인 개념

- '양'적인 개념을 기준에 따라 '질'을 따지는 것.
- 시간이라는 기준으로 물리량을 따지면 강도(세기)를 알 수 있다.



### 변화량

- 크기가 변한 양
  - 기준(시작)값 - 최종값
- 델타(Delta) 기호로 나타낸다.

$$
\Delta
$$



### 이동 거리와 변위

#### 이동 거리

- 물체가 실제로 움직인 거리
- 이리저리 움직인것 모두 포함

#### 변위

- 위치 변화량, 항상 직선상의 최소 거리
- 이리저리 이동한것은 취급하지 않고 처음과 끝의 직선상의 변화량만 따진다.



## 속력과 속도

### 속력

- 물체의 <u>빠르기(강도)</u>
- 단위 시간당 움직인 거리
- 스칼라

$$
속력=\frac{이동(변한) 거리}{이동에 걸린(변한) 시간}\\
v=\frac{\Delta s}{\Delta t}(m/s)
$$

### 속도

- 물체의 <u>빠르기(강도)</u>와 <u>방향</u>을 함께 나타낸 물리량
- 단위 시간당 움직인 거리와 <u>방향</u>
- 벡터

$$
속도=\frac{이동(변한)거리,방향}{이동에걸린(변한)시간}\\
\vec{v}=\frac{\Delta \vec{s}}{\Delta t}(m/s)
$$



### 평균속도와 순간속도

#### 평균속도

- 특정한 시간 범위에서 이동한 변위

$$
평균속도=\frac{변위}{시간}\\
\vec{v_{av}}=\frac{\Delta \vec{s}}{\Delta t}=\frac{\vec{s_2}-\vec{s_1}}{t_2-t_1}
$$


- 속도 변화에 <u>규칙성</u>이 있다면 다음과 같이 평균 속도를 쉽게 구할 수 있다

$$
평균속도=\frac{처음속도+나중속도}{2}\\
\vec{v_{av}}=\frac{\vec{v_0}+\vec{v_n}}{2}
$$



#### 순간속도

- 순간(0에 수렴하는 아주 짧은 시간동인) 이동한 변위

$$
순간속도=\frac{변위}{시간(0에 수렴)}\\
\vec{v}=\lim_{\Delta t \rightarrow 0 }\frac{\Delta \vec{s}}{\Delta t}
$$



## 상대속도

- 기준이 되는 물체의 속도를 0으로 생각했을 때 다른 물체의 속도
- 기준이 되는 물체의 속도를 0으로 만들고 만들기 위해 더하거나 빼준값을 다른 물체에 적용한다.

$$
v_{ab}=v_b-v_a
$$





## 가속도

- 물체의 속력 또는 속도가 변화된 강도
- 단위 시간단 변경된 속력 또는 속도
- 방향이 없으면 스칼라, 방향이 있으면 벡터

$$
가속도=\frac{변경된속력(속도)}{변경에걸린시간}\\
a=\frac{\Delta v}{\Delta t}\\
\vec{a}=\frac{\Delta \vec{v}}{\Delta t}
$$



### 평균가속도와 순간가속도

#### 평균가속도

- 특정한 시간 범위에서 변경된 가속도

$$
평균가속도=\frac{변경된가속도}{시간}\\
\vec{a_{aa}}=\frac{\Delta \vec{v}}{\Delta t}=\frac{\vec{v_2}-\vec{v_1}}{t_2-t_1}
$$

- 속도 변화에 <u>규칙성</u>이 있다면 다음과 같이 평균 속도를 쉽게 구할 수 있다

$$
평균속도=\frac{처음속도+나중속도}{2}\\
\vec{v_{av}}=\frac{\vec{v_0}+\vec{v_n}}{2}
$$



#### 순간가속도

- 순간(0에 수렴하는 아주 짧은 시간동인)에 변한 가속도

$$
순간가속도=\frac{변경된가속도}{시간(0에 수렴)}\\
\vec{a}=\lim_{\Delta t \rightarrow 0 }\frac{\Delta \vec{v}}{\Delta t}
$$



### 등가속도 운동

- 일정한 가속도가 더해지는 운동
- 중력가속도가 대표적
  - g = 9.8m/s²
- 



##  그래프 해석

- 서양말은 중요한 것이 앞에 나온다.
- 따라서 중요한 또는 최종적으로 구할 값을 y축으로 삼는다.
- 그래프의 기울기가 어떻게 변하는지를 보면 증감의 추세를 알 수 있다.


<svg xmlns="http://www.w3.org/2000/svg" width="662" height="454.28472900390625" style="
        width:662px;
        height:454.28472900390625px;
        background: #FFF;
        fill: none;
">
        <svg xmlns="http://www.w3.org/2000/svg"><g><defs><pattern id=".11691916777632905" width="10" height="10" patternUnits="userSpaceOnUse"><path d="M 10 0 L 0 0 0 10" fill="none" stroke="lightgray" stroke-width="0.5"/></pattern></defs><rect width="100%" height="100%" fill="url(#.11691916777632905)" stroke="lightgray" stroke-width="0.5"/></g></svg>
        <svg xmlns="http://www.w3.org/2000/svg" class="role-diagram-draw-area"><g class="shapes-region" style="stroke: black; fill: none;"><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M150,110 L230,30" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: rgb(164, 131, 131);"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M140,110 L240,110 M150,20 L150,120"/><path d=" M233,105 L240,110 L233,115"/><path d=" M145,27 L150,20 L155,27"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M290,110 C316,73.28 341,50.28 380,50" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M280,110 L380,110 M290,20 L290,120"/><path d=" M373,105 L380,110 L373,115"/><path d=" M285,27 L290,20 L295,27"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M440,110 C477,82.28 496,66.28 500,20" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M430,110 L530,110 M440,20 L440,120"/><path d=" M523,105 L530,110 L523,115"/><path d=" M435,27 L440,20 L445,27"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M290,210 L380,210" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M280,250 L380,250 M290,160 L290,260"/><path d=" M373,245 L380,250 L373,255"/><path d=" M285,167 L290,160 L295,167"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M150,320 L230,390" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M140,390 L240,390 M150,300 L150,400"/><path d=" M233,385 L240,390 L233,395"/><path d=" M145,307 L150,300 L155,307"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M290,320 C320,360.28 351,368.28 380,370" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M280,390 L380,390 M290,300 L290,400"/><path d=" M373,385 L380,390 L373,395"/><path d=" M285,307 L290,300 L295,307"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M440,320 C472,337.28 486,357.28 490,390" style="stroke: rgb(0, 0, 0); stroke-width: 1; fill: none;"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M430,390 L530,390 M440,300 L440,400"/><path d=" M523,385 L530,390 L523,395"/><path d=" M435,307 L440,300 L445,307"/></g><g/></g><g/><g/><!-- react-empty: 10451 --></svg>
        <svg xmlns="http://www.w3.org/2000/svg" width="660" height="452.28472900390625" style="width:660px;height:452.28472900390625px;font-family:Asana-Math, Asana;background:#FFF;"><g><g><text x="149.9132080078125" y="120.5555419921875" style="white-space:pre;stroke:none;fill:rgb(74, 144, 226);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;font-style:normal;dominant-baseline:text-before-edge;text-decoration:none solid rgb(74, 144, 226);">일정하게 증가</text></g></g><g><g><text x="295.32989501953125" y="120.5555419921875" style="white-space:pre;stroke:none;fill:rgb(74, 144, 226);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;font-style:normal;dominant-baseline:text-before-edge;text-decoration:none solid rgb(74, 144, 226);">점점 덜 증가</text></g></g><g><g><text x="451.32989501953125" y="122.5555419921875" style="white-space:pre;stroke:none;fill:rgb(74, 144, 226);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;font-style:normal;dominant-baseline:text-before-edge;text-decoration:none solid rgb(74, 144, 226);">점점 더 증가</text></g></g><g><g><text x="322" y="260.5555419921875" style="white-space:pre;stroke:none;fill:rgb(0, 0, 0);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;font-style:normal;dominant-baseline:text-before-edge;text-decoration:none solid rgb(0, 0, 0);">일정</text></g></g><g><g><text x="149.9132080078125" y="400.5555419921875" style="white-space:pre;stroke:none;fill:rgb(208, 2, 27);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;font-style:normal;dominant-baseline:text-before-edge;text-decoration:none solid rgb(208, 2, 27);">일정하게 감소</text></g></g><g><g><text x="295.32989501953125" y="400.5555419921875" style="white-space:pre;stroke:none;fill:rgb(208, 2, 27);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;font-style:normal;dominant-baseline:text-before-edge;text-decoration:none solid rgb(208, 2, 27);">점점 덜 감소</text></g></g><g><g><text x="451.32989501953125" y="402.5555419921875" style="white-space:pre;stroke:none;fill:rgb(208, 2, 27);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;font-style:normal;dominant-baseline:text-before-edge;text-decoration:none solid rgb(208, 2, 27);">점점 더 감소</text></g></g></svg>
</svg>



### 속도(v)와 변위(s)관계 그래프

- 부호는 방향을 나타낸다.
  - 음의 속도는 뒤로가는 속도, 음의 변위는 반대로 이동하는 변위이다.

<svg xmlns="http://www.w3.org/2000/svg" width="662" height="274.5555725097656" style="
        width:662px;
        height:274.5555725097656px;
        background: #FFF;
        fill: none;
">
        <svg xmlns="http://www.w3.org/2000/svg"><g><defs><pattern id=".7604072477914605" width="10" height="10" patternUnits="userSpaceOnUse"><path d="M 10 0 L 0 0 0 10" fill="none" stroke="lightgray" stroke-width="0.5"/></pattern></defs><rect width="100%" height="100%" fill="url(#.7604072477914605)" stroke="lightgray" stroke-width="0.5"/></g></svg>
        <svg xmlns="http://www.w3.org/2000/svg" class="role-diagram-draw-area"><g class="shapes-region" style="stroke: black; fill: none;"><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M130,110 L210,30" style="stroke: rgb(208, 2, 27); stroke-width: 1; fill: rgb(164, 131, 131);"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M10,110 L110,110 M20,20 L20,120"/><path d=" M103,105 L110,110 L103,115"/><path d=" M15,27 L20,20 L25,27"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M570,110 C596,73.28 621,50.28 660,50" style="stroke: rgb(208, 2, 27); stroke-width: 1; fill: none;"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M120,110 L220,110 M130,20 L130,120"/><path d=" M213,105 L220,110 L213,115"/><path d=" M125,27 L130,20 L135,27"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M230,110 L330,110 M240,20 L240,120"/><path d=" M323,105 L330,110 L323,115"/><path d=" M235,27 L240,20 L245,27"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M350,110 C387,82.28 406,66.28 410,20" style="stroke: rgb(208, 2, 27); stroke-width: 1; fill: none;"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M340,110 L440,110 M350,20 L350,120"/><path d=" M433,105 L440,110 L433,115"/><path d=" M345,27 L350,20 L355,27"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M20,60 L110,60" style="stroke: rgb(74, 144, 226); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M240,110 L320,30" style="stroke: rgb(74, 144, 226); stroke-width: 1; fill: rgb(164, 131, 131);"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M450,110 L550,110 M460,20 L460,120"/><path d=" M543,105 L550,110 L543,115"/><path d=" M455,27 L460,20 L465,27"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M560,110 L660,110 M570,20 L570,120"/><path d=" M653,105 L660,110 L653,115"/><path d=" M565,27 L570,20 L575,27"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M460,40 L540,110" style="stroke: rgb(74, 144, 226); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M130,150 L210,230" style="stroke: rgb(208, 2, 27); stroke-width: 1; fill: rgb(164, 131, 131);"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M10,150 L110,150 M20,240 L20,140"/><path d=" M103,155 L110,150 L103,145"/><path d=" M15,233 L20,240 L25,233"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M570,150 C596,186.72 621,209.72 660,210" style="stroke: rgb(208, 2, 27); stroke-width: 1; fill: none;"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M120,150 L220,150 M130,240 L130,140"/><path d=" M213,155 L220,150 L213,145"/><path d=" M125,233 L130,240 L135,233"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M230,150 L330,150 M240,240 L240,140"/><path d=" M323,155 L330,150 L323,145"/><path d=" M235,233 L240,240 L245,233"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M350,150 C387,177.72 406,193.72 410,240" style="stroke: rgb(208, 2, 27); stroke-width: 1; fill: none;"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M340,150 L440,150 M350,240 L350,140"/><path d=" M433,155 L440,150 L433,145"/><path d=" M345,233 L350,240 L355,233"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M20,200 L110,200" style="stroke: rgb(74, 144, 226); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M240,150 L320,230" style="stroke: rgb(74, 144, 226); stroke-width: 1; fill: rgb(164, 131, 131);"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M450,150 L550,150 M460,240 L460,140"/><path d=" M543,155 L550,150 L543,145"/><path d=" M455,233 L460,240 L465,233"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M560,150 L660,150 M570,240 L570,140"/><path d=" M653,155 L660,150 L653,145"/><path d=" M565,233 L570,240 L575,233"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M460,220 L540,150" style="stroke: rgb(74, 144, 226); stroke-width: 1; fill: none;"/></g><g/></g><g/><g/><!-- react-empty: 25140 --></svg>
        <svg xmlns="http://www.w3.org/2000/svg" width="660" height="272.5555725097656" style="width:660px;height:272.5555725097656px;font-family:Asana-Math, Asana;background:#FFF;"><g><g><g><g><g><g style="transform:matrix(1,0,0,1,2.125,26.77777099609375);"><path d="M166 420C187 420 203 421 229 424C118 304 76 221 76 121C76 44 122 -11 186 -11C324 -11 477 236 477 384C477 441 451 482 415 482C402 482 390 478 382 470L332 423L343 404C352 410 361 413 370 413C397 413 413 390 413 350C413 202 316 39 228 39C179 39 148 81 148 146C148 251 187 342 285 464L275 482C255 473 242 470 214 470C186 470 144 472 115 475L103 476C97 477 92 477 91 477C79 477 70 475 59 470C45 443 34 407 21 352L43 352L60 394C67 411 87 422 111 422C144 422 128 420 166 420Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g></g></g></g><g><g><g><g><g><g style="transform:matrix(1,0,0,1,112.125,26.77777099609375);"><path d="M31 148C26 97 20 62 9 16C47 -2 81 -11 116 -11C165 -11 211 7 262 47C313 87 334 124 334 174C334 228 302 257 228 271L185 279C125 290 106 307 106 348C106 401 151 442 208 442C249 442 287 424 303 397L303 342L326 342C330 377 334 404 345 455C306 474 278 482 245 482C193 482 132 452 84 404C58 377 47 352 47 316C47 260 78 228 144 215L207 203C251 195 267 177 267 138C267 73 221 29 150 29C115 29 84 40 56 64L56 148Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g></g></g></g><g><g><g><g><g><g style="transform:matrix(1,0,0,1,222.125,26.77777099609375);"><path d="M166 420C187 420 203 421 229 424C118 304 76 221 76 121C76 44 122 -11 186 -11C324 -11 477 236 477 384C477 441 451 482 415 482C402 482 390 478 382 470L332 423L343 404C352 410 361 413 370 413C397 413 413 390 413 350C413 202 316 39 228 39C179 39 148 81 148 146C148 251 187 342 285 464L275 482C255 473 242 470 214 470C186 470 144 472 115 475L103 476C97 477 92 477 91 477C79 477 70 475 59 470C45 443 34 407 21 352L43 352L60 394C67 411 87 422 111 422C144 422 128 420 166 420Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g></g></g></g><g><g><g><g><g><g style="transform:matrix(1,0,0,1,332.125,26.77777099609375);"><path d="M31 148C26 97 20 62 9 16C47 -2 81 -11 116 -11C165 -11 211 7 262 47C313 87 334 124 334 174C334 228 302 257 228 271L185 279C125 290 106 307 106 348C106 401 151 442 208 442C249 442 287 424 303 397L303 342L326 342C330 377 334 404 345 455C306 474 278 482 245 482C193 482 132 452 84 404C58 377 47 352 47 316C47 260 78 228 144 215L207 203C251 195 267 177 267 138C267 73 221 29 150 29C115 29 84 40 56 64L56 148Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g></g></g></g><g><g><g><g><g><g style="transform:matrix(1,0,0,1,442.125,26.77777099609375);"><path d="M166 420C187 420 203 421 229 424C118 304 76 221 76 121C76 44 122 -11 186 -11C324 -11 477 236 477 384C477 441 451 482 415 482C402 482 390 478 382 470L332 423L343 404C352 410 361 413 370 413C397 413 413 390 413 350C413 202 316 39 228 39C179 39 148 81 148 146C148 251 187 342 285 464L275 482C255 473 242 470 214 470C186 470 144 472 115 475L103 476C97 477 92 477 91 477C79 477 70 475 59 470C45 443 34 407 21 352L43 352L60 394C67 411 87 422 111 422C144 422 128 420 166 420Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g></g></g></g><g><g><g><g><g><g style="transform:matrix(1,0,0,1,552.125,26.77777099609375);"><path d="M31 148C26 97 20 62 9 16C47 -2 81 -11 116 -11C165 -11 211 7 262 47C313 87 334 124 334 174C334 228 302 257 228 271L185 279C125 290 106 307 106 348C106 401 151 442 208 442C249 442 287 424 303 397L303 342L326 342C330 377 334 404 345 455C306 474 278 482 245 482C193 482 132 452 84 404C58 377 47 352 47 316C47 260 78 228 144 215L207 203C251 195 267 177 267 138C267 73 221 29 150 29C115 29 84 40 56 64L56 148Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g></g></g></g><g><g><g><g><g><g style="transform:matrix(1,0,0,1,-2.888885498046875,236.77780151367188);"><path d="M555 243L555 299L51 299L51 243Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g><g style="transform:matrix(1,0,0,1,7.40277099609375,236.77780151367188);"><path d="M166 420C187 420 203 421 229 424C118 304 76 221 76 121C76 44 122 -11 186 -11C324 -11 477 236 477 384C477 441 451 482 415 482C402 482 390 478 382 470L332 423L343 404C352 410 361 413 370 413C397 413 413 390 413 350C413 202 316 39 228 39C179 39 148 81 148 146C148 251 187 342 285 464L275 482C255 473 242 470 214 470C186 470 144 472 115 475L103 476C97 477 92 477 91 477C79 477 70 475 59 470C45 443 34 407 21 352L43 352L60 394C67 411 87 422 111 422C144 422 128 420 166 420Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g></g></g></g><g><g><g><g><g><g style="transform:matrix(1,0,0,1,108.05557250976562,236.77780151367188);"><path d="M555 243L555 299L51 299L51 243Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g><g style="transform:matrix(1,0,0,1,118.34722900390625,236.77780151367188);"><path d="M31 148C26 97 20 62 9 16C47 -2 81 -11 116 -11C165 -11 211 7 262 47C313 87 334 124 334 174C334 228 302 257 228 271L185 279C125 290 106 307 106 348C106 401 151 442 208 442C249 442 287 424 303 397L303 342L326 342C330 377 334 404 345 455C306 474 278 482 245 482C193 482 132 452 84 404C58 377 47 352 47 316C47 260 78 228 144 215L207 203C251 195 267 177 267 138C267 73 221 29 150 29C115 29 84 40 56 64L56 148Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g></g></g></g><g><g><g><g><g><g style="transform:matrix(1,0,0,1,217.11114501953125,236.77780151367188);"><path d="M555 243L555 299L51 299L51 243Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g><g style="transform:matrix(1,0,0,1,227.40277099609375,236.77780151367188);"><path d="M166 420C187 420 203 421 229 424C118 304 76 221 76 121C76 44 122 -11 186 -11C324 -11 477 236 477 384C477 441 451 482 415 482C402 482 390 478 382 470L332 423L343 404C352 410 361 413 370 413C397 413 413 390 413 350C413 202 316 39 228 39C179 39 148 81 148 146C148 251 187 342 285 464L275 482C255 473 242 470 214 470C186 470 144 472 115 475L103 476C97 477 92 477 91 477C79 477 70 475 59 470C45 443 34 407 21 352L43 352L60 394C67 411 87 422 111 422C144 422 128 420 166 420Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g></g></g></g><g><g><g><g><g><g style="transform:matrix(1,0,0,1,328.0555419921875,236.77780151367188);"><path d="M555 243L555 299L51 299L51 243Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g><g style="transform:matrix(1,0,0,1,338.34722900390625,236.77780151367188);"><path d="M31 148C26 97 20 62 9 16C47 -2 81 -11 116 -11C165 -11 211 7 262 47C313 87 334 124 334 174C334 228 302 257 228 271L185 279C125 290 106 307 106 348C106 401 151 442 208 442C249 442 287 424 303 397L303 342L326 342C330 377 334 404 345 455C306 474 278 482 245 482C193 482 132 452 84 404C58 377 47 352 47 316C47 260 78 228 144 215L207 203C251 195 267 177 267 138C267 73 221 29 150 29C115 29 84 40 56 64L56 148Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g></g></g></g><g><g><g><g><g><g style="transform:matrix(1,0,0,1,437.11114501953125,236.77780151367188);"><path d="M555 243L555 299L51 299L51 243Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g><g style="transform:matrix(1,0,0,1,447.40277099609375,236.77780151367188);"><path d="M166 420C187 420 203 421 229 424C118 304 76 221 76 121C76 44 122 -11 186 -11C324 -11 477 236 477 384C477 441 451 482 415 482C402 482 390 478 382 470L332 423L343 404C352 410 361 413 370 413C397 413 413 390 413 350C413 202 316 39 228 39C179 39 148 81 148 146C148 251 187 342 285 464L275 482C255 473 242 470 214 470C186 470 144 472 115 475L103 476C97 477 92 477 91 477C79 477 70 475 59 470C45 443 34 407 21 352L43 352L60 394C67 411 87 422 111 422C144 422 128 420 166 420Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g></g></g></g><g><g><g><g><g><g style="transform:matrix(1,0,0,1,548.0555419921875,236.77780151367188);"><path d="M555 243L555 299L51 299L51 243Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g><g style="transform:matrix(1,0,0,1,558.3472290039062,236.77780151367188);"><path d="M31 148C26 97 20 62 9 16C47 -2 81 -11 116 -11C165 -11 211 7 262 47C313 87 334 124 334 174C334 228 302 257 228 271L185 279C125 290 106 307 106 348C106 401 151 442 208 442C249 442 287 424 303 397L303 342L326 342C330 377 334 404 345 455C306 474 278 482 245 482C193 482 132 452 84 404C58 377 47 352 47 316C47 260 78 228 144 215L207 203C251 195 267 177 267 138C267 73 221 29 150 29C115 29 84 40 56 64L56 148Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g></g></g></g></svg>
</svg>



### 가속도(a)와 속도(v)관계 그래프

<svg xmlns="http://www.w3.org/2000/svg" width="662" height="274.5555725097656" style="
        width:662px;
        height:274.5555725097656px;
        background: #FFF;
        fill: none;
">
        <svg xmlns="http://www.w3.org/2000/svg"><g><defs><pattern id=".7107199120273584" width="10" height="10" patternUnits="userSpaceOnUse"><path d="M 10 0 L 0 0 0 10" fill="none" stroke="lightgray" stroke-width="0.5"/></pattern></defs><rect width="100%" height="100%" fill="url(#.7107199120273584)" stroke="lightgray" stroke-width="0.5"/></g></svg>
        <svg xmlns="http://www.w3.org/2000/svg" class="role-diagram-draw-area"><g class="shapes-region" style="stroke: black; fill: none;"><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M130,110 L210,30" style="stroke: rgb(74, 144, 226); stroke-width: 1; fill: rgb(164, 131, 131);"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M10,110 L110,110 M20,20 L20,120"/><path d=" M103,105 L110,110 L103,115"/><path d=" M15,27 L20,20 L25,27"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M570,110 C596,73.28 621,50.28 660,50" style="stroke: rgb(74, 144, 226); stroke-width: 1; fill: none;"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M120,110 L220,110 M130,20 L130,120"/><path d=" M213,105 L220,110 L213,115"/><path d=" M125,27 L130,20 L135,27"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M230,110 L330,110 M240,20 L240,120"/><path d=" M323,105 L330,110 L323,115"/><path d=" M235,27 L240,20 L245,27"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M350,110 C387,82.28 406,66.28 410,20" style="stroke: rgb(74, 144, 226); stroke-width: 1; fill: none;"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M340,110 L440,110 M350,20 L350,120"/><path d=" M433,105 L440,110 L433,115"/><path d=" M345,27 L350,20 L355,27"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M20,60 L110,60" style="stroke: rgb(126, 211, 33); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M240,110 L320,30" style="stroke: rgb(126, 211, 33); stroke-width: 1; fill: rgb(164, 131, 131);"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M450,110 L550,110 M460,20 L460,120"/><path d=" M543,105 L550,110 L543,115"/><path d=" M455,27 L460,20 L465,27"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M560,110 L660,110 M570,20 L570,120"/><path d=" M653,105 L660,110 L653,115"/><path d=" M565,27 L570,20 L575,27"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M460,40 L540,110" style="stroke: rgb(126, 211, 33); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M130,150 L210,230" style="stroke: rgb(74, 144, 226); stroke-width: 1; fill: rgb(164, 131, 131);"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M10,150 L110,150 M20,240 L20,140"/><path d=" M103,155 L110,150 L103,145"/><path d=" M15,233 L20,240 L25,233"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M570,150 C596,186.72 621,209.72 660,210" style="stroke: rgb(74, 144, 226); stroke-width: 1; fill: none;"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M120,150 L220,150 M130,240 L130,140"/><path d=" M213,155 L220,150 L213,145"/><path d=" M125,233 L130,240 L135,233"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M230,150 L330,150 M240,240 L240,140"/><path d=" M323,155 L330,150 L323,145"/><path d=" M235,233 L240,240 L245,233"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M350,150 C387,177.72 406,193.72 410,240" style="stroke: rgb(74, 144, 226); stroke-width: 1; fill: none;"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M340,150 L440,150 M350,240 L350,140"/><path d=" M433,155 L440,150 L433,145"/><path d=" M345,233 L350,240 L355,233"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M20,200 L110,200" style="stroke: rgb(126, 211, 33); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M240,150 L320,230" style="stroke: rgb(126, 211, 33); stroke-width: 1; fill: rgb(164, 131, 131);"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M450,150 L550,150 M460,240 L460,140"/><path d=" M543,155 L550,150 L543,145"/><path d=" M455,233 L460,240 L465,233"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M560,150 L660,150 M570,240 L570,140"/><path d=" M653,155 L660,150 L653,145"/><path d=" M565,233 L570,240 L575,233"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M460,220 L540,150" style="stroke: rgb(126, 211, 33); stroke-width: 1; fill: none;"/></g><g/></g><g/><g/><!-- react-empty: 34737 --></svg>
        <svg xmlns="http://www.w3.org/2000/svg" width="660" height="272.5555725097656" style="width:660px;height:272.5555725097656px;font-family:Asana-Math, Asana;background:#FFF;"><g><g><g><g><g><g style="transform:matrix(1,0,0,1,2.125,26.77777099609375);"><path d="M271 204L242 77C238 60 236 42 236 26C236 4 245 -9 260 -9C283 -9 324 17 406 85L399 106C375 86 346 59 324 59C315 59 309 68 309 82C309 87 309 90 310 93L402 472L392 481L359 463C318 478 301 482 274 482C246 482 226 477 199 464C137 433 104 403 79 354C35 265 4 145 4 67C4 23 19 -11 38 -11C75 -11 155 41 271 204ZM319 414C297 305 278 253 244 201C187 117 126 59 94 59C82 59 76 72 76 99C76 163 104 280 139 360C163 415 186 433 234 433C257 433 275 429 319 414Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g></g></g></g><g><g><g><g><g><g style="transform:matrix(1,0,0,1,112.125,26.77777099609375);"><path d="M166 420C187 420 203 421 229 424C118 304 76 221 76 121C76 44 122 -11 186 -11C324 -11 477 236 477 384C477 441 451 482 415 482C402 482 390 478 382 470L332 423L343 404C352 410 361 413 370 413C397 413 413 390 413 350C413 202 316 39 228 39C179 39 148 81 148 146C148 251 187 342 285 464L275 482C255 473 242 470 214 470C186 470 144 472 115 475L103 476C97 477 92 477 91 477C79 477 70 475 59 470C45 443 34 407 21 352L43 352L60 394C67 411 87 422 111 422C144 422 128 420 166 420Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g></g></g></g><g><g><g><g><g><g style="transform:matrix(1,0,0,1,222.125,26.77777099609375);"><path d="M271 204L242 77C238 60 236 42 236 26C236 4 245 -9 260 -9C283 -9 324 17 406 85L399 106C375 86 346 59 324 59C315 59 309 68 309 82C309 87 309 90 310 93L402 472L392 481L359 463C318 478 301 482 274 482C246 482 226 477 199 464C137 433 104 403 79 354C35 265 4 145 4 67C4 23 19 -11 38 -11C75 -11 155 41 271 204ZM319 414C297 305 278 253 244 201C187 117 126 59 94 59C82 59 76 72 76 99C76 163 104 280 139 360C163 415 186 433 234 433C257 433 275 429 319 414Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g></g></g></g><g><g><text x="332.125" y="11.5555419921875" style="white-space:pre;stroke:none;fill:rgb(0, 0, 0);font-size:15px;font-family:Arial, Helvetica, sans-serif;font-weight:400;font-style:normal;dominant-baseline:text-before-edge;text-decoration:none solid rgb(0, 0, 0);">v</text></g></g><g><g><g><g><g><g style="transform:matrix(1,0,0,1,442.125,26.77777099609375);"><path d="M271 204L242 77C238 60 236 42 236 26C236 4 245 -9 260 -9C283 -9 324 17 406 85L399 106C375 86 346 59 324 59C315 59 309 68 309 82C309 87 309 90 310 93L402 472L392 481L359 463C318 478 301 482 274 482C246 482 226 477 199 464C137 433 104 403 79 354C35 265 4 145 4 67C4 23 19 -11 38 -11C75 -11 155 41 271 204ZM319 414C297 305 278 253 244 201C187 117 126 59 94 59C82 59 76 72 76 99C76 163 104 280 139 360C163 415 186 433 234 433C257 433 275 429 319 414Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g></g></g></g><g><g><g><g><g><g style="transform:matrix(1,0,0,1,552.125,26.77777099609375);"><path d="M166 420C187 420 203 421 229 424C118 304 76 221 76 121C76 44 122 -11 186 -11C324 -11 477 236 477 384C477 441 451 482 415 482C402 482 390 478 382 470L332 423L343 404C352 410 361 413 370 413C397 413 413 390 413 350C413 202 316 39 228 39C179 39 148 81 148 146C148 251 187 342 285 464L275 482C255 473 242 470 214 470C186 470 144 472 115 475L103 476C97 477 92 477 91 477C79 477 70 475 59 470C45 443 34 407 21 352L43 352L60 394C67 411 87 422 111 422C144 422 128 420 166 420Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g></g></g></g><g><g><g><g><g><g style="transform:matrix(1,0,0,1,-2.413177490234375,236.77780151367188);"><path d="M555 243L555 299L51 299L51 243Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g><g style="transform:matrix(1,0,0,1,7.87847900390625,236.77780151367188);"><path d="M271 204L242 77C238 60 236 42 236 26C236 4 245 -9 260 -9C283 -9 324 17 406 85L399 106C375 86 346 59 324 59C315 59 309 68 309 82C309 87 309 90 310 93L402 472L392 481L359 463C318 478 301 482 274 482C246 482 226 477 199 464C137 433 104 403 79 354C35 265 4 145 4 67C4 23 19 -11 38 -11C75 -11 155 41 271 204ZM319 414C297 305 278 253 244 201C187 117 126 59 94 59C82 59 76 72 76 99C76 163 104 280 139 360C163 415 186 433 234 433C257 433 275 429 319 414Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g></g></g></g><g><g><g><g><g><g style="transform:matrix(1,0,0,1,107.11111450195312,236.77780151367188);"><path d="M555 243L555 299L51 299L51 243Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g><g style="transform:matrix(1,0,0,1,117.40277099609375,236.77780151367188);"><path d="M166 420C187 420 203 421 229 424C118 304 76 221 76 121C76 44 122 -11 186 -11C324 -11 477 236 477 384C477 441 451 482 415 482C402 482 390 478 382 470L332 423L343 404C352 410 361 413 370 413C397 413 413 390 413 350C413 202 316 39 228 39C179 39 148 81 148 146C148 251 187 342 285 464L275 482C255 473 242 470 214 470C186 470 144 472 115 475L103 476C97 477 92 477 91 477C79 477 70 475 59 470C45 443 34 407 21 352L43 352L60 394C67 411 87 422 111 422C144 422 128 420 166 420Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g></g></g></g><g><g><g><g><g><g style="transform:matrix(1,0,0,1,217.5867919921875,236.77780151367188);"><path d="M555 243L555 299L51 299L51 243Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g><g style="transform:matrix(1,0,0,1,227.87847900390625,236.77780151367188);"><path d="M271 204L242 77C238 60 236 42 236 26C236 4 245 -9 260 -9C283 -9 324 17 406 85L399 106C375 86 346 59 324 59C315 59 309 68 309 82C309 87 309 90 310 93L402 472L392 481L359 463C318 478 301 482 274 482C246 482 226 477 199 464C137 433 104 403 79 354C35 265 4 145 4 67C4 23 19 -11 38 -11C75 -11 155 41 271 204ZM319 414C297 305 278 253 244 201C187 117 126 59 94 59C82 59 76 72 76 99C76 163 104 280 139 360C163 415 186 433 234 433C257 433 275 429 319 414Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g></g></g></g><g><g><g><g><g><g style="transform:matrix(1,0,0,1,327.11114501953125,236.77780151367188);"><path d="M555 243L555 299L51 299L51 243Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g><g style="transform:matrix(1,0,0,1,337.40277099609375,236.77780151367188);"><path d="M166 420C187 420 203 421 229 424C118 304 76 221 76 121C76 44 122 -11 186 -11C324 -11 477 236 477 384C477 441 451 482 415 482C402 482 390 478 382 470L332 423L343 404C352 410 361 413 370 413C397 413 413 390 413 350C413 202 316 39 228 39C179 39 148 81 148 146C148 251 187 342 285 464L275 482C255 473 242 470 214 470C186 470 144 472 115 475L103 476C97 477 92 477 91 477C79 477 70 475 59 470C45 443 34 407 21 352L43 352L60 394C67 411 87 422 111 422C144 422 128 420 166 420Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g></g></g></g><g><g><g><g><g><g style="transform:matrix(1,0,0,1,437.5867919921875,236.77780151367188);"><path d="M555 243L555 299L51 299L51 243Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g><g style="transform:matrix(1,0,0,1,447.87847900390625,236.77780151367188);"><path d="M271 204L242 77C238 60 236 42 236 26C236 4 245 -9 260 -9C283 -9 324 17 406 85L399 106C375 86 346 59 324 59C315 59 309 68 309 82C309 87 309 90 310 93L402 472L392 481L359 463C318 478 301 482 274 482C246 482 226 477 199 464C137 433 104 403 79 354C35 265 4 145 4 67C4 23 19 -11 38 -11C75 -11 155 41 271 204ZM319 414C297 305 278 253 244 201C187 117 126 59 94 59C82 59 76 72 76 99C76 163 104 280 139 360C163 415 186 433 234 433C257 433 275 429 319 414Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g></g></g></g><g><g><g><g><g><g style="transform:matrix(1,0,0,1,547.1111450195312,236.77780151367188);"><path d="M555 243L555 299L51 299L51 243Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g><g style="transform:matrix(1,0,0,1,557.4027709960938,236.77780151367188);"><path d="M166 420C187 420 203 421 229 424C118 304 76 221 76 121C76 44 122 -11 186 -11C324 -11 477 236 477 384C477 441 451 482 415 482C402 482 390 478 382 470L332 423L343 404C352 410 361 413 370 413C397 413 413 390 413 350C413 202 316 39 228 39C179 39 148 81 148 146C148 251 187 342 285 464L275 482C255 473 242 470 214 470C186 470 144 472 115 475L103 476C97 477 92 477 91 477C79 477 70 475 59 470C45 443 34 407 21 352L43 352L60 394C67 411 87 422 111 422C144 422 128 420 166 420Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g></g></g></g></svg>
</svg>



### 가속도(a), 속도(v), 변위(s) 관계 그래프

- 가속도가 일정하면 속도는 일정하게 증가하고 변위는 점점 더 증가한다.

<svg xmlns="http://www.w3.org/2000/svg" width="662" height="152.32638549804688" style="
        width:662px;
        height:152.32638549804688px;
        background: #FFF;
        fill: none;
">
        <svg xmlns="http://www.w3.org/2000/svg"><g><defs><pattern id=".6098815336406229" width="10" height="10" patternUnits="userSpaceOnUse"><path d="M 10 0 L 0 0 0 10" fill="none" stroke="lightgray" stroke-width="0.5"/></pattern></defs><rect width="100%" height="100%" fill="url(#.6098815336406229)" stroke="lightgray" stroke-width="0.5"/></g></svg>
        <svg xmlns="http://www.w3.org/2000/svg" class="role-diagram-draw-area"><g class="shapes-region" style="stroke: black; fill: none;"><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M300,110 L380,30" style="stroke: rgb(74, 144, 226); stroke-width: 1; fill: rgb(164, 131, 131);"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M180,110 L280,110 M190,20 L190,120"/><path d=" M273,105 L280,110 L273,115"/><path d=" M185,27 L190,20 L195,27"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M290,110 L390,110 M300,20 L300,120"/><path d=" M383,105 L390,110 L383,115"/><path d=" M295,27 L300,20 L305,27"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M400,110 L500,110 M410,20 L410,120"/><path d=" M493,105 L500,110 L493,115"/><path d=" M405,27 L410,20 L415,27"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M190,60 L280,60" style="stroke: rgb(126, 211, 33); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M410,110 C447,82.28 466,66.28 470,20" style="stroke: rgb(208, 2, 27); stroke-width: 1; fill: none;"/></g><g/></g><g/><g/><!-- react-empty: 38429 --></svg>
        <svg xmlns="http://www.w3.org/2000/svg" width="660" height="150.32638549804688" style="width:660px;height:150.32638549804688px;font-family:Asana-Math, Asana;background:#FFF;"><g><g><g><g><g><g style="transform:matrix(1,0,0,1,172.125,26.77777099609375);"><path d="M271 204L242 77C238 60 236 42 236 26C236 4 245 -9 260 -9C283 -9 324 17 406 85L399 106C375 86 346 59 324 59C315 59 309 68 309 82C309 87 309 90 310 93L402 472L392 481L359 463C318 478 301 482 274 482C246 482 226 477 199 464C137 433 104 403 79 354C35 265 4 145 4 67C4 23 19 -11 38 -11C75 -11 155 41 271 204ZM319 414C297 305 278 253 244 201C187 117 126 59 94 59C82 59 76 72 76 99C76 163 104 280 139 360C163 415 186 433 234 433C257 433 275 429 319 414Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g></g></g></g><g><g><g><g><g><g style="transform:matrix(1,0,0,1,282.125,26.77777099609375);"><path d="M166 420C187 420 203 421 229 424C118 304 76 221 76 121C76 44 122 -11 186 -11C324 -11 477 236 477 384C477 441 451 482 415 482C402 482 390 478 382 470L332 423L343 404C352 410 361 413 370 413C397 413 413 390 413 350C413 202 316 39 228 39C179 39 148 81 148 146C148 251 187 342 285 464L275 482C255 473 242 470 214 470C186 470 144 472 115 475L103 476C97 477 92 477 91 477C79 477 70 475 59 470C45 443 34 407 21 352L43 352L60 394C67 411 87 422 111 422C144 422 128 420 166 420Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g></g></g></g><g><g><g><g><g><g style="transform:matrix(1,0,0,1,392.125,26.77777099609375);"><path d="M31 148C26 97 20 62 9 16C47 -2 81 -11 116 -11C165 -11 211 7 262 47C313 87 334 124 334 174C334 228 302 257 228 271L185 279C125 290 106 307 106 348C106 401 151 442 208 442C249 442 287 424 303 397L303 342L326 342C330 377 334 404 345 455C306 474 278 482 245 482C193 482 132 452 84 404C58 377 47 352 47 316C47 260 78 228 144 215L207 203C251 195 267 177 267 138C267 73 221 29 150 29C115 29 84 40 56 64L56 148Z" stroke="rgb(0, 0, 0)" stroke-width="8" fill="rgb(0, 0, 0)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g></g></g></g></g></g></svg>
</svg>






# 참고

- 기초 물리학(뉴 탐스런)
  - https://www.youtube.com/playlist?list=PLK3h2AfW2qK2jRPiZ3a9SBbBJw4guTFUu