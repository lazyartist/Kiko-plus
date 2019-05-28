---
layout: post
title: "Unity - Shader"
description: ""
date: 2019-04-22 19:00:00+09:00
tags: [unity, Shader]
comments: true
share: true
---

[TOC]



## 쉐이더 자료형

- float : 32bit
- half : 16bit
- fixed : 11bit



## 쉐이더 Properties

- float
  - Range(min, max)
  - float
  - int
- float4
  - 멤버변수 : rgba == xyzw
  - Color : 컬러픽커를 통해 입력
  - Vector : float4를 직접 숫자로 입력
- sampler
  - 2D : 2D 텍스쳐를 받는 인터페이스
  - Rect
  - Cube
  - 3D



## 명령어

- fullforwardshadows
  - Forward Rendering 상태일 때 모든 라이트에게서 그림자를 생성
  - 이 구문을 삭제하면 가장 가벼운 라이트인 디렉셔널(Directional) 라이트의 그림자를 생성하고 다른 라이트의 그림자는 무시한다.



## 함수

- lerp
  - Linear Interpolation(선형보간)
  - 두 값을 선형적으로 놓고 0~1에 해당하는 값을 반환



## UV

- 0, 0 좌표
  - 언리얼, DirectX : 좌상단
  - 유니티, OpenGL :  좌하단



## 텍스쳐 옵션

- Repeat
  - UV를 벗어나는 영역에서도 텍스쳐가 계속 반복
- Clamp
  - 마지막 픽셀의 색이 연속되어 늘어나 보임



## 유니티에 내장된 시간 변수

- _Time
  - float4
  - t : 원래 시간
  - (x, y, z, w) == (t/20, t, t×2, t×3)
- _SinTime
  - float4
  - Sin 그래프의 시간
  - (t/8, t/4, t/2, t)
    - x의 경우 Sin 함수에 넣는 시간값을 1/8 했기 때문에 시간이 천천히 흐르는 효과가 있다.
- _CosTime
- unity_DeltaTime
  - 프레임의 시간차
  - (dt, 1/dt, smoothDt, 1/smoothDt)



## #pragma

- Standard
  - 물리 기반 라이팅



## 버텍스 정보

- 위치(Position)
- UV(Texcoord)
- 컬러(Color)
- 노멀(Normal)
- 탄젠트(Tangent)



## 물리 기반 쉐이더

주변 환경에 따른 재질 변화를 물리 법칙에 기반하여 실시간으로 재질을 구현해주는 사실적인 쉐이더 표현 기법

- Metallic
  - 재질이 금속인지를 결정
  - 0이면 스페큘러 컬러가 흑백, 1이면 Albedo에 넣은 색
- Smoothness
  - 재질이 매끄러운지를 결정
  - 0이면 완전 거칠어 난반사만 일어나고, 1이면 완벽히 매끄러워서 정반사만 일어남
- Occlusion
  - Occlusion은 float을 받는 변수이므로 _OcclusionTex의 r채널만 사용하고 나머지 값은 버려진다.
  - 따라서 _MainTex의 알파값등을 사용하지 않는다면 이곳에 Occlusion 값을 넣어 사용해도 된다.



Matallic Value Chart [<https://docs.unity3d.com/Manual/StandardShaderMaterialCharts.html>]



## 노멀맵

#### 노멀맵 저장 방법

노멀벡터의 x, y, z 값을 저장할 때 z값은 x, y 값으로 계산해낼 수 있으므로 x, y 값만 저장한다.

저장 포맷은 DXTnm(DXT5nm)이라는 방식을 사용하는데 이 포맷은 DXT와 같지만 R, G를 A, G에 저장하도록해서 가장 넓은 대역폭을 가진 A와 G를 활용하는 포맷이다.

DXT는 다음과 같이 배분되어 있다.

R:G:B:A = 5:6:5:8



#### UnpackNormal  함수

``` c
 inline fixed3 UnpackNormal(fixed4 packednormal)
 {
 #if defined(SHADER_API_GLES) && defined(SHADER_API_MOBILE)
     return packednormal.xyz * 2 - 1;
 #else
     fixed3 normal;
     normal.xy = packednormal.wy * 2 - 1;
     normal.z = sqrt(1 - normal.x*normal.x - normal.y * normal.y);
     return normal;
 #endif
 }
```

###### x, y 값에 x2 - 1 해주는 이유

좌표값이 양수만 있을 경우 각도를 90도까지밖에 나타낼 수 없으므로 -1~1 사이의 값을 나타내기 위해 저장 시 1을 더하고 x0.5 해주기 때문



###### UnpackNormal  함수가  normal.z 구하는 원리

normal 벡터는 길이가 1인 벡터이므로 x, y 값을 알면 삼각함수를 이용하여 z값을 구할 수 있다.
$$
\begin{gather*}
1=\sqrt{x^{2} +y^{2} +z^{2}}\\
1=x^{2} +y^{2} +z^{2}\\
z^{2} =1-x^{2} -y^{2}\\
\therefore z=\sqrt{1-x^{2} -y^{2}}
\end{gather*}
$$



## 프레스넬 효과(Fresnel Effect)

- 지표각에서 반사가 더 강해지는 효과
- 이 반사는 구체의 가장자리 주변에만 나타남
- 머티리얼의 평활도가 증가할수록 반사가 더 잘보이고 선명
- 스탠다드 쉐이더에서는 프레스넬 효과가 직접 제어되지 않고 머티리얼의 평활도(Smoothness)를 통해 간접적으로 제어됨
  - 표면이 매끄러우면 프레스넬 효과가 강하게 나타남
  - 표면이 거칠면 프레스넬 효과가 나타나지 않음





## fixed Luminance (fixed3 c)

컬러를 휘도(그레이스케일)로 변환합니다.



## IBL RImLight

외곽라인이 빛나게 하는것



## 렌더링 파이프라인

- 로컬 변환
- 월드 변환
- 뷰 변환
- 후면 추려내기(back-face culling)
- 조명(Light)
  - 광원 벡터, 시선 벡터, 법선 벡터 등 조명 계산식을 이용해 정범의 색상을 계산
- 테셀레이션
  - GPU에서 정점을 증가, 감소
- 클리핑
  - 시야 절두체를 벗어나는 폴리곤 자르기
- 투영
- 뷰포트
  - 렌더 타겟(윈도우)의 화면 좌표로 변환
- 래스터라이즈
  - 폴리곤을 픽셀로 변환하고 컬러를 계산
- 픽셀 쉐이더
  - 텍스처 컬러와 (래스터라이즈된)정점 컬러를 사용하여 픽셀의 최종 색상 결정
- 렌더 백앤드
  - 비디오 메모리에 넣을지 결정
    - 알파 테스트(Alpha Test)
      - 알파값이 있으면 1, 없으면 0으로 판단하여 그릴지 안그릴지 판단. 연산 속도가 빠르다.
    - 스텐실 테스트(Stencil Test(buffer))
      - 그리지 말아야할 부분인지 체크
    - 깊이 테스트(Z buffer Test)
  - 비디오 메모리에 넣을 방법
    - 알파 블렌딩(Alpha Blending)
    - 안개(Fog)
    - 안티앨리어싱(Anti-aliasing)
- 출력



## Input 구조체

- float3 viewDir
  - 뷰 방향 표시
  - 시차 효과, Rim 라이팅
- float4 color:COLOR
  - 보간된 버텍스 컬러
- float4 screenPos
  - 스크린 스페이스 위치
- float3 worldPos
  - 월드 공간상의 위치
- float3 worldRefl
  - 서피스 쉐이더에 o.Normal이 작성되지 않은 경우, 월드 반사 벡터를 포함
- float3 worldNormal
  - 서피스 쉐이더에 o.Normal이 작성되지 않는 경우, 월드 노멀 벡터를 포함
- float3 worldRefl; INTERNAL_DATA
  - 서피스 쉐이더에 o.Normal을 작성했을 경우 월드 반사 벡터를 포함
  - 픽셀 당 노멀맵에 기초하여 반사 벡터를 얻으려면 WorldReflectionVector(IN, o.Normal)을 사용
- float3 worldNormal; INTERNAL_DATA
  - 서피스 쉐이더에 o.Normal을 작성했을 경우 월드 반사 벡터를 포함
  - 픽셀 당 노멀맵에 기초하며 노멀 벡트를 얻으려면 WorldNormalVector(IN, o.Normal)을 사용



## 버텍스 구조체

- appdata_base, appdata_tan, appdata_full
  - float4 vertex
    - 버텍스의 위치
  - float4 tangent
    - 접선 방향(NormalMap 연산시 사용)
  - float3 normal
    - 버텍스의 노멀
  - float4 texcoord
    - 첫 번째 UV 좌표
  - float4 texcoord1
    - 두 번째 UV 좌표
    - 라이트맵용 커스텀 UV 데이터를 사용할 때 많이 사용
  - float4 texcoord2
    - 세 번째 UV 좌표
  - float4 texcoord3
    - 네 번째 UV 좌표
  - float4 color
    - 버텍스 컬러



## 렌더링 방식

- PR
  - Photo Realistic
- NPR
  - Non Photo Realistic



## 탄젠트 좌표계

- 픽셀 자신이 중심축을 가진 듯한 좌표계
- NormalMap



## z buffer

- 필셀마다 카메라를 기준으로 가장 가까운 오브젝트의 깊이값이 저장되어 있는 데이터
- 1~0 사이의 숫자
- 이 값을 컬러로하여 그러놓은 그림



## Z Fighting

같은 z값을 가진 픽셀이 매 프레임 먼저 그려지기위해 경합하며 깜빡이게 보이는 현상



## 알파의 원리

- 불투명(opaque) 오브젝트는 먼저 그린다.
- 반투명(transparent) 오브젝트는 나중에 그린다.
- 반투명 오브젝트까리는 뒤어서부터 그린다.



## 알파가 느린 이유

- 반투명 오브젝트는 불투명 오브젝트가 다 그려질 때까지 대기해야한다.
- 반투명 오브젝트끼리 거리를 체크하는 연산을 추가해야한다.
- 가려진 오브젝트도 반투명에 의해 그려져야한다.
- 디퍼드 렌더링으로 반투명을 처리할 수 없다. 포워드 렌더링 사용.



## 알파 블렌딩에서 알파 소팅의 문제

- 오브젝트의 피봇점을 기준으로 카메라로부터의 거리를 계산하는데 이 때 의도와 다르게 피봇점이 카메라와 가까운 객체를 먼저 그리게 된다.
- 이는 어쩔 수 없는 현상으로 이를 zwrite를 off하는 방법이 있다.
  - 이는 문제를 해결하는 것이 아니라 시각적으로 허용할 정도의 범위에서 마무리하는 것이다.



## 알파 테스트

- 지정하는 값과 알파 픽셀의 색상 값을 비교해서 더 낮은 픽셀은 그리지 않고 더 높은 픽셀은 그린다.
- 픽셀을 그리거나 그리지 않기 때문에 반투명한 픽셀은 없어진다.
- 반투명이 없으니 외곽이 거칠게 표현된다.
- 장점
  - 그림자가 나온다.
  - 알파 소팅의 문제가 없다.
  - PC에서는 알파블렌딩보다 빠르다.
  - 


