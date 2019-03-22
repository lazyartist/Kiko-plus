---
layout: post
title: "Math - Vector(Cross Product)"
description: ""
date: 2019-03-20 19:00:00+09:00
tags: [game, math, math]
comments: true
share: true
---

#### 외적(Cross Product)
하나의 점에서 만나는 두 벡터 각각과 수직인 벡터

외적은 두 벡터가 만드는 평행사변형의 면적과 크기가 같은 벡터이다.



#### 외적 구하기

하나의 선 위에 있지 않은 평면 위의 세 점(평면 위의 벡터2개)으로 외적을 구할 수 있다.

하나의 선 위에 있다면 영벡터가 나온다.

$$
\begin{matrix}
A \times B &=& (a_yb_z - a_zb_y, a_zb_x - a_xb_z, a_xb_y - a_yb_x)
\end{matrix}
$$



#### 외적의 교환법칙

외적의 결과는 벡터인데 외적 연산의 순서가 바뀌면 벡터의 방향이 반대가 된다.

$$
\begin{matrix}
A \times B &=& (a_yb_z - a_zb_y, a_zb_x - a_xb_z, a_xb_y - a_yb_x) \\
B \times A &=& (b_ya_z - b_za_y, b_za_x - b_xa_z, b_xa_y - b_ya_x) \\
&& a_yb_z - a_zb_y \neq b_ya_z - b_za_y \\
&& \therefore A \times B \ne A \times B \\\\

&& a_yb_z - a_zb_y = b_ya_z - b_za_y \times -1 = b_za_y - b_ya_z  \\
&& \therefore A \times B = -(B \times A)

\end{matrix}
$$


#### 외적 벡터의 방향

좌표계에 따라 달라진다.

- 왼손 좌표계 : 두 벡터가 만나는 점을 축으로 왼손으로 감싸쥐는 방향(시계방향)에서 엄지 방향
- 오른손 좌표계 : 두 벡터가 만나는 점을 축으로 오른손으로 감싸쥐는 방향(시계방향)에서 엄지 방향



#### 외적 벡터의 길이

외적 벡터를 만드는 두 벡터의 길이는 외적 벡터의 방향에 영향을 주지 않는다.

또한 계산 과정에서 정규화된 외적 벡터를 얻을 수 없으므로 외적 벡터를 얻은 후에 정규화 시켜줘야한다.



