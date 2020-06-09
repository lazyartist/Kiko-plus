---
layout: post
title: "Math - Matrix"
description: ""
date: 2019-03-22 19:00:00+09:00
tags: [math]
comments: true
share: true
---


[TOC]



## 행렬의 덧셈과 뺄셈

- 결합법칙, 교환법칙 성립

$$
A+B=B+A\\
A-B=B-A\\
(A+B)+C=A+(B+C)\\
A+(-A)=(-A)+A=O
$$

## 행렬의 곱셈

- 결합법칙 성립
- 교환법칙 성립하지 않음
- 분해법칙 성립

$$
(AB)C=A(BC)\\
AB \ne BA\\
A(B+C)=AB+AC, (A+B)C=AC+BC\\
k(AB)=(kA)B=A(kB)(단\ k는\ 실수값)\\
AB=O, A=O\ or\ B=O
$$

## 영행렬

- 행렬의 모든 요소가 0인 행렬

$$
O=\begin{bmatrix}
0 & 0\\
0 & 0
\end{bmatrix}
$$



## 단위행렬

- 단위행렬은 대각 원소들은 1이고 나머지는 0인 행렬
- 다른 행렬에 곱했을 때 그 행렬이 그대로 나온다.
- 항등행렬

$$
E=\begin{pmatrix} 1 & 0 \\ 0 & 1 \end{pmatrix} or
\begin{pmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & 1 \end{pmatrix} or
\begin{pmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix}
or \cdots
$$



## 역수

- 어떠한 수에 곱했을 때 그 수를 1로 만드는 수


$$
a \times a^{-1}(역수) = 1 \\
a^{-1}(역수) \times a = 1
$$


## 역행렬

- 어떠한 행렬에 곱했을 때 단위 행렬로 만드는 수

### 역행렬의 성질

$$
\begin{gather*}
\left( A^{-1}\right)^{-1} =A\\
( AB)^{-1} =B^{-1} A^{-1}\\
\left( A^{-1}\right)^{n} =\left( A^{n}\right)^{-1}\\
( kA)^{-1} =\frac{1}{k} A^{-1}\\
AX=B\Longrightarrow A^{-1} AX=A^{-1} B\Longrightarrow EX=A^{-1} B\Longrightarrow X=A^{-1} B\\
XA=B\Longrightarrow XAA^{-1} =BA^{-1} \Longrightarrow XE=BA^{-1} \Longrightarrow X=BA^{-1}\\
( AB)\left( B^{-1} A^{-1}\right) =A\left( BB^{-1}\right) A^{-1} =AEA^{-1} =AA^{-1} =E
\end{gather*}
$$



### 역행렬 공식

$$
E = M \times M^{-1} \\
E = M^{-1} \times M \\
\text{역행렬은 곱셈의 교환법칙이 성립한다.}
$$


$$
\text{2x2 행렬의 역행렬 공식} \\
A = \begin{bmatrix}
a & b \\
c & d
\end{bmatrix} \\

A^{-1} = \begin{vmatrix}
a & b \\
c & d
\end{vmatrix}^{-1}
= \frac{1}{\lvert A \rvert} \begin{bmatrix}
d & -b \\
-c & a
\end{bmatrix}
= \frac{1}{ad - bc} \begin{bmatrix}
d & -b \\
-c & a
\end{bmatrix} \\
$$



### 역행렬의 판별식

- 역행렬이 존재하는지 판별하는 식
- 행렬식의 값으로 역행력의 존재 유무를 판단한다.

$$
\begin{gather*}
A=\begin{bmatrix}
a & b\\
c & d
\end{bmatrix}\\
ad-bc\neq 0\Longrightarrow 역행렬\ 존재\\
ad-bc=0\Longrightarrow 역행렬\ 존재하지\ 않음
\end{gather*}
$$



### 변환행렬과 역행렬

- 회전행렬은 반드시 역행렬이 존재한다.
- 크기, 회전, 위치 변환 행렬에 역행렬을 곱하면 변환을 되돌리는 효과가 있다.



## 전치행렬(Transposed Matrix)

### 전치행렬이란?

- 대각 원소를 기준으로 대칭 원소를 교환한 행렬


$$
\begin{equation*}
M\begin{bmatrix}
1 & 2 & 3\\
4 & 5 & 6\\
7 & 8 & 9
\end{bmatrix} \ \Longrightarrow M^{t}\begin{bmatrix}
1 & 4 & 7\\
2 & 5 & 8\\
3 & 6 & 9
\end{bmatrix}
\end{equation*}
$$

### 전치행렬의 특징

$$
\begin{gather*}
\left( A^{T}\right)^{T} =A\\
( A+B)^{T} =A^{T} +B^{T}\\
( AB)^{T} =B^{T} A^{T}\\
( kA)^{T} =kA^{T}( 단\ k는\ 스칼라)
\end{gather*}
$$



### 회전행렬과 전치행렬

- 회전행렬의 전치행렬은 회전행렬의 역행렬과 같다.

$$
M_r \times M_r^t = M_r^t \times M_r = E \\
\therefore M_r^t = M_r^{-1}
$$


#### 전치행렬을 쓰는 이유

- 역행렬 계산은 비용이 크지만 전치행렬은 값을 바꾸기만 하면 되므로 비용이 작다.
- 따라서 회전행렬만 있을 때는 역행렬 계산을 하지 않고 전치행렬을 만들어 처리할 수 있다.




## 행렬식(Determinant)

$$
A = (a_{ij}) = \begin{pmatrix}
0 & \cdots & 0 \\
\vdots & \ddots & \vdots \\
0 & \cdots & 0
\end{pmatrix} \\

\text{A 행렬에 대한 행렬식의 표현} \\
\lvert A \rvert = 
\lvert a_{ij} \rvert = 
\det A = \det(a_{ij}) = 
\det \begin{pmatrix}
0 & \cdots & 0 \\
\vdots & \ddots & \vdots \\
0 & \cdots & 0
\end{pmatrix} = 
\begin{vmatrix}
0 & \cdots & 0 \\
\vdots & \ddots & \vdots \\
0 & \cdots & 0
\end{vmatrix} \\
$$



$$
\text{1x1 행렬의 행렬식} \\
\det(a) = a \\
$$



$$
\text{2x2 행렬의 행렬식} \\
\det \begin{pmatrix}
a & b \\
c & d
\end{pmatrix} = ab - bc \\
$$



$$
\text{3x3 행렬의 행렬식} \\
\begin{matrix}
\det \begin{pmatrix}
a & b & c \\
d & e & f \\
g & h & i
\end{pmatrix} &=& aei + bfg + cdh - ceg - bdi - afh \\
&=& a \det \begin{pmatrix}
e & f\\
h & i
\end{pmatrix}
- b \det \begin{pmatrix}
d & f\\
g & i
\end{pmatrix}
- c \det \begin{pmatrix}
d & e\\
g & h
\end{pmatrix}\\
\end{matrix}
$$





## 3x4 행렬

- 크기, 회전, 이동 행렬의 4x4 행렬의 4행은 언제나 (0, 0, 0, 1)이기 때문에 메모리 절약과 처리속도 상승을 위해 4행을 제거하고 4행은 (0, 0, 0, 1)이라고 가정한다.



## 벡터와 행렬곱의 의미

- 벡터를 새로운 좌표로 변환시키는 역할
- 벡터를 선형변환시킨다.

