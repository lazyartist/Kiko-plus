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
// Quaternion
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
// Quaternion
// 요약:
//     Rotates a rotation from towards to.
// 매개 변수:
//   from:
//   to:
//   maxDegreesDelta: 360도 기반 회전량, 프레임당 회전속도를 얻으려면 deltaTime을 곱해서 전달한다.
public static Quaternion RotateTowards(Quaternion from, Quaternion to, float maxDegreesDelta);
```



#### 목표방향으로 회전을 마쳤는지 확인

- Vector3.Dot()을 이용
- 목표방향 벡터와 캐릭터 오브젝트의 정면 벡터의 내적으로 알 수 있다.
- 내적결과 1이면 같은 방향, 0이면 수직(직교), -1이면 반대이다.

```c#
// Vector3
// 요약:
//     Dot Product of two vectors.
// 매개 변수:
//   lhs:(Left-Hand Side)
//   rhs:(Right-Hand Side)
public static float Dot(Vector3 lhs, Vector3 rhs);
```



### 캐릭터 이동 코드

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

//캐릭터 이동
public class CharacterMove : MonoBehaviour
{
    //중력값
    const float GravityPower = 9.8f;
    //목적지에 도착했다고 보는 정지 거리
    const float StoppingDistance = 5.6f;

    //현재 이동 속도
    Vector3 velocity = Vector3.zero;
    //캐릭터 컨트롤러의 캐시
    CharacterController characterController;
    //도착했는지 여부(true:도착, false:미도착)
    public bool arrived = false;
    //방향을 강제로 지시하는가?
    bool forceRotate = false;
    //강제로 향하게 하고 싶은 방향
    Vector3 forceRotateDirection;
    //목적지
    public Vector3 destination;
    //이동속도
    public float walkSpeed = 6.0f;
    //회전속도
    public float rotationSpeed = 360.0f;

    void Start()
    {
        characterController = GetComponent<CharacterController>();
        destination = transform.position;
    }

    void Update()
    {
        //이동속도 velocity를 갱신한다.
        if (characterController.isGrounded)
        {
            //test
            //destination = transform.position + Vector3.forward;
            //수평면에서 이동을 고려하므로 XZ만 다룬다.
            Vector3 destinationXZ = destination;
            //목적지와 현재 위치 높이를 똑같이 한다.
            destinationXZ.y = transform.position.y;

            //목적지까지 거리와 방향을 구한다.
            Vector3 direction = (destinationXZ - transform.position).normalized;
            float distance = Vector3.Distance(transform.position, destinationXZ);

            //현재 속도를 보관
            Vector3 currentVelocity = velocity;

            //목적지에 가까이 왔으면 도착
            if (arrived || distance < StoppingDistance)
            {
                arrived = true;
            }

            //이동속도
            if (arrived)
            {
                velocity = Vector3.zero;
            }
            else
            {
                velocity = direction * walkSpeed;
            }

            //이동속도를 부드럽게 보간 처리
            velocity = Vector3.Lerp(currentVelocity, velocity, Mathf.Min(Time.deltaTime * 2.0f, 1.0f));
            velocity.y = 0;

            if (!forceRotate)
            {
                //이동중이라면 이동하는 방향으로 회전한다
                if (velocity.magnitude > 0.1f && !arrived)
                {
                    Quaternion characterTargetRotation = Quaternion.LookRotation(direction);//지정하는 방향에 대한 회전값을 구하고
                    transform.rotation = Quaternion.RotateTowards(transform.rotation, characterTargetRotation, rotationSpeed * Time.deltaTime);//주어진 최댓값이내에서 목표 회전값까지 회전한 값을 구한다.
                }
            }
            else
            {
                //강제로 방향을 지정한다. (목표 지점을 항상 바라본다.)
                Quaternion characterTargetRotation = Quaternion.LookRotation(forceRotateDirection);
                transform.rotation = Quaternion.RotateTowards(transform.rotation, characterTargetRotation, rotationSpeed * Time.deltaTime);
            }
        }

        //중력
        velocity += Vector3.down * GravityPower * Time.deltaTime;//GravityPower값을 조절하여 Time.deltaTime을 곱하지 않게해도 된다.

        //땅에 닿아 있으면 지면을 꽉 누른다.(지면에 따라 튀어오를 수 있기 때문)
        Vector3 snapGround = Vector3.zero;
        if (characterController.isGrounded)
        {
            snapGround = Vector3.down;
        }

        characterController.Move(velocity * Time.deltaTime + snapGround);

        //도착
        if(characterController.velocity.magnitude < 0.1f)
        {
            arrived = true;
        }

        //강제 방향 변경 해제
        if(forceRotate && Vector3.Dot(transform.forward, forceRotateDirection) > 0.99f)
        {
            forceRotate = false;
        }
    }
}

```





## 입력

### Input 클래스

- Edit > Project Settings > Input에서 미리 지정한 이름으로 키, 마우스, 조이스틱의 값을 가져올 수 있다.
- Horizontal, Vertical, Fire1, Fire2, Jump, ... 

#### GetButtonDown

- 미리 지정한 버튼 이름으로 버튼이 눌렸는지 확인
- 눌린 프레임만 true

#### GetButtonUp

- 버튼이 올라온 프레임만 true

#### GetButton

- 버튼이 눌려있는 동안 true

#### GetAxis

- 스틱의 기울기를 -1~1 사이의 값으로 가져온다.
- Horizontal, Vertical

#### GetKeyDown

- 가상 매핑한 키이름이 아니라 키보드의 키 입력을 직접가져온다.
- Input.GetKeyDown(keyCode.Escape)

#### mousePosition

- 마우스 커서의 위치를 가지고 있다
- 좌표가 좌하단 부터 시작하며 (0, 0)이 시작좌표이기 때문에 전체 크기에서 -1해준 값이 끝 픽셀좌표이다.
  - 100x100 스크린이라면 좌하단(0,0), 우상단(99, 99)



### 슬라이드 조작

- 마우스 버튼을 누른 채 일정값 이상으로 이동하면 슬라이드로 간주
- 커서가 이동한 값을 deltaPosition으로 저장
- 마우스 버튼을 떼면 슬라이드 종료

```c#
//슬라이드 시작
if (Input.GetButtonDown("Fire1"))
{
	slideStartPosition = GetCursorPosition();
}
//슬라이드인지 아닌지 판단
if(Input.GetButton("Fire1"))
{
    if(Vector2.Distance(slideStartPosition, GetCursorPosition()) >= Screen.width * 0.1f)
    {
    	moved = true;
    }
}
//슬라이드 종료
if(!Input.GetButtonUp("Fire1") && !Input.GetButton("Fire1"))//버튼을 뗀 프레임까지 슬라이드로 간주
{
	moved = false;
}
```



### 슬라이드 시 마우스 이동량 구하기

- 매 프레임마다 마우스 위치를 기억
- 이전 프레임 마우스 위치와 현재 프레임 마우스 위치의 차



## 다른 게임 오브젝트에 있는 컴포넌트 가져오기

### public 변수에 Inspector에서 지정

- Inspector에서 public 변수에 게임 오브젝트를 드래그 드랍하면 해당 변수의 타입과 맞는 컴포넌트 또는 게임 오브젝트가 할당된다.



### FindObjectOfType(), FindObjectsOfTypes()로 찾는다

- 현재 인스턴스화된 컴포넌트에서 타입이 맞는 컴포넌트를 찾아준다.
- 느리다.

```c#
//하나의 객체만 찾는다
PlayerCtrl playerCtrl = FindObjectOfType<PlayerCtrl>();
PlayerCtrl playerCtrl = FindObjectOfType(typeof(PlayerCtrl)) as PlayerCtrl;
//모든 객체를 찾는다
PlayerCtrl[] plyaerCtrls = FindObjectsOfTypes<PlayerCtrl>();
PlayerCtrl[] plyaerCtrls = FindObjectsOfTypes(typeof(PlayerCtrl)) as PlayerCtrl;
```



### 게임 오브젝트에 태그를 설정하고 FindGameObjectWithTag()로 찾는다.

- 게임 오브젝트를 선택하고 Inspector에서 tag를 설정한다.
- 느리다.

```c#
GameObject go = GameObject.FindGameObjectWithTag("Player");
PlayerCtrl playerCtrl = go.GetComponent<PlayerCtrl>();
```



## Ray

- 게임 세계에서 보이지 않는 광선을 날려 광선이 닿는 물체와 위치를 조사하기 위한 방법
- 광선에 해당하는 Ray와 Ray와 닿는 물체를 조사하는 Physics.RayCast() 함수를 이용



### Ray 만들기

- Ray의 시작위치와 방향으로 만들 수 있다.

```c#
Ray ray = new Ray(startVector, directionVector);
```



### 카메라에서 화면 안쪽을 향하는 Ray 만들기

```c#
Ray ray = Camera.main.ScreenPointToRay();
```



### Ray 광선이 지면과 충돌한 위치 구하기

- Ray와 모델의 메쉬의 충돌을 검사하는게 아니라 Collider 컴포넌트의 형상과 충돌했는지 검사한다.
- 지면에는 Terrain Collider 컴포넌트가 있으므로 지면과 Ray이 충돌을 검사할 수 있다.

```c#
public static bool Raycast(Ray ray, out RaycastHit hitInfo, float maxDistance, int layerMask);
```

#### RaycastHit

- 충돌한 물체의 정보와 위치를 저장

```c#
    //
    // 요약:
    //     Structure used to get information back from a raycast.
    [NativeHeader("Runtime/Interfaces/IRaycast.h")]
    [NativeHeader("PhysicsScriptingClasses.h")]
    [NativeHeader("Runtime/Dynamics/RaycastHit.h")]
    [UsedByNativeCode]
    public struct RaycastHit
    {
        //
        // 요약:
        //     The Collider that was hit.
        public Collider collider { get; }
        //
        // 요약:
        //     The impact point in world space where the ray hit the collider.
        public Vector3 point { get; set; }
        //
        // 요약:
        //     The normal of the surface the ray hit.
        public Vector3 normal { get; set; }
        //
        // 요약:
        //     The barycentric coordinate of the triangle we hit.
        public Vector3 barycentricCoordinate { get; set; }
        //
        // 요약:
        //     The distance from the ray's origin to the impact point.
        public float distance { get; set; }
        //
        // 요약:
        //     The index of the triangle that was hit.
        public int triangleIndex { get; }
        //
        // 요약:
        //     The uv texture coordinate at the collision location.
        public Vector2 textureCoord { get; }
        //
        // 요약:
        //     The secondary uv texture coordinate at the impact point.
        public Vector2 textureCoord2 { get; }
        [Obsolete("Use textureCoord2 instead. (UnityUpgradable) -> textureCoord2")]
        public Vector2 textureCoord1 { get; }
        //
        // 요약:
        //     The Transform of the rigidbody or collider that was hit.
        public Transform transform { get; }
        //
        // 요약:
        //     The Rigidbody of the collider that was hit. If the collider is not attached to
        //     a rigidbody then it is null.
        public Rigidbody rigidbody { get; }
        //
        // 요약:
        //     The uv lightmap coordinate at the impact point.
        public Vector2 lightmapCoord { get; }
    }
```



#### layerMask

- 충돌 검사할 오브젝트의 layer번호를 비트 마스크로 지정한다.
- 이름으로 레이어 번호를 찾기 위해서 LayerMask.NameToLayer() 함수를 이용한다.

```c#
1 << 8;
1 << LayerMask.NameToLayer("Ground");
1 << LayerMask.NameToLayer("Ground") | 1 << LayerMask.NameToLayer("Player");
```



SendMessage

- 같은 게임 오브젝트의 다른 컴포넌트의 함수를 호출하는 함수
- 호출할 함수 이름과 인수를 받는다.
- 지정한 해당 함수가 다른 컴포넌트에 있으면 호출하고 없으면 무시한다.

```c#
SendMessage("FuncName", arg);//FuncName 함수를 호출한다.
```



## 카메라

### 대상 추적 카메라

#### 추적 대상의 위치

- 추적 대상의 위치(position)
- 추적 대상의 위치에서 카메라의 주시점까지의 보정값(offset)
- 이 두 값을 더한 위치값이 카메라가 실제 바라보는 위치(lookPosition=position+offset)

```c#
Vector3 lookPosition = lookTarget.position + offset;
```

#### 대상 추적 카메라 위치  및 회전

- 추적 대상의 주시점에서 바라본 카메라의 위치를 구한다(relativePos)
- 카메라의 위치는 기준이 되는 방향 벡터에 회전값을 적용하여 구한다.
- verticalAngle, horizontalAngle 값에 따라 카메라의 위치가 결정되고 이 값을 변경하면 대상을 중심으로 카메라가 원 궤적에서 이동한다.
- distance는 대상과 카메라의 거리에 해당한다.

```c#
//플레이어 위치를 기준으로하는 카메라 위치 구하기
Vector3 relativePos = Quaternion.Euler(verticalAngle, horizontalAngle, 0) * new Vector3(0, 0, -distance);
//카메라의 실제 위치
Vector3 cameraPos = lookPosition + relativePos;
```

#### 카메라를 타깃으로 향하기

- transform 클래스의 LookAt 함수를 이용

```
transform.LookAt(lookPosition);
```

#### 화면 슬라이드로 카메라 회전 갱신

- 화면을 슬라이드한 값과 1필셀당 회전할 각도를 곱해서 현재 카메라의 각도에 적용한다.

```c#
//화면 전체를 슬라이드 했을 때 회전할 양, 회전 최댓값
float rotAngle = 180.0f;
//픽셀당 회전할 각도
float anglePerPixel = rotAngle / Screen.width;
//이번 프레임에 슬라이드된 거리(픽셀)
Vector2 slideDelta;

//좌우 회전값
horizontalAngle += slideDelta.x * anglePerPixel;
//Repeat 함수로 회전값을 0~360도 사이에서 순환되도록 한다.
horizontalAngle = Mathf.Repeat(horizontalAngle, 360.0f);
//상하 회전값
verticalAngle -= slideDelta.y * anglePerPixel;
//Clamp 함수로 회전값을 -60~60도를 벗어나지 않게 한다.
verticalAngle = Mathf.Clamp(verticalAngle, -60.0f, 60.0f);
```



## 스크립트 처리 순서 바꾸기

- 같은 프레임에서 다른 스크립트의 갱신값을 입력값으로 사용할 경우 스크립트 사이에의 종속관계가 생기고 이 때 스크립트 실행 순서를 지정해줘야 일정한 결과 값을 기대할 수 있다.
- Edit > Project Setting > Script Execution Order
  - 순서를 정할 스크립트를 Inspector에 드래그 드랍
  - 가장 먼저 실행되어야할 스크립트를 Default Time 영역 위로 이동
    - Default Time은 순서를 지정하지 않은 스크립트가 실행되는 타이밍
  - 갱신된 값을 기준으로 갱신하는 스크립트는 Default Time 아래로 이동



## 애니메이션

### 매카님(Mecanim)

#### 애니메이션 대상 변경(Retargeting)

- 다양한 3D 모델에서 같은 애니메이션 데이터를 사용할 수 있는 기능
- 유니티에서는 인간형 모델(휴머노이드-Humanoid)에 사용

#### 상태 머신(State Machines)

- 애니메이션의 상태 전환을 유니티에서 편집할 수 있는 기능
- 애니메이션 간 전환 조건, 블랜딩 설정 등을 시각적으로 확인



### 애니메이션 대상 변경(Retargeting) 설정

- 모델 데이터 선택 > Inspector > [Player] Import Settings
  - Rig 탭 선택 > Animation Type > Humanoid 설정 > Apply
    - Animation Type
      - None: 애니메이션을 사용하지 않는 모델
      - Genenic: 휴머노이드가 맞지 않는 모델 데이터, 애니메이션 대상 변경 기능을 사용할 수 없음
      - Legacy: 유니티 3.x 버전과 호환을 위한 모드, 사용하지 않는다.
      - Humanoid: 애니메이션 대상 변경을 사용하기 위한 타입
- 애니메이션 데이터도 모델 데이터와 마찮가지로 Animation Type을 Humanoid로 설정



### 애니메이션 클립(Animation Clip)

- 유니티로 임포트한 애니메이션 데이터에서 실제로 이용할 데이터만 뽑아내 유니티에서 사용하기 쉽게 조정한 데이터
- 애니메이션 데이터 선택 > Inspector > [Player@Stay] Import Settings > Animation 탭 선택
- 클립에서는 애니메이션 데이터를 추출하는 시간을 조절할 수 있고 여러 애니메이션을 FBX 파일에 저장했다가 유니티에서 나누어 사용하는 것도 가능하다.
- 재생 설정
  - Loop Time
    - 애니메이션이 반복 재생됨
    - Loop Pose : 체크하면 애니메이션의 시작과 끝이 매끄럽다.
  - Root Transform Rotation
    - Bake Into Pose
      - 체크하면 루트 오브젝트의 Transform > Rotation에 애니메이션 값을 대입하지 않는다.
      - 스크립트 쪽에서 오브젝트의 회전을 제어할 때 사용
      - Body Transform의 Orientation을 따름
      - Root Orientation은 상수값
      - AnimationClip에 의해 게임 오브젝트는 일절 회전되지 않음
      - 비슷한 시작과 끝의 루트 방향을 가진 애니메이션 클립에만 옵션을 사용해야함
      - loop match가 녹색이면 사용하기 좋은 클립
        - 적합한 후보는 똑바로 걷거나 달리는 것
    - Based Upon
      - 회전의 루트 위치를 설정
      - Original : 애니메이션 데이터를 따름
      - Body Orientation : 상반신 전방을 루트의 Transform>Rotation에 맞춤
    - Offset
      - 회전의 보정값 설정
  - Root Transform Position(Y)
    - Bake Into Pose
      - 체크하면 루트 오브젝트의 Transform > Position > Y에 애니메이션 값을 대입하지 않는다.
      - 스크립트 족에서 캐릭터의 점프 등을 제어할 때 이용
      - 애니메이션의 루트 기준점의 Y값의 변화는 모두 무시됨
    - Based Upon(at Start)
      - 수직 방향의 기준이 되는 것을 설정
      - Original : 애니메이션 데이터를 따름
      - Center of Mass : 오브젝트의 중심을 루트의 Position > Y에 맞춤, 몸 기준점으로 일치
      - Feet : 발 위치에 맞춤
    - Offset
      - Position > Y의 보정값을 설정
  - Root Transform Position(XZ)
    - Bake Into Pose
      - 체크하면 루트 오브젝트의 Transform > Position > XZ에 애니메이션 값을 대입하지 않음
      - 스크립트 쪽에서 오브젝트의 수평 위치를 제어할 때 이용
      - 숨쉬기와 같이 캐릭터 위치를 변화시키지 않는 애니메이션을 사용하는 경우 이 옵션을 켜면 불필요한 계산을 방지할 수 있음.
  - loop match 아이콘
    - 애니메이션의 시작과 끝을 연결했을 때 깔끔하게 재생되는지 나타냄
  - Mirror
    - 애니메이션의 좌우 반전



### 애니메이션 이벤트

- 애니메이션 클립을 재생할 때 특정 타이밍에 게임 오브젝트에 설치한 스크립트의 이벤트 함수를 호출할 수 있다.
- Import Settings > Animation > Events
- 인수에는 0이나 1만 설정 가능
- 인수가 두 개 이상인 함수 호출 시 오류
- 오버로딩된 함수를 호출 시 먼저 만든 함수를 호출
- SendMessage 함수와 비슷하게 스크립트의 함수를 호출한다
  - Unity가 애니메이터 컨트롤러가 있는 오브젝트의 하위 오브젝트의 스크립트에 있는 함수까지 호출해주는듯..



### 애니메이션 전환

- 모델의 실제 애니메이션 처리는 Animator 컴포넌트가 담당
- 이 Animator 컴포넌트가 애니메이션을 제어하는데 필요한 데이터를 Animator Controller라 함
- Animator Controller 데이터에는 재생할 애니메이션, 애니메이션까리 전환 관계, 애니메이션 전환 조건이 저장됨



#### 애니메니션 컨트롤러(Animation Controller)

- 애니메이션 스테이트(Animation State)
  - 애니메이션의 재생 상태를 나타내는 요소
- Project 브라우저에서 애니메이션을 Animator 윈도우로 드래그 드랍하면 애니메이션 스테이트가 만들어진다.
- Ani State
  - 모든 스테이트에 같은 전환 설정을 하는 특수한 스테이트
- 디폴트 스테이트
  - 가장 먼저 선택되는 스테이트
  - 주황색 스테이트



#### 애니메이션 스테이트 전환 파라미터

- Animator Controller에 설정한다.
- Animator 윈도우 > Parameters
- Float, Int, Bool, Trigger
  - Trigger는 true/false 값을 갖지만 Bool 형과 달리 애니메이션이 전환되는 순간 자동으로 false가 됨

#### 애니메이션 스테이트 전환

##### 트랜지션(Transition)

- 어느 스테이트에서 어느 스테이트로 향하는지 나타내는 정보
- 화살표로 표시됨
- Inspector에 표시된 트렌지션의 파라미터 내에있는 Conditions에서 전환 조건을 지정



#### Animator에 Animator Controller 적용

- Animator 컨포넌트의 Controller에 Animator Controller 지정
- Apply Root Motion
  - 루트 오브젝트의 Transform에 애니메이션의 파라미터가 반영될지 여부





## 스켈레탈 애니메이션(Skeletal animation)

- 컴퓨터 애니메이션에서 캐릭터가 두 부분으로 표현되는 기술
  1. Skin or Mesh
     - 캐릭터를 그리는데 사용되는 표면
  2. Skeleton or Rig
     - 메시에 애니메이션을 적용하는데 사용되는 상호 연결된 본(bone)
- 리깅(Rigging)
  - 조인트 계층 구조를 만드는 과정
- 스키닝(Skinnig)
  - 스켈레톤을 메시에 연결하는 과정



## 충돌

### 컬라이더(Collider) 컴포넌트

- 오브젝트 간의 충돌을 판정하는 컴포넌트
- 리지드바디 컴포넌트와 함께 물리 시뮬레이션에서 사용
- 형태
  - 상자, 구, 캡슐, 메시(처리가 무겁다)

#### 컬라이더 속성

- Is Trigger
  - 컬라이더의 충돌 검출에만 이용
  - 물리적 작용을 하지 않음



#### 컬라이더 충돌 이벤트

- Is Trigger 설정된 경우
  - OnTriggerEnter
    - 다른 컬라이더가 이 Trigger에 접촉한 때
  - OnTriggerStay
    - 다른 컬라이더가 이 Trigger에 계속 닿아 있을 때
  - OnTriggerExit
    - 다른 컬라이더가 이 Trigger에서 떨어졌을 때
- Is Trigger 설정되지 않음 경우
  - OnCollisionEnter
    - 다른 컬라이더가 이 컬라이더에 접촉한 때
  - OnCollisionStay
    - 다른 컬라이더가 이 컬라이더에 계속 닿아 있을 때
  - OnCollisionExit
    -  다른 컬라이더가 이 컬라이더에서 떨어졌을 때



#### 컬라이더 충돌 이벤트 조건

- OnCollision 함수가 호출되려면 적어도 충돌한 오브젝트 중 어느 한쪽에는 리지드바디 컴포넌트가 설치되어 있어야 한다.
- OnTriggerEnter, OnTriggerStay, OnTriggerExit 함수가 정의된 컴포넌트가 disable 상태라도 함수는 호출된다.
- Collider 컴포넌트와 OnTriggerEnter, .. 등이 정의된 컴포넌트는 같은 게임오브젝트에 있어야한다.
  - 부모, 자식 관계에서는 호출되지 않는다.



### 리지드바디 컴포넌트(Rigidbody)

#### 리지드바디 속성

- Is Kinematic
  - 물리 시뮬레이션에 따라 이동할 필요가 없을 때 체크
  - 다른 오브젝트가 가하는 힘과 충돌에 영향을 받지 않음

#### 리지드바디(Rigidbody) 컴포넌트와 충돌 판정

- 리지드바디 컴포넌트는 물리 시뮬레이션을 하는 컴포넌트
- 리지드바디 컴포넌트는 처리가 무거운 컴포넌트이므로 필요한 곳에만 설치
- 게임 내에서 물리적으로 이동시키고 싶은 오브젝트에 설치
- 리지드바디 컴포넌트는 물리 엔진에 이 오브젝트가 이동할 가능성이 있다고 알려줌



#### 캐릭터 컨트롤러(Character Controller) 컴포넌트와 충돌 판정

- 리지드바디가 없어도 캐릭터 컨트롤러 컴포넌트가 있으면 다른 컬라이더와 충돌할 수 있다.
- 단, 캐릭터 컨트롤러끼리는 충돌 시 OnTriggerEnter... 등의 함수가 호출되지 않는다.



### Character Controller, Rigidbody, Collider의 충돌 연관성

|                      | Collider | Collider(Rigidbody) | Character Controller |
| :------------------: | :------: | :-----------------: | :------------------: |
|       Collider       |    X     |          O          |          O           |
| Collider(Rigidbody)  |    O     |          O          |          O           |
| Character Controller |    O     |          O          |          X           |

- Collider 끼리는 최소한 한 쪽에 Rigidbody가 있어야 충돌한다.
- Character Controller 끼리는 충돌하지 않는다.
- Collider와 Character Controller 컴포넌트는 같은 게임 오브젝트에 있을 시 충돌 이벤트가 발생한다.
  - 이 때 Collider에 대해 한 번, Character Controller에 대해 한 번 충돌 이벤트가 발생 하므로 최종적으로 충돌 이벤트가 두 번 발생하게 된다. 의도하지 않았을 경우 낭비가된다.
  - 부모 자식 관계도 상관없이 Collider와 Character Controller가 충돌하면 이벤트가 발생한다.



### 충돌 관련 레이어 설정

- 물체끼리 작용과 충돌 검출 여부를 레이어에서 설정 가능
- 컬라이더가 있는 게임 오브젝트의 레이어를 설정할 때 자식 오브젝트의 레이어는 변경하지 않아도 된다.



#### 레이어 설정

- Edit > Project Settings > Tags and Layers
  - Ground : 지면
  - EnemyHit : 적의 대미지를 받는 부분
  - PlayerHit : 플레이어의 대미지를 받는 부분
  - EnemyAttack : 적의 공격 부분
  - PlayerAttack : 플레이어의 공격 부분



#### 레이어의 접촉 검출(Layer Collision Matrix) 설정

-  Edit > Project Settings > Physics > PhysicsManager
  - Layer Collision Matrix에서 체크된 레이어끼리 충돌 판정을 함



### 충돌 스크립트

- AttackArea
  - 공격 판정 컬라이더와 같은 게임 오브젝트에 추가
  - 공격이 적중하면 OnTriggerEnter 이벤트를 받아서 대미지를 계산한 후 공격받은 HitArea에 대미지값을 전달
- HitArea
  - 공격을 받는 컬라이더와 같은 게임 오브젝트에 추가
  - AttackArea 스크립트에서 대미지값이 넘어오면 그 값을 루트인 부모 오브젝트에 전파(SendMessage)해서 그곳에 설치된 PlayerCtrl과 EnemyCtrl 컴포넌트에 대미지 값을 전달
- PlayerCtrl, EnemyCtrl
  - 대미지 처리를 구현
  - 체력에 대미지값을 적용



## 캐릭터 스테이트 구현 

- 플레이어는 한번에 한가지 상태만 가질 수 있다.
- Update 함수
  - 현재 상태 갱신 함수를 호출한다.
  - 상태가 갱신됐는지 확인한다.
- 상태가 갱신될 때 상태초기화 함수를 호출한다.



## AI
- 공격 대상을 검출할 컬라이더에 대상이 들어오면 공격 대상으로 지정하고 따라다님

- 공격 대상과 일정 거리 이상이면 공격대상까지 이동

- 공격 대상과 일정 거리 이하이면 공격

  







## 단축키

### Animator Window 바닥 움직이기

- Alt + 왼클릭





## Mathf

### Repeat

```c#
// 요약:
//     Loops the value t, so that it is never larger than length and never smaller than 0.
//     t의 값이 length를 넘어서면 0으로 돌아간 값을 반환한다.
public static float Repeat(float t, float length);
```

### Clamp

```c#
// 요약:
//     Clamps value between min and max and returns value.
//     value가 min, max를 넘지 않은 값을 반환한다.
public static int Clamp(int value, int min, int max);
```



## Random

```c#
/// <summary>
///   <para>Returns a random point inside a circle with radius 1 (Read Only).</para>
/// </summary>
public static Vector2 insideUnitCircle {
	get;
}
```


## 에러

### Camera.main이 null인 경우

- Camera 게임 오브젝트의 tag를 MainCamera로 지정한다





## 영어

- shininess
  - 미국: 시니니스, 영국: 샤이니니스
  - 번쩍번쩍 빛남
- warg
  - 와르그
  - 톨킨의 작품 세계관에서 바르그에서 따온 와르그라는 존재가 등장
  - 늑대처럼 생긴 사악한 생명체
- Clamp *[klæmp]*
  - 쇠집게, 고정시키다, 단속하다, 진압, 물리다
- angle
  - 각도, 관점, 모서리
- rotation
  - 회전, 교대, 순환, 로테이션
- skeletal
  - 해골의, 골격의, 해골 같은
- based upon ~
  - ~을 기반으로
- kinematic [*kìnəmǽtik*]
  - 운동학적인, 운동상의
- 



# 참고

- 반다이 남코 현역 개발팀이 알려주는 유니티 3D 온라인 액션 게임 공작소
- [루트 모션 - 작업 방법](https://docs.unity3d.com/kr/530/Manual/RootMotion.html)
- [Mecanim Animation](https://m.blog.naver.com/PostView.nhn?blogId=aeroviper&logNo=70169024232&proxyReferer=https%3A%2F%2Fwww.google.com%2F)
- [Preparing Humanoid Assets for export](https://docs.unity3d.com/kr/2019.3/Manual/UsingHumanoidChars.html