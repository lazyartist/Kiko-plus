---
layout: post
title: "Math - Linear Transformation"
description: ""
date: 2019-03-22 19:00:00+09:00
tags: [game, math, math]
comments: true
share: true
---

#### 



#### 선형 변환의 벡터

선형 변환에 쓰이는 벡터는 x, y, z에 w가 추가된 4개의 성분은 갖는 벡터를 사용한다.

$$
\begin{pmatrix} 
x \\ y \\ z \\ w 
\end{pmatrix}
$$


좌표로 쓰이는 벡터

평행이동을 위해 w성분이 1이다.

$$
\begin{pmatrix} 
x \\ y \\ z \\ 1 
\end{pmatrix}
$$


벡터로 쓰이는 벡터

평행이동을 하지 않기(무의미 하기) 때문에 w성분이 0이다.

$$
\begin{pmatrix} 
x \\ y \\ z \\ 0 
\end{pmatrix}
$$

#### 좌표와 벡터

|      | 크기 변환 | 회전 변환 | 평행 이동 |
| :--: | :-------: | :-------: | :-------: |
| 좌표 |     ○     |     ○     |     ○     |
| 벡터 |     ○     |     ○     |     ×     |

벡터는 실체(위치)가 없기 때문에 위치를 이동시키는 평행이동은 무의미하다.



#### 크기변환(Scaling) 행렬

$$
\begin{pmatrix}
S_x & 0 & 0 & 0 \\ 
0 & S_y & 0 & 0 \\ 
0 & 0 & S_z & 0 \\ 
0 & 0 & 0 & 1 
\end{pmatrix}
\times
\begin
{pmatrix} 
x \\ y \\ z \\ w 
\end{pmatrix}
=
\begin{pmatrix} 
S_xx \\ S_yy \\ S_zz \\ w 
\end{pmatrix}
$$



#### 회전 변환(Rotation)

$$
x축 회전 변환 \\
\begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & \cos\theta_x & -\sin\theta_x & 0 \\ 0 & \sin\theta_x & \cos\theta_x & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix}
\times
\begin
{pmatrix} x \\ y \\ z \\ w \end{pmatrix}
=
\begin{pmatrix} x \\ \cos\theta_xy -\sin\theta_xz \\ \sin\theta_xy + \cos\theta_xz \\ w \end{pmatrix}
$$



$$
y축 회전 변환 \\
\begin{pmatrix}
\cos\theta_y & 0 & \sin\theta_y & 0 \\
0 & 1 & 0 & 0 \\
-\sin\theta_y & 0 & \cos\theta_y & 0 \\
0 & 0 & 0 & 1 
\end{pmatrix}
\times
\begin
{pmatrix} x \\ y \\ z \\ w \end{pmatrix}
=
\begin{pmatrix}
\cos\theta_yx +\sin\theta_yz \\
y \\ 
-\sin\theta_yx +\cos\theta_yz\\
w 
\end{pmatrix}
$$



$$
z축 회전 변환 \\
\begin{pmatrix}
\cos\theta_z & -\sin\theta_z & 0 & 0 \\
\sin\theta_z & \cos\theta_z & 0 & 0 \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1 
\end{pmatrix}
\times
\begin
{pmatrix} x \\ y \\ z \\ w \end{pmatrix}
=
\begin{pmatrix}
\cos\theta_zx -\sin\theta_zy \\
\sin\theta_zx +\cos\theta_zy\\
z \\ 
w 
\end{pmatrix}
$$



#### 평행 이동

$$
\begin{pmatrix}
1 & 0 & 0 & T_x \\ 
0 & 1 & 0 & T_y \\ 
0 & 0 & 1 & T_z \\ 
0 & 0 & 0 & 1 
\end{pmatrix}
\times
\begin
{pmatrix} 
x \\ y \\ z \\ w 
\end{pmatrix}
=
\begin{pmatrix} 
x+T_x \\ y+T_y \\ z+T_z \\ w 
\end{pmatrix}
$$



#### 행렬의 합성

여러 행렬을 한번에 곱해서 결과를 내야하는 경우 값이 고정된 행렬들을 미리 계산하여 하나의 행렬로 만들어 계산 횟수를 줄일 수 있다.

단, 행렬곱은 교환법칙이 성립하지 않으므로 순서를 변경하면 안된다.

$$
\begin{matrix}
V_{result} &=& M_t \times M_r \times M_s \times V \\
&=& M_{trs} \times V
\end{matrix} \\
\text{(일반적으로 크기 -> 회전 -> 이동 순으로 행렬을 적용한다.)}
$$


#### 좌표계 변환

###### 로컬 좌표계

오브젝트에 붙어 있는 좌표계.



###### 월드 좌표계

오브젝트가 놓여질 공간의 좌표계



###### 뷰 좌표계

카메라가 원점인 좌표계

카메라를 월드에 배치하는 행렬의 역행렬은 카메라를 원점에 배치하는 행렬이된다. 

따라서 뷰 좌표계 변환 행렬은 카메라를 월드에 배치하는 행렬의 역행렬이다.



투영 좌표계

카메라에서 바라본 3D 오브젝트를 투영행렬을 이용하여 2D 스크린에 투영한 좌표계

- 투시투영(Perspective)
  - 원근감 적용
  - 4행이 (0, 0, 0, 1)이 아니라 (0, 0, 1, 0) 이다.
  - M_p를 곱한 후 w 성분으로 x, y, z를 나눈다.
- 정사투영(Orthographic)
  - 원근감 미적용



###### 좌표계 변환 행렬 처리

로컬 -> 월드 -> 뷰 -> 투영 행렬을 하나로 합쳐서 처리한다.

$$
M_{wvp} = M_p \times M_v \times M_w \\
\grave{P} = M_{wvp} \times P \leftarrow \text{w성분으로 나눈다}
$$

위의 공식은 오브젝트 하나에 대한 변환 행렬이다.

따라서 각각의 오브젝트 마다 변환 행렬을 하나씩 만들어 줘야하는데 M_vp는 모든 오브젝트가 같기 때문에 물체마다 M_w를 계한하고 미리 계산한 M_vp와 계산하면 된다.



#### 쿼터니온(사원수 - Quaternion)

회전만 필요한 곳의 정보는 쿼터니언으로 표시한다.

짐벌락을 피할 수 있다.

4개의 수로 회전을 표현한다.(변환 행렬의 1/4)

$$
쿼터니언의 표현 방식 \\
스칼라 :s, 허수 : i, j, k \\
q = (s; u, v, w) = s + ui + vj + wk
$$
