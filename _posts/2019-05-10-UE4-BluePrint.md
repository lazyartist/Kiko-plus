---
layout: post
title: "UE4 - BluePrint"
description: ""
date: 2019-05-10 19:00:00+09:00
tags: [UE4, BluePrint]
comments: true
share: true
---

[TOC]



## 액터

- UE4 공간에 배치되어 있는 오브젝트





## 좌표계

- z-up 좌표계
- xy : 평면
  - x : 우 +
  - y : 아래 +
- z : 위
  - z : 위 +
- UE4 좌표계 불일치
  - 월드 뷰포트 좌표계 : Y-front/Z-up
  - 액터의 로컬 뷰포트 좌표계 : X-front/Z-up
  - 따라서 Y-front/Z-up로 임포트한 애셋은 90도 회전되어 나온다.
  - 해결
    - 임포트 시 Y-front/Z-up으로 임포트
    - 블루프린트 또는 프로그램에서 제어하는 애셋은 블루프린트 컴포넌트 Mesh에서 90도 회전
    - 위 방법으로 안되면 임포트 시 오프셋 회전 설정





## 크기

- 단위 cm
- 1유닛 = 1cm





## 에디터 조작

- 뷰포트
  - 게임 스타일
    - MR + z or 1 : 줌인
    - MR + c or 3 : 줌아웃
  - Maya 스타일
    - F : 선택 오브젝트를 중앙에 표시
    - Alt + ML + Drag : 텀블(선택 오브젝트를 중심으로 회전)
    - Alt + MR + Drag : 돌리(선택 오브젝트에 가까워지거나 멀어짐)
    - Alt + MM + Drag : 트래킹(카메라 평행 이동)
  - 2D 뷰
    - MR : 스크롤
    - ML + MR or MM : 줌 인/아웃
  - 액터 옮길 때
    - Alt : 복제하며 옮김
    - Shift : 카메라도 함께 움직임
    - Alt + Shift : 복제와 카메라 이동
  - 몰입 모드 : F11
  - 마키 사용 : ctrl + alt + drag
  - 추천 레이아웃
    - 배치 작업 중심이므로 2분할(상단, 원근) 레이아웃이 좋다.
  - <http://api.unrealengine.com/KOR/Engine/UI/LevelEditor/Viewports/ViewportControls/>
- 블루프린트 에디터
  - ctrl + f : 이벤트 노드 찾기





## 요, 피치, 롤

- (모음의 방향으로 기억한다)
- 요(Yaw)
  - 좌우
- 피치(Pitch)
  - 상하
- 롤(Roll)
  - 바라보는 축(z) 중심으로 회전





## 게임 개발 워크플로(Workflow, 작업 흐름)

- 프로토타입
  - 게임의 재미 검증을 위해 테스트 가능할 정도로 간단히 만들어봄
  - 꼭 디지털일 필요는 없다.
- 프리 프로덕션
  - 게임의 일부분을 완벽하게 만듦
  - 실제 제품 수준으로 만들면서 워크플로를 검증, 개선
  - 버티컬 슬라이스(세로 쪼개기)
    - 스테이지를 쌓아올리고 세로로 잘라서 전체 스테이지에 필요한 기술들을 하나의 스테이지에 모두 구현해본다.
    - 제작의 소요를 산정하기 위한 검증과 기술 축적
    - [http://dnotewiki.com/note/index.php/%EB%B2%84%ED%8B%B0%EC%BB%AC_%EC%8A%AC%EB%9D%BC%EC%9D%B4%EC%8A%A4](http://dnotewiki.com/note/index.php/버티컬_슬라이스)
  - 이 단계에서 만들어진 프로그램, 툴, 파이프라인, 워크플로는 프로덕션 단계까지 이어진다.
  - 현실적 이유로 기술적인 우려가 있는 스테이지만 만들거나, 가장 광범위한 사양이 포함되는 스테이지만 만들 수도 있다.
- 프로덕션
  - 본격적인 완제품 제작을 위해 제작체제를 확대한다.





## 워크플로

- 워크플로가 반대로 진행되지 않게 한다.
- 빠른 이터레이션을 할 수 있게 한다.
  - 이터레이션 : 개션할 부분을 찾고 수정하는 과정





## 스테이지 제작 워크플로

- 컨셉 결정

  - 플롯(plot)
    - 스테이지와 줄거리를 구상한다.
  - 컨셉 아트
    - 최종 제품으로 만들기 전에 시각적으로 표현에서 전달하는 것을 목적으로 하는 일러스트의 한 형태

- 플레이 가능한 프로토타입 제작

  - 그레이박스(greybox)
    - 텍스처가 적용되지 않은 직육면체, 원기둥 같은 간단한 메시로 스테이지를 만드는 것.
    - 플레이 방식을 완성한다.
  - 메싱(Meshing)
    - 그레이박스 단계의 임시 메시를 정식 애셋으로 바꾸는 것.
    - 모노코크 방식보다 레고 블록 방식으로 만들어야 교체와 수정이 용이하다.
      - 모노코크 : 배경등을 일체형으로 만드는 것.
    - 그레이박싱 단계에서 블록 단위를 결정해서 작업해야 정식 에셋으로 교체가 쉽다.
    - 참고 : 히어로 애셋
      - 레고 블록처럼 재사용을 목적으로 하지 않고 한 번만 사용하는 것을 목적으로 만들어진 애셋
      - 다른 블록과의 연결과 레귤레이션(regulation)에 얽매이지 않는다.
  - 라이팅
    - 정식 라이트 작업
  - 폴리시(polish)
    - 전체적인 품질 향상
    - 파티클 이펙트, 사운드 배치
  - 워크플로를 반복하며 완성도를 높인다.
  - 제작 단계에서는 최적화에 많을 시간을 쓰지 않는다.
    - 게임의 외형이 어느정도 갖춰진 뒤 최적화를 수행하는 것이 효율적이다.
    - 애셋 제작 단계에서 메시의 폴리곤 카운트(트라이앵글의 수), 뼈의 수, 머티리얼의 스탭 수등의 제한을 두는 정도가 적당하다.






## BSP(Binary Space Patitioning - 이진 공간 분할법)

- 이진 공간 분할법은 하나의 공간을 특정한 최종 목적을 만족할 때까지 공간을 재귀적으로 2개씩 분할하는 과정이다.
- 분할 과정에서 BSP 트리라 불리는 트리 구조가 만들어진다.
- [https://ko.wikipedia.org/wiki/%EC%9D%B4%EC%A7%84_%EA%B3%B5%EA%B0%84_%EB%B6%84%ED%95%A0%EB%B2%95](https://ko.wikipedia.org/wiki/이진_공간_분할법)





## UE4 프로젝트에서 .gitignore

- 다음 파일 폴더만 있으면 프로젝트를 다시 세팅할 수 있다.
  - /Config, /Content, /Intermediate, *.uproject
  - .uproject 우클릭 "Generate Visual Studio project files" 
- .gitignore 파일 만들기
  - <https://www.gitignore.io/>
  - Visual Studio, Unreal Engine을 써넣고 생성
- 참고
  - <https://zenoahn.tistory.com/33>





## 라이팅

- 라이팅 제외
  - 라이트를 두지 않은 상태에서도 뷰포트의 시야를 확보



#### 게임 플레이중 라이트 변경

- F1
  - 와이어 프레임
- F2
  - 라이트 제외
- F3
  - 라이트 포함



## 브러시

- BSP 기능으로 만드는 형상을 브러시라 한다.
- 순서가 있어서 빼기 브러시는 더하기 브러시 다음에 추가되어야 한다.
- 입체성
  - 반입체
    - 불리언 연산이 일어나지 않는다.
    - 빼기 브러시의 영향을 받지 않는다.
    - 빼기 브러시로 깎아 만든 공간에 기둥 또는 장애물을 설치할 때 사용
  - 비입체
    - Collision 판정에 반응하지 않는다.





## 지오메트리 편집

- 브러시 또는 볼륨의 면, 변, 정점을 편집

- 편집

  - 면, 변, 정점을 편집

- 돌출

  - 이동할 때 마다 새로운 면을 추가






## PIE(Play In Editor)

- 선택된 뷰포트
  - 마지막으로 작업했던 뷰포트에서 게임이 플레이된다.
- 새 에디터 창
  - 새로운 에디터 창이 열리면서 게임이 플레이 된다.
  - 화면의 해상도와 화면 비율이 프로젝트에서 설정한 대로 나온다.
- 시뮬레이트
  - 플레이어 캐릭터가 나오지 않고 레벨 공간을 자유롭게 이동 가능하다.





## 이미지 파일 포맷

- TGA/TAGA(True vision advanced raster graphics adapter)
  - 무손실 압축 기반의 비트맵 이미지 파일 포맷
  - 32비트 컬러까지 저장
  - 알파채널 지원
  - 이미지 합성과 영상 편집을 위해 고안
  - 자막 파일이나 동영상 프레임을 '연속된 이미지 파일 시퀀스'로 만들 때 사용
  - 압축률이 안좋아 용량이 큼
  - 호환성이 좋아 윈도우, 리눅스, 매킨토시에서 사용
  - 특허에서 자유로움
- PNG(Portable Network Graphics)
  - 비손실 그래픽 파일 포맷
  - 8비트 알파 채널을 이용한 다양한 투명층 지원
  - 32비트 컬러
  - 알파값이 0인 필셀의 rgb값이 1(흰색) 이다.
    - 이로 인해 유니티에서 png를 불러오면 경계부분에 흰색이 묻어 날 수 있다.
    - 다른 rgb 채널에서 1이하의 값을 넣을 수 있지만 결국 그 컬러가 묻어난다.
    - 해결
      - rgb 채널에서 경계의 색으로 투명한 곳을 채우거나 TGA 파일 포맷을 사용한다.
      - 유니티에서는 텍스처 설정에서 "Alpha Is Transparency"를 체크한다.
      - 얼리얼에서는 자동으로 경계의 색을 확장하므로 이런 문제가 없다.
-  참고
  - <https://itrum.tistory.com/72>
  - <https://ko.wikipedia.org/wiki/PNG>
  - <https://chulin28ho.tistory.com/362>
  - <https://chulin28ho.tistory.com/363>





## FBX 임포트 옵션

- Mesh > Import as Skeletal
  - 뼈대가 없는 fbx를 스켈레탈 메시로 강제 임포트
- Mesh > Auto Generate Collision
  - 콜리전을 자동 생성
- Mesh > Normal Import Method
  - 노멀을 fbx에서 임포트할지 다시 재연산할지를 선택
- Transform > Import Translation
  - 설정한 오프셋만큼 모델의 원점을 이동
- Transform > Import Rotation
  - 좌표계가 다른 DCC에서 만든 모델의 경우 보정해서 임포트한다.
- Transform > Import Uniform Scale
  - 설정한 배율로 모델의 크기를 변경
- Material > Import Materials
  - fbx 데이터를 임포트할 때 머티리얼 정보가 있으면 UE4 머티리얼을 자동으로 생성하고 메시에 적용
- Material > Import Textures
  - fbx에 포함된 텍스처와 같은 경로에 이미지 파일일 있다면 동시에 임포트를 수행





## 스태틱 메시 에디터

- 라이트 이동
  - L + ML + 마우스 이동





## DCC 툴에서 콜리전 추가

- 외부 DCC 툴에서 객체의 이름을 특정 규칙으로 시작하면 UE4에서 콜리전으로 인식한다.
  - UCX_
    - 볼록 형태
  - UBX_
    - 박스 형태
  - USP
    - 구 형태
- 스켈레탈 메시는 외부에서 생성한 콜리전을 가지고 올 수 없고 언리얼 에디터에서 만들어야한다.





## 리디렉터

- 애셋을 이동시고 기존의 경로로 접근해도 새로운 경로로 접근할 수 있게 해주는 기능.
- 처리에 부하가 걸리므로 최종적으로 수정해줘야한다.





## 퍼시스턴스 레벨

- 현재 레벨 에디터에서 읽어 들이고 있는 레벨
- 서브 레벨의 읽기와 언로드를 관리
- 여러 개의 서브 레벨에서 공통으로 사용하는 액터를 배치할 때 사용
- 퍼시스턴스 레발은 언로드 불가, 서브레벨은 언로드 가능





## 레이어

- 폴더처럼 액터를 분류하는 기능
- 하나의 액터를 여러 레이어에 추가할 수 있다.
- 에디터만의 정보
- 게임 중에 레이어로 제어하기는 안됨
- 월드 아웃라이너 패널의 계층 구조에 영향을 주지 않음





## 디버그 카메라

- 게임 플레이 시 게임 카메라를 자유롭게 조작할 수 있는 모드
- `키를 눌러 콘솔 명령 입력 화면이 나오면 ToggleDebugCamera를 입력





## 레벨 블루프린트

- 툴바 > 블루프린트 > 레벨 블루프린트 열기
- Tick 이벤트
  - 각 프레임에서 화면을 새로 그리는 시점 직전에 발생
- 스크립트가 맵과 함께 저장
  - 따라서 스크립트를 재사용하기 힘듦





## 클래스 블루프린트

- 스크립트가 액터와 함께 저장
  - 따라스 스크립트 재사용은 쉽지만, 맵에 있는 액터에 접근이 힘듦





## 액터를 움직이는 방법

- 좌료를 매 프레임마타 변경
  - 등속 직선 운동에 적합
- 이동 컴포넌트에 파라미터 전달
  - 관성 등 현실 세계를 반영한 움직임
  - MovementComponent 사용
    - CharacterMovement, RotatingMovement, ProjectileMovement
- 미리 정의한 시퀸서로 이동
  - 키 프레임을 지정하고 특정 시간에서의 위치와 방향을 자동으로 보간하여 움직임
  - 방식
    - 마티네(Matinee)
      - 에디터에서 <u>컷씬</u>을 생성하고 재생하기 위한 구조
        - 컷씬
          - 게임 중간에 3D 모델들이 움직이며 스토리 등을 전달
          - 시네마틱 영상은 동영상을 재생하는 것이므로 컷씬과는 다르다.
    - 타임라인(Timeline)
      - 키 프레임을 사용
- 물리 엔진 이용
  - 게임 오브젝트의 움직임을 물리 엔진이 처리
- 루트 모션 이용
  - 외부 툴에서 만든 애니메이션을 UE4에서 재생





## 입력 추출

- UE4 4.10.2 기준으로 게임패드 또는 키 스위치의 상태(현재 눌리고 있는지)를 직접 추출하는 것은 불가능하다.
  - 따라서 오래 누르기, 동시에 누르기, 슬라이드 입력 등은 다루기 힘들다.
- 이런 입력이 필요하면 C++로 하드웨어의 입력 상태를 처리해야한다.





## 입력 매핑

- 가상의 버튼 이름을 설정하고 이에 물리적 키를 매핑하는 방법
- 이식과 사양 변경이 쉽다.
- UE4에서는 프로젝트 세팅에서 설정한다.
  - 툴바 > 세팅 > 프로젝트 세팅 > 엔진 > 입력
- 세팅
  - 액션 매핑
    - 디지털 입력
- 게임패드
  - Xbox One/360 레이아웃을 따른다.
  - 게임패드 전면 아래, 위, 왼쪽, 오른쪽 버튼은 X, Y, A, B버튼을 의미한다.
- 입력 축에서의 Scale 프로퍼티
  - 입력된 값에 곱해주는 값
  - 하드웨어 값 * Scale = 입력된 값
  - 입력을 역전하거나 크기를 조절한다.





## 블루프린트 노드

- 연결 끊기
  - Alt + 노드 클릭





## 페르소나 애니메이션 에디터

- 애니메이션과 관련된 작업을 수행할 수 있는 에디터
- 모프 타겟 프리뷰어
  - 얼굴 표정 변화, 차량의 손상 등의 표현에 사용되는 기술





## GameMode, PlayerPawn, PlayerController의 관계

- 조작자를 사람과 AI 중에서 선택할 수 있도록 Pawn은 반드시 Controller 액터로 운용해야한다.
- PlayerController가 하드웨어 입력을 받고 Pawn에 반영하는 것이 정석이지만 작은 게임에서는 불편하므로 Pawn에서도 입력을 받을 수 있다.
- 게임이 시작되면 PlayerPawn, PlayerController가 공간에 존재하며 회전과 관련된 프로퍼티를 가진다.
- Pawn과 Controller의 방향
  - Controller도 액터의 일종이므로 맵에서 위치와 방향을 갖으며 일반적으로 Pawn에 붙어 움직인다.
  - UE4의 캐릭터 방향은 Pawn의 방향을 기반으로 결정
  - 플레이어의 Aiming은 Controller의 방향으로 결정



## 피직스 애셋(Physics Asset)

- 스켈레톤의 관절과 관절 사이에 콜리전을 추가해 애니메이션과 함께 움직이게 하는 애니메이션 대응 콜리전.
- 캐릭터 콜리전이 부분적으로 작동해야하는 경우 사용.
- 지형 콜리전과 캐릭터 콜리전을 따로 만든다.
- 컨스트레인트 모드
  - Angular Limits
    - Angular Swing 1Motion
      - 빨간색 원주의 스윙(롤 회전)
    - Angular YMotion
      - 초록색 원주의 스윙(요 회전)
    - Angular Swing 2Motion
      - 파란색 원주의 스윙(피치 회전)



## zero extend

- 작은 크기의 데이터를 큰 크기의 데이터로 변경할 때 데이터가 모자라는 부분을 0으로 채우는 방식





## UE4의 콜리전

- 블록
  - 물리적인 현상이 일어나는 충돌
- 오버랩
  - 물리적인 현상이 일어나지 않는 충돌
  - 단순히 겹치는 것만 검출
  - 트리거
    - 오버랩 활용을 주 목적으로 하는 콜리전
    - 이벤트 박스라고도 한다.





## 컴포넌트



- 루트 컴포넌트
  - 컴포넌트 계층 구조에서 가장 위에 있는 컴포넌트
  - 액터의 중심점에 위치
  - 다른 자식 계층 컴포넌트 위치의 중심
    - 따라서 루트 컴포넌트는 위치 지정 및 회전 지정이 불가
- Arrow 컴포넌트
  - 화살표를 그려서 액터의 방향을 쉽게 파악하도록 돕는 컴포넌트
  - 에디터에서만 그려진다.





## Words

- prop
  - 소도구
- convex
  - 볼록면의, 볼록한, 볼록면
- pillar
  - 기둥
- hull
  - 겉껍질을 벗기다
  - 겉껍질
  - 덮개
- hull shader
  - 모델의 표면을 삼각형으로 변환
- bonfire
  - 모닥불, 화톳불, 횟불
- IRC(Internet Relay Chat)
  - 실시간 채팅 프로토콜로, 여러 사용자가 대화를 나눌 수 있다.
  - 개인 간의 대화도 가능
  - 'DCC'라는 파일 전송 기능도 제공
- fix up
  - 수리, 개량
- atmosphere
  - 대기, 분위기, 기압
- persistent
  - 지속하는, 끊임없는
- swarm
  - 무리, 떼, 군중
- PoC(Proof of Concept)
  - 컨셉 증명
  - 아이디어를 실체로 만들고, 아이디어가 괜찮은지 따져보는 것
- pawn
  - 저당물, 담보
  - 남에게 이용되는 사람, 남의 앞잡이, (빙의)
    - 언리얼 엔진에선 이 뜻으로 쓰인듯.
  - 사람 또는 AI가 조작하는 것
- marquee
  - 차양, 대형 천막
  - 원하는 영역 선택 툴
- strafing
  - 맹공격하다, 기총 소사, 맹공격
  - 정면을 바라보고 왼쪽, 오른쪽으로 이동
  - 한 지점을 조준한 상태로 이동
- spine
  - 척추
- ankle
  - 발목, 복사뼈
- toe
  - 발가락
- emitter
  -  방사체, 발포자, 발행인





## 읽어 볼 것

- [FBX 스켈레탈 메시 파이프라인 | Unreal Engine](https://docs.unrealengine.com/latest/KOR/Engine/Content/FBX/SkeletalMeshes/)





## 참고

- 실전 게임 제작으로 배우는 언리얼 엔진4
- 