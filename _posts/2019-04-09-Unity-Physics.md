---
layout: post
title: "Unity - Physics"
description: ""
date: 2019-04-09 19:00:00+09:00
tags: [physics]
comments: true
share: true
---


[TOC]



참고 : "유니티 2D 디펜스 게임은 이렇게 만든다"

참고 : <http://www.iforce2d.net/embox2d/testbed.html>



## 리지드바디(Rigid body)

- rigid
  - 경직된, 엄격한, 융통성이 없는, 굳어진
- 리지드바디
  - 강체
  - 모든 부분이 함께 이동하고 회전하는 물체
  - 형태가 고정돼 변하지 않는 이상적인 물체



## Physics2DSettings

- Gravity
  - 중력 가속도
- Default Material
- Time to Sleep
  - Rigidbody 2D가 슬립 상태로 들어가기까지 경과 시간(초)
  - 슬립 상태에서는 물리 엔진이 업데이트 되지 않는다.
- Linear Sleep Tolerance
  - Tolerance
    - 허용 오차
  - Time to Sleep 이후 슬립 상태로 들어가기 전에 가질 수 있는 최저 속도의 제한
- Angular Sleep Tolerance
  - Time to Sleep 이후 슬립 상태로 들어가는 각속도(회전속도)
- Layer Collision Matrix
  - 어떤 종류의 오브젝트가 다른 것들과 충돌하는지를 결정



## 물리 컴포넌트

- 리지드바디 : 물리 엔진 내의 리지드바디를 정의
- 콜라이더 : 리지드바디의 물리적 형태를 정의
- 조인트 : 리지드바디에 하나 이상의 제약을 부여
- 이펙터 ; 게임 월드 일부 영역의 물리적 특성을 변경해 그 영역 내의 모든 리지드바디에 영향을 미친다.



## 리지드바디 컴포넌트

- Body Type
  - Dynamic
    - 리지드바디가 모든 다이나믹 연산을 따른다
      - 다이나믹 연산
        - 모션을 일으키는 힘을 다룬다
    - 가장 많이 사용되고 모든 것과 충돌한다.
    - 연산 비용이 많이 든다.
  - Kinematic
    - 자체 모션을 위한 힘이 존재하지 않기 때문에 중력의 영향을 받지 않는다.
    - 모션은 직접 스크립트해야 한다.
    - 충돌할 수 있다.
    - 다이나믹 리지드바디와 충돌할 경우 고정된 것으로 간주하고 이는 무한 질량을 의미한다.
    - 질량과 관련된 프로퍼티는 사용할 수 없다.
    - 연산 비용이 적다.
  - Static
    - 무한 중력으로  전혀 움직이지 않는 오브젝트로 간주된다.
    - Static 리지드바디끼리는 충돌하지 않는다.
    - 연산 비용이 가장 적다.

| 파라미터의 종류 |    기능 \ 바디 타입     | Static | Kinematic | Dynamic |
| :-------------: | :---------------------: | :----: | :-------: | :-----: |
|    물리 엔진    |        머티리얼         |   O    |     O     |    O    |
|    물리 엔진    |      시뮬레이티드       |   O    |     O     |    O    |
|    다이나믹     |        자동 질량        |        |           |    O    |
|    다이나믹     |          질량           |        |           |    O    |
|    다이나믹     |  위치 이동에 대한 항력  |        |           |    O    |
|    다이나믹     |  회전 동작에 대한 항력  |        |           |    O    |
|    다이나믹     |       중력 스케일       |        |           |    O    |
|    물리 엔진    | 모든 키네마틱 접촉 사용 |   O    |     O     |         |
|    키네마틱     |        충돌 감지        |        |     O     |    O    |
|    물리 엔진    |       슬리핑 모드       |        |     O     |    O    |
|    물리 엔진    |          보간           |        |     O     |    O    |
|    키네마틱     |          제약           |        |     O     |    O    |
|    키네마틱     |        위치 동결        |        |     O     |    O    |
|    키네마틱     |        회전 동결        |        |     O     |    O    |
|    물리 엔진    |          정보           |   O    |     O     |    O    |



## 리지드바디 프로퍼티

- Material

  - 마찰, 반발 같은 충돌 프로퍼티를 결정하는 물리 머티리얼
- Simulated

  - 체크 시 리지드바디가 물리 엔진에 의해 계산된다.
- Use Auto Mass

  - 체크 시 콜라이더의 크기와 밀도를 기반으로 유니티가 오브젝트의 질량을 스스로 연산
- Mass

  - Use Auto Mass가 체크 해제 시 질량을 수동으로 설정
- Linear Drag
  - 위치 이동에 대한 항력 값
  - 0일 경우 이동을 멈추지 않는다.
- Angular Drag
  - 회전 동작에 대한 항력 값
  - 0일 경우 회전을 멈추지 않는다.
- Gravity Scale
  - 중력값에 대한 배율
  - 중력에 영향을 받을 경우 0이상 영향을 받지 않을 경우 0으로 설정
- Use Full Kinematic Contacts
  - Contacts
    - 접촉
  - 키네마틱 바디 타입에만 사용
  - 체크 시 다른 키네마틱 리지드바디와 충돌할 수 있다.
- Collision Detection
  - 유니티가 충돌을 감지하는 방식
  - Discrete
    - [diskríːt] 분리된, 별개의, 독립된 장치
    - 다른 물리 오브젝트의 위치를 기준으로 충돌 감지를 연산
    - 위치 업데이트 후 콜라이더가 겹친경우 충돌로 간주
  - Continuous
    - [kəntínjuəs] 연속적인, 지속적인, 계속되는
    - 위치뿐만 아니라 궤도 자체를 기준으로 충돌 연산
    - Discrete보다 연산 비용이 더 들어간다.
- Sleeping Mode
  - Never Sleep
    - 슬립 모드로 들어가지 않는다. 계속 awake 상태.
  - Start Awake
    - awake 상태로 시작
  - Start Asleep
    - asleep 상태로 시작
- Interpolate
  - 물리 연산의 수치적 불안정성으로 인해 움직임이 불규칙적으로 나타나는 현상을 보간하거나 추정하는 방법
  - None
    - 물리 연산의 결과를 보간, 추정하지 않고 그대로 사용한다.
  - Interpolate
    - [intə́ːrpəlèit] 삽입하다, 보충하다, 보간법을 쓰다.
    - 리지드바디의 이전 위치를 고려하여 보간한다.
  - extrapolate
    - [ikstrǽpəlèit] 외삽하다, 추론하다.
    - 리지드바디의 다음 위치를 고려하여 이를 반영한다.
- Constraints
  - [kənstréint] 제약, 조건, 제한, 구속, 문제
  - 리지드바디의 이동이나 회전을 제약한다.



## 리지드바디 움직이기

- Dynamic
  - AddForce, AddForceAtPosition, AddRelativeForce, AddTorque 등을 사용한다.
- Kinematic
  - transform.position을 직접 수정한다.



## 콜라이더

- Density
  - [dénsəti] 밀도, 농도, 조밀도
  - 리지드바디의 Use Auto Mass 체크 시에만 보인다.
  - 리지드바디의 질량에 영향을 미친다.
- Material
  - 마찰, 반발을 결정하는 물리 머티리얼
- IsTrigger
  - 체크 시 콜라이더가 이벤트 트리거로서 역할
  - 충돌에 사용되지 않고 다른 콜라이더가 영역 내에 들어올 때 이벤트를 트리거한다.
- Used By Effector
  - 콜라이더가 어태치된 이펙터에 의해 사용되고 있는지에 대한 옵션
- Offset
  - 로컬 좌표계에서의 콜라이더의 지오메트리 오프셋
  - 콜라이더가 어태치된 게임 오브젝트의 위치에서 얼마나 멀리 있는지를 지정



## 콜라이더 검출

- 부모에 리지드바디에 있고 자식 객체에 콜라이더가 붙어 있어도 충돌 검출한다.
- 특정 콜라이더만 검출하려면 레이어를 사용하고 레이어 마스크로 필터링해서 가져온다.
- 



## 볼륨 트리거를 위한 함수

OnTriggerEnter, OnTriggerStay, OnTriggerExit



## 충돌 정보를 위한 함수

OnCollisionEnter, OnCollisionStay, OnCollisionExit



## 조인트 컴포넌트

- Enable Collision
  - 양쪽 리지드바디 모두 콜라이더를 갖는다.
  - 두 콜라이더간에 충돌이 일어난다.
- Connected Rigid Body
  - 연결된 리지드 바디에 대한 참조
- Auto Configure Connected Anchor
  - 유니티가 상대 리지드바디의 앵커의 위치를 자동으로 결정
- Anchor
  - 현재 조인트의 앵커 위치
- Connected Anchor
  - 상대 리지드바디의 앵커 위치
  - 상대 리지드바디의 로컬 위치 기준
- Break Force
  - 조인트를 끊을 힘을 수치로 나타낸 값
  - 기본값은 Infinity로 끊어지지 않는다.
  - 끊어지면 조인트 컴포넌트가 게임 오브젝트에서 제거된다.
- Break Torque
  - 조인트를 끊을 토크 수치



## 조인트

- Distance Joint
  - 두 리지드바디를 일정한 간격으로 유지
- Fixed Joint
  - 두 리지드바디의 상대적 오프셋(거리 및 각도)을 유지
  - 단단한 스프링을 사용하지만 진동 수와 같은 스프링 값을 조정할 수 있다.
  - Damping Ratio
    - Damping 
      - [dǽmpiŋ] 제동하는
    - 스프링의 진동 진폭을 억제하는 정도를 정의
    - 스프링이 원래 위치로 얼마나 빨리 돌아오는지 결정
  - Frequency
    - 리지드바디가 이격 거리(Separation distance)에 도달할 때 스프링이 진자 운동하는 진동 수를 정의
    - 초당 사이클 수로 측정, 1~100M
- Friction Joint
  - Friction 마찰
  - 두 리지드바디 사이의 움직임을 늦춘다.
- Hinge Joint
  - Hinge 경첩, ~에 달려 있다.
  - 다른 리지드바디 또는 공간의 고정점을 중심으로 회전하도록 제한
  - Use Motor
    - 모터를 활성화
    - 조인트가 리지드바디에 토크를 능동적으로 적용할 수 있다.
  - Motor Speed
    - 모터의 속도를 지정
    - 초당 회전 각도(Degree)
  - Maximum Motor Force
    - Motor Speed에 도달할 때까지 모터가 적용할 수 있는 모터 속도를 지정
  - Use Limit
    - 체크 시 리지드바디의 회전 각도를 조인트가 제한
  - Lower Angle
    - 제한된 회전각의 최솟값
  - Upper Angle
    - 제한된 회전각의 최댓값
- Relative Joint
  - 두 리지드바디의 상대적 위치를 유지
  - Fixed Joint와 비슷하지만 모터 타입의 조인트로 직접 힘과 토크를 리지드바디에 전달한다.
- Slider Joint
  - 리지드바디의 움직임을 제한해 직선상에서 슬라이드만 할 수 있게 한다.
- Spring Joint
  - 순수한 Spring Joint
- Target Joint
  - 연결 리지드바디 대신 타깃을 갖는다.
  - 어태치된 리지드바디와 타깃을 일정 거리로 유지
  - 선형 힘만 적용
- Wheel Joint
  - 스피링과 모터 조인트의 조합
  - 모터로 바퀴를 회전시킬 수 있고 스프링으로 서스펜션을 시뮬레이션할 수 있다.



## 이펙터

다른 곳과는 다른 물리 법칙이 적용되는 특별한 영역을 지정

- Constant Force 2D
  - 리지드바디에 직접 적용되므로 엄밀히 이펙터는 아니다.
  - 리지드바디에 일정한 힘을 가한다.
- Area Effector 2D
  - 영역 내의 모든 리지드바디에 힘을 가한다
  - Used By Effector와 isTrigger가 true로 설정된 콜라이더가 필요
- Buoyancy Effector 2D
  - [bɔ́iənsi] 부력, 부양성
  - 유체를 시뮬레이션
  - Used By Effector와 isTrigger가 true로 설정된 콜라이더가 필요
  - Density
    - 유체의 밀도
    - 리지드바디의 밀도가 높으면 가라앉고 낮으면 뜬다.
- Point Effector 2D
  - 한 지점을 기준으로 밀어내거나 끌어당긴다.
  - 자석과 비슷
  - Used By Effector와 isTrigger가 true로 설정된 콜라이더가 필요
- Platform Effector 2D
  - 2D게임을 위한 플랫폼 이펙트를 제공
  - 플랫폼 아래에서는 통과 가능하지만 위에서는 통과 불가
  - Used By Effector와 isTrigger가 true로 설정된 콜라이더가 필요
- Surface Effector 2D
  - 지정된 표면을 따라 탄젠트 힘(접선 방향의 힘, tangential force)을 적용
  - 리지드바디를 운반하는 컨베이어 벨트와 같다.



## Physics Material 2D

충돌 시 생기는 마찰과 반발을 조정할 수 있는 머티리얼

- 콜라이더와 리지드바디 양쪽에 물리 머티리얼이 있을 경우
  - 콜라이더에 있는 머티리얼 우선
  - 콜라이더와 리지드바디 양쪽에 없으면 디폴트 Physics Material 2D가 할당, 이는 Physics Settings에서 설정 가능



## Physics2D의 주요 함수

- OverlapCircleAll
  - 원 안에 있는 모든 Collider2D 배열을 반환
- OverlapCircle
  - OverlapCircleAll와 비슷하지만 첫번째 콜라이더만 반환
- RaycastAll
  - 레이를 쏴서 충돌한 RaycastHit2D 배열을 반환
- Raycast
  - RaycastAll와 비슷하지만 첫번째 RaycastHit2D만 반환



## 리지드바디의 Simulated

리지드바디 컴포넌트가 추가, 삭제, Enable, Disable 될 때 마다 물리 엔진의 내부 메모리에 오브젝트를 생성, 삭제하므로 메모리와 프로세서 파워 비용이 발생한다.

Simulated를 켜고 끄는 것은 메모리를 변경하지 않고 단순히 물리 연산 대상에서 제외하므로 오버헤드가 발생하지 않는다.



## Physics 2D Raycaster

물리와 관련된 이벤트가 트리거될 때 호출될 함수를 작성할 수 있다.



## 물리 설정

- Velocity Iterations
  - 물리 오브젝트의 속도 연산의 반복 횟수
  - 높을 수록 정확하고 비용이 많이 든다.
- Position Iterations
  - 물리 오브젝트의 위치 연산의 반복 횟수
- Velocity Threshold
  - 이 값보다 낮은 상대 속도의 충돌을 비탄성 충돌로 간주한다.
  - 튕겨나오지 않는다.
- Max Linear Correction
  - Correction [kərékʃən] 교정, 정정, 수정, 조정
  - 제약에 대한 연산 시 사용되는 최대 선형 위치 보정
  - 0.0001~1,000,000
  - 오버슈트를 방지하는데 도움이 된다.
- Max Angular Correction
  - Max Linear Correction와 같고 각에 대한 보정
- Max Translation Speed
  - 오브젝트가 가질 수 있는 최대 속도
- Max Rotation Speed
  - 오브젝트가 가질 수 있는 최대 회전 속도
- Min Penetration For Penalty
  - Penetration [pènətréiʃən] 침투, 관통, 진출
  - 분리 충격이 가해지기 전에 허용되는 접촉에 따른 최소 관통 반경
  - 물체가 얼마나 깊게 서로를 뚫을 수 있는지를 결정한다.
  - 값이 높을수록 물체가 더 많이 뚫린다.
- Baumgarte Scale
  - 충돌 시 오브젝트가 포개진 경우 얼마나 빨리 해결할지를 결정하는 배율
  - 바움가르트의 제약 안정화 방법(Baumgarte's constraint stabilization method) 혹은 바움가르트 메소드
- Baumgarte Time Of Impact Scale
  - 임펙트가 일어난 시간의 중복이 얼마나 빨리 해결되는지를 결정하는 배율
- Queries Hit Trigger
  - true(기본값) : 레이캐스트가 트리거된 콜라이더와의 충돌을 감지한다.
  - false : 콜라이더만 감지하고 트리거된 콜라이더를 레이캐스팅에서 제외한다.
  - 트리거된 콜라이더 : 현재 프레임에서 이미 트리거된 것?
- Queries Start In Collider
  - true(기본값) : 콜라이더 내부에서 시작하는 레이캐스트가 감싸는 콜라이더와 히트를 포함한다.
  - false : 레이캐스트 시작점을 감싸는 콜라이더를 포함하지 않는다.
- Change Stops Playback
  - true : 충돌에 관련된 게임 오브젝트 중 하나라도 삭제되거나 이동된 경우 즉시 충돌에 대한 콜백 보고를 중지한다.
  - false(기본값)
- Gizmos
  - 에디터에서 콜라이더의 시각화에 대한 추가 옵션
  - 디버깅에 유용
  - 





