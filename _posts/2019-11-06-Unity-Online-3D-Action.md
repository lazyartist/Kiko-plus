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



## 캐릭터

### 캐릭터 컴포넌트

- 사람이나 몬스터 등 캐릭터 이동에 특화된 컴포넌트
- Add Component > Physics > Character Controller



### 캐릭터 이동

```c#
//목적지까지 방향 벡터를 구하고 정규화한다.
Vector3 direction = (destination - transform.position).normalized;
//목적지까지 거리를 구한다.
float distance = Vector3.Distance(transform.position, destination);
//매 프레임 이동할 속도 벡터를 구한다.
Vector3 velocity = direction * speed * Time.deltaTime;
//매 프레임 이동할 벡터를 현재 위치에 더해서 이동한다.
transform.position += velocity;
//목적지에 도착했는지 확인(간단히)
if(velocity.magnitude < 0.01f){
    //도착
}
//목적지에 도착했는지 확인(정확히)
//속도 벡터의 크기와 목적지까지의 거리의 차가 특정값(도착거리범위) 이하일 경우
//이 조건은 목적지를 지나친 경우도 판단할 수 있다.
if(distance - velocity.magnitude <= 0.01f){
    //도착
}

```



### 캐릭터의 가속, 감속 이동

- 가속
  - 속도가 점점 빨라지지만 최대속도에 다가갈 수록 천천히 빨라진다.
  - 목표속도가 현재속도보다 크다.
  - 현재속도와 목표속도의 차이값을 일정한 t값으로 선형보간하여 가속도로 사용한다.(속도 증가)
    - 따라서 현재속도는 점점 증가하고 차이값은 감소하므로 선형보간한 값이 점점 작아진다.(가속도 감소)
    - 선형보간 함수 Vector3.Lerp()로 ease 함수의 easeOutCubic과 비슷한 효과를 내고 있다.
      - Lerp : Linear Interpolation
- 감속
  - 속도가 점점 느려지지만 최소속도에 다가갈 수록 천천히 느려진다.
  - 목표속도가 현재속도보다 작다.
  - 계산 원리는 가속과 같다.




<svg xmlns="http://www.w3.org/2000/svg" width="662" height="221.9791717529297" style="
        width:662px;
        height:221.9791717529297px;
        background: #FFF;
        fill: none;">
        <svg xmlns="http://www.w3.org/2000/svg"><g><defs><pattern id=".3567723788908499" width="10" height="10" patternUnits="userSpaceOnUse"><path d="M 10 0 L 0 0 0 10" fill="none" stroke="lightgray" stroke-width="0.5"/></pattern></defs><rect width="100%" height="100%" fill="url(#.3567723788908499)" stroke="lightgray" stroke-width="0.5"/></g></svg>
        <svg xmlns="http://www.w3.org/2000/svg" class="role-diagram-draw-area"><g class="shapes-region" style="stroke: black; fill: none;"><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M96.12,180.94 C149.58,118.92 200.98,80.06 281.16,79.58" style="stroke: rgb(74, 144, 226); stroke-width: 1; fill: none;"/></g><g class="composite-shape axis2d" style="stroke-width: 1; stroke: rgb(0, 0, 0);"><path class="real" d=" M40.29,180.94 L598.57,180.94 M96.12,28.89 L96.12,197.84"/><path d=" M591.57,175.94 L598.57,180.94 L591.57,185.94"/><path d=" M91.12,35.89 L96.12,28.89 L101.12,35.89"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M96.12,180.94 L170.94,86.11" style="stroke: rgb(126, 211, 33); stroke-width: 1; fill: rgb(126, 211, 33);"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M134.53,135.53 L224.44,77.71" style="stroke: rgb(126, 211, 33); stroke-width: 1; fill: rgb(126, 211, 33);"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M180.49,96.59 L302.39,69.87" style="stroke: rgb(126, 211, 33); stroke-width: 1; fill: rgb(126, 211, 33);"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M591.5,181.94 C535.91,119.92 482.46,81.06 399.08,80.58" style="stroke: rgb(74, 144, 226); stroke-width: 1; fill: none;"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M591.5,181.94 L513.7,87.11" style="stroke: rgb(126, 211, 33); stroke-width: 1; fill: rgb(126, 211, 33);"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M551.56,136.53 L458.07,78.71" style="stroke: rgb(126, 211, 33); stroke-width: 1; fill: rgb(126, 211, 33);"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M503.77,97.59 L377.01,70.87" style="stroke: rgb(126, 211, 33); stroke-width: 1; fill: rgb(126, 211, 33);"/></g><g class="arrow-line"><path class="connection real" stroke-dasharray="" d="  M281.16,79.58 L399.08,80.58" style="stroke: rgb(74, 144, 226); stroke-width: 1; fill: rgb(126, 211, 33);"/></g><g/></g><g/><g/><g/></svg>
        <svg xmlns="http://www.w3.org/2000/svg" width="660" height="219.9791717529297" style="width:660px;height:219.9791717529297px;font-family:Asana-Math, Asana;background:#FFF;"><g><g><g><g><g><text x="52.361114501953125" y="42.21483534177145" style="white-space:pre;stroke:none;fill:rgb(0, 0, 0);font-size:17px;font-family:Asana-Math, Asana;font-weight:400;font-style:normal;dominant-baseline:auto;text-decoration:none solid rgb(0, 0, 0);">속도</text></g></g></g></g></g><g><g><g><g><g><text x="584.0208129882812" y="207.2981483300527" style="white-space:pre;stroke:none;fill:rgb(0, 0, 0);font-size:17px;font-family:Asana-Math, Asana;font-weight:400;font-style:normal;dominant-baseline:auto;text-decoration:none solid rgb(0, 0, 0);">시간</text></g></g></g></g></g><g><g><g><g><g><text x="275.201416015625" y="57.0411903222402" style="white-space:pre;stroke:none;fill:rgb(126, 211, 33);font-size:17px;font-family:Asana-Math, Asana;font-weight:400;font-style:normal;dominant-baseline:auto;text-decoration:none solid rgb(126, 211, 33);">기울기</text><g style="transform:matrix(1,0,0,1,329.59722900390625,56.4930419921875);"><path d="M123 111C93 111 66 83 66 53C66 23 93 -5 122 -5C154 -5 182 22 182 53C182 83 154 111 123 111ZM123 456C93 456 66 428 66 398C66 368 93 340 122 340C154 340 182 367 182 397C182 428 154 456 123 456Z" stroke="rgb(126, 211, 33)" stroke-width="8" fill="rgb(126, 211, 33)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g><g><g style="transform:matrix(1,0,0,1,337.22918701171875,56.4930419921875);"><path d="" stroke="rgb(126, 211, 33)" stroke-width="8" fill="rgb(126, 211, 33)" style="transform:matrix(0.017,0,0,-0.017,0,0);"></path></g><text x="341.45831298828125" y="57.0411903222402" style="white-space:pre;stroke:none;fill:rgb(126, 211, 33);font-size:17px;font-family:Asana-Math, Asana;font-weight:400;font-style:normal;dominant-baseline:auto;text-decoration:none solid rgb(126, 211, 33);">가속도</text></g></g></g></g></g></g><g><g><g><g><g><text x="162.83331298828125" y="149.0411903222402" style="white-space:pre;stroke:none;fill:rgb(126, 211, 33);font-size:17px;font-family:Asana-Math, Asana;font-weight:400;font-style:normal;dominant-baseline:auto;text-decoration:none solid rgb(126, 211, 33);">가속</text></g></g></g></g></g><g><g><g><g><g><text x="495.83331298828125" y="148.0411903222402" style="white-space:pre;stroke:none;fill:rgb(126, 211, 33);font-size:17px;font-family:Asana-Math, Asana;font-weight:400;font-style:normal;dominant-baseline:auto;text-decoration:none solid rgb(126, 211, 33);">감속</text></g></g></g></g></g></svg>
</svg>

$$
\begin{equation*}
Lerp( a,b,t) =a+_{(} b-a) \times t
\end{equation*}
$$


```c#
//특정 조건으로 목표속도를 설정한다.
if(distance > 1.0f){//목표지점과 거리가 1.0이상일 경우 가속
	goalVelocity = 10.0f;//목표속도 10.0f
} else {//목표지점과 거리가 1.0이하일 경우 감속
	goalVelocity = 0.0f;//목표속도 0.0f
}
//현재속도와 목표속도를 선형보간하여 가속도를 구한다.
accelate = Vector3.Lerp(currentVelocity, goalVelocity, 0.1f);//두 속도차의 10%씩 가속한다.
//현재속도에 가속도를 더한다.
currentVelocity += accelate;
```



### 캐릭터의 지면 이동

#### Character Controller 컴포넌트

- 지면과 충돌체크를 하여 지면 아래로 내려가지 않게 한다.
- 지면과 충돌처리로 통과하지 않게 해주고 지면의 경사도에 따라 올라갈 수 있는 곳과 아닌곳을 구분할 수 있다.
- Move() 함수로 이동할 수 있고 "수평 이동량(가속도) + 중력 이동량(가속도)"을 전달해줘야한다.
  - 중력 적용은 자동이 아니다.
- 지면에 닿아 이동할 때 지면의 작은 요철로 캐릭터가 튀어오를 수 있기 때문에 추가로 지면 방향으로 잡아 끄는 힘을 줘야한다.
  - 중력에 추가로 큰 값을 더한다.
  - 이 값은 deltaTime을 곱하는 의미가 없다.

#### 접지 판정

- isGrounded 변수 사용
- 전 이동에서 땅에 닿았으면 true, 공중이면 false



### 캐릭터 회전

#### Vector를 향하는 Quaternion 구하기

- Quaternion.LookRotation()을 이용

```c#
// 요약:
//     Creates a rotation with the specified forward and upwards directions.
//
// 매개 변수:
//   forward:
//     The direction to look in.
//
//   upwards:
//     The vector that defines in which direction up is.
[FreeFunction("QuaternionScripting::LookRotation", IsThreadSafe = true)]
public static Quaternion LookRotation(Vector3 forward, [DefaultValue("Vector3.up")] Vector3 upwards);
```



#### Quaternion 회전량 보간하기

- Quaternion.RotateTowards()를 이용

```c#
// 요약:
//     Rotates a rotation from towards to.
// 매개 변수:
//   from:
//   to:
//   maxDegreesDelta: 360도 기반 회전량, 프레임당 회전속도를 얻으려면 deltaTime을 곱해서 전달한다.
public static Quaternion RotateTowards(Quaternion from, Quaternion to, float maxDegreesDelta);
```



#### 목표방향으로 회전을 마쳤는지 확인

- 목표방향 벡터와 캐릭터 오브젝트의 정면 벡터의 내적으로 알 수 있다.
- 내적결과 1이면 같은 방향, 0이면 수직(직교), -1이면 반대이다.

```c#
// 요약:
//     Dot Product of two vectors.
// 매개 변수:
//   lhs:(Left-Hand Side)
//   rhs:(Right-Hand Side)
public static float Dot(Vector3 lhs, Vector3 rhs);
```



### 캐릭터 이동 코드

```

```





## 영어

- shininess
  - 미국: 시니니스, 영국: 샤이니니스
  - 번쩍번쩍 빛남
- warg
  - 와르그
  - 톨킨의 작품 세계관에서 바르그에서 따온 와르그라는 존재가 등장
  - 늑대처럼 생긴 사악한 생명체