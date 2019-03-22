---
layout: post
title: "Math - Matrix"
description: ""
date: 2019-03-22 19:00:00+09:00
tags: [game, math, math]
comments: true
share: true
---





#### 단위행렬

단위행렬은 대각 원소들은 1이고 나머지는 0인 행렬로 보통 E로 나타내고 A행렬에 곱했을 때 A가 그대로 나온다.

$$
\begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix} or
\begin{pmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{pmatrix} or
\begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix}
or \cdots
$$


#### 행렬의 곱

행렬의 곱은 교환법칙이 성립하지 않는다.



#### 역수

어떠한 수에 곱했을 때 그 수를 1로 만드는 수

$$
a \times a^{-1}(역수) = 1 \\
a^{-1}(역수) \times a = 1
$$


#### 역행렬

어떠한 행렬에 곱했을 때 단위 행렬로 만드는 수

역행렬 구하는 법은 복잡하므로 생략

$$
E = M \times M^{-1} \\
E = M^{-1} \times M \\
\text{역행렬은 곱셈의 교환법칙이 성립한다.}
$$

#### 역행렬의 의의

크기, 회전, 위치 변환 행렬에 역행렬을 곱하면 변환을 되돌리는 효과가 있다.



#### 전치행렬

대각 원소를 기준으로 대칭 원소를 교환한 행렬

$$
M의 전치행렬 \Rightarrow M^t
$$

#### 전치행렬의 특징

회전행렬의 전치행렬은 회전행렬의 역행렬과 같다.

$$
M_r \times M_r^t = M_r^t \times M_r = E \\
\therefore M_r^t = M_r^{-1}
$$


#### 전치행렬을 쓰는 이유

역행렬 계산은 비용이 크지만 전치행렬은 값을 바꾸기만 하면 되므로 비용이 작다.

따라서 회전행렬만 있을 때는 역행렬 계산을 하지 않고 전치행렬을 만들어 처리할 수 있다.



#### 3x4 행렬

크기, 회전, 이동 행렬의 4x4 행렬의 4행은 언제나 (0, 0, 0, 1)이기 때문에 메모리 절약과 처리속도 상승을 위해 4행을 제거하고 4행은 (0, 0, 0, 1)이라고 가정한다.


