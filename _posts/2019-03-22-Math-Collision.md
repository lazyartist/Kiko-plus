---
layout: post
title: "Math - Collision"
description: ""
date: 2019-03-22 19:00:00+09:00
tags: [game, math, math]
comments: true
share: true
---

## 충돌 판정에 사용하는 형태

|        형태         | 특징                                                         | 구조체                                                       |
| :-----------------: | ------------------------------------------------------------ | ------------------------------------------------------------ |
|        선분         | - 좌표 2개를 이은 선<br />- 굵기가 없는 선 형태              | 시작점, 벡터                                                 |
|         구          | - 중심에서 같은 거리에 있는 면으로 만든 형태<br />- 중심과 반지름으로 표현 | 중심좌표, 반지름                                             |
| 평면<br /> (삼각형) | - 3차원 공간에 무한히 퍼져 있는 평평한 면<br />- 평면 방정식으로 표현<br />- 삼각형일 때는 평면을 범위로 제한 | - 평면의 성분<br />- 꼭짓점 3개, 삼각형을 포함하는 평면(계산 편의) |



## 직선과 직선의 충돌

#### 직선의 방정식 - 기울기와 y절편이 주어졌을 때

$$
a:기울기, b:y절편 \\
y = ax + b
$$

#### 직선의 방정식 - 기울기와 한 점의 좌표가 주어졌을 때

$$
a:기울기, P:한 점 \\
P_y = aP_x + b \\
P_y - aP_x = b \\
\therefore b = P_y - aP_x \\
\text{b를 대입} \\
y = ax + P_y - aP_x \\
\therefore y - P_y = a(x - p_x)
$$

#### 직선의 방정식 - 두 점이 주어졌을 때

$$
P:한 점, Q:두 점 \\
\text{'기울기와 한 점의 좌표' 공식에 대입} \\
y - P_y = \frac{Q_y - P_y}{Q_x - P_x}(x - p_x) \\
Q_y = P_y\text{라면 기울기가 0이되어 x축에 평행인 } y = P_y 직선이 되고 \\
Q_x = P_x\text{라면 기울기를 구할 수 없기 때문에 } x = P_x 직선이 된다. \\ 
\text{그 외는 위 식을 전개하면 된다.}
$$

#### 직선의 충돌(교점)

직선이 충돌한다는 것은 교점이 있다는 것

두 직선의 방정식을 연립하여 해를 구하면 된다.

​	해가 없다. -> 교점이 없다. 충돌(교차)하지 않는다.

​	해가 무수히 많다. -> 두 직선이 겹친다. 기울기와 y절편이 같다. 충돌(교차)하지 않는다.

​	해가 하나이다. -> 교점이 있다. 충돌(교차)한다.

$$
P:시작점, a:기울기 \\
y = a_1(x-p_{1x})+p_{1y} \\
y = a_2(x-p_{2x})+p_{2y} \\
$$


$$
\text{y에 대입}\\\\
a_1(x-p_{1x})+p_{1y} = a_2(x-p_{2x})+p_{2y} \\
a_1x-a_1p_{1x}+p_{1y} = a_2x-a_2p_{2x}+p_{2y} \\
a_1x-a_2x = -a_2p_{2x}+p_{2y}+a_1p_{1x}-p_{1y} \\
\therefore x = \frac{-a_2p_{2x}+p_{2y}+a_1p_{1x}-p_{1y}}{a_1-a_2} \\
$$


$$
\require{cancel}
\text{x에 대입}\\\\
y = a_1x-a_1p_{1x}+p_{1y}\\
y = a_1(\frac{-a_2p_{2x}+p_{2y}+a_1p_{1x}-p_{1y}}{a_1-a_2})-a_1p_{1x}+p_{1y} \\
y = \frac{-a_1a_2p_{2x}+a_1p_{2y}+a_1^2p_{1x}-a_1p_{1y}}{a_1-a_2}-a_1p_{1x}+p_{1y} \\
y = \frac{-a_1a_2p_{2x}+a_1p_{2y}+a_1^2p_{1x}-a_1p_{1y}}{a_1-a_2} - 
\frac{a_1^2p_{1x}-a_1a_2p_{1x}}{a_1-a_2} +
\frac{a_1p_{1y}-a_2p_{1y}}{a_1-a_2} \\
y = \frac{-a_1a_2p_{2x}+a_1p_{2y}+\cancel{a_1^2p_{1x}}-\cancel{a_1p_{1y}} - \cancel{a_1^2p_{1x}} + a_1a_2p_{1x} + \cancel{a_1p_{1y}}-a_2p_{1y}}{a_1-a_2} \\
\therefore y = \frac{-a_1a_2p_{2x}+a_1p_{2y} + a_1a_2p_{1x} - a_2p_{1y}}{a_1-a_2}
$$



> 유니티 구현 코드

```C#
private void OnDrawGizmos()
{
    /*
        이 방법으로는 수직인 직선과의 교점을 찾을 수 없다.
    */

    // 직선의 방정식 : y = ax + b, y = cx + d
    // x` = (d - b) / (a - c)
    // y` = ax` + b
    float a = (LineEnd1.position.y - LineStart1.position.y) / (LineEnd1.position.x - LineStart1.position.x);
    float c = (LineEnd2.position.y - LineStart2.position.y) / (LineEnd2.position.x - LineStart2.position.x);
    float b = LineEnd1.position.y - a * LineEnd1.position.x;
    float d = LineEnd2.position.y - c * LineEnd2.position.x;

    if(a == c && b == d)
    {
        Debug.Log("Overlap");
        return;
    } else if (a == c)
    {
        Debug.Log("Parallel");
        return;
    } else
    {
        Debug.Log("Collision");
    }

    float x = (d - b) / (a - c);
    float y = a * x + b;

    Gizmos.color = Color.red;
    Gizmos.DrawLine(LineStart1.position, LineEnd1.position);
    Gizmos.color = Color.blue;
    Gizmos.DrawLine(LineStart2.position, LineEnd2.position);
    Gizmos.color = Color.yellow;
    Gizmos.DrawWireSphere(new Vector3(x, y, 0), 1);

    Debug.Log(x + ", " + y);
}
```



#### 선분의 충돌(교점)

직선의 교점이 두 선분의 영역안에 있는지 확인한다.

x축 방향 벡터가 0이면 기울기 계산 시 0으로 나누게 되므로 다른 처리가 필요하다.

- 기울기가 같다 : 평행
- 기울기가 같고 y절편이 다르다 : 평행
- 기울기가 같고 y절편이 같다 : 겹침



## 선분과 선분의 충돌

#### 선분을 나타내는 방법

직선의 방정식으로 수직인 직선을 표현할 수 없으므로 매개변수 t를 사용하여 x와 y에 대한 방정식 2개로 선분을 표현한다.

$$
\text{서로 다른 두 점 P1, P2로 이루어진 벡터 위의 한 점} \\
x = P1_x + (P2_x - P1_x)t \\
y = P1_y + (P2_y - P1_y)t
$$



#### 선분의 교점을 구하는 방정식 

[참고]: http://www.cs.swan.ac.uk/~cssimon/line_intersection.html	" "
$$
벡터 : P1 \to P2, Q1 \to Q2 \\
P(t) = P1 + (P2-P1)t \\
Q(s) = Q1 + (Q2-Q1)s \\
\text{교점이 있다는 것은 두 함수의 값이 같다는 것} \\
P(t) = Q(s) \\
\text{x 성분으로 전개} \\
P1_x + (P2_x - P1_x)t = Q1_x + (Q2_x - Q1_x)s \\
P1_x - Q1_x = (Q2_x - Q1_x)s - (P2_x - P1_x)t \\
\text{y 성분으로 전개} \\
P1_y + (P2_y - P1_y)t = Q1_y + (Q2_y - Q1_y)s \\
P1_y - Q1_y = (Q2_y - Q1_y)s - (P2_y - P1_y)t \\
$$



$$
\text{위 식에서 t, s를 구하기 위해 행렬을 이용} \\
\begin{bmatrix}
(Q2_x - Q1_x) & -(P2_x - P1_x) \\
(Q2_y - Q1_y) & -(P2_y - P1_y)
\end{bmatrix}
\begin{bmatrix}
s \\
t
\end{bmatrix}
= 
\begin{bmatrix}
P1_x - Q1_x \\
P1_y - Q1_y
\end{bmatrix} \\\\

\text{위 식을 } AX = B\text{ 형태로 봤을 때}\\
\text{좌변에 X만 남기기 위해서는 좌, 우변에 } A^{-1}\text{(역행렬)을 곱해야함} \\
X = BA^{-1} \\

\begin{matrix}

    \begin{bmatrix}
    s \\
    t
    \end{bmatrix}
    
    &=& 
    \frac{1}
    {\begin{vmatrix}
    (Q2_x - Q1_x) & -(P2_x - P1_x) \\
    (Q2_y - Q1_y) & -(P2_y - P1_y)
    \end{vmatrix}} 
    \begin{bmatrix}
    -(P2_y - P1_y) & -(P2_x - P1_x) * -1 \\
    (Q2_y - Q1_y) * -1 & (Q2_x - Q1_x)
    \end{bmatrix}
    \begin{bmatrix}
    P1_x - Q1_x \\
    P1_y - Q1_y
    \end{bmatrix} 
    \\

    &=& \frac{1}
    {\begin{vmatrix}
    (Q2_x - Q1_x) & (P1_x - P2_x) \\
    (Q2_y - Q1_y) & (P1_y - P2_y)
    \end{vmatrix}} 
    \begin{bmatrix}
    (P1_y - P2_y) & (P2_x - P1_x) \\
    (Q1_y - Q2_y) & (Q2_x - Q1_x)
    \end{bmatrix}
    \begin{bmatrix}
    P1_x - Q1_x \\
    P1_y - Q1_y
    \end{bmatrix} \\
    
    &=& 
    \frac{1}{(Q2_x - Q1_x)(P1_y - P2_y) - (P1_x - P2_x)(Q2_y - Q1_y)}
    \begin{bmatrix}
    (P1_y - P2_y) & (P2_x - P1_x) \\
    (Q1_y - Q2_y) & (Q2_x - Q1_x)
    \end{bmatrix} 
    \begin{bmatrix}
    P1_x - Q1_x \\
    P1_y - Q1_y
    \end{bmatrix} \\
    
    &=& 
    \begin{bmatrix}
    \frac{(P1_y - P2_y)}{(Q2_x - Q1_x)(P1_y - P2_y) - (P1_x - P2_x)(Q2_y - Q1_y)} & \frac{(P2_x - P1_x)}{(Q2_x - Q1_x)(P1_y - P2_y) - (P1_x - P2_x)(Q2_y - Q1_y)} \\
    \frac{(Q1_y - Q2_y)}{(Q2_x - Q1_x)(P1_y - P2_y) - (P1_x - P2_x)(Q2_y - Q1_y)} & \frac{(Q2_x - Q1_x)}{(Q2_x - Q1_x)(P1_y - P2_y) - (P1_x - P2_x)(Q2_y - Q1_y)}
    \end{bmatrix} 
    \begin{bmatrix}
    P1_x - Q1_x \\
    P1_y - Q1_y
    \end{bmatrix} \\
\end{matrix}
$$



$$
\begin{matrix}
\therefore t &=& \frac{(Q1_y - Q2_y)(P1_x - Q1_x)}{(Q2_x - Q1_x)(P1_y - P2_y) - (P1_x - P2_x)(Q2_y - Q1_y)} + \frac{(Q2_x - Q1_x)(P1_y - Q1_y)}{(Q2_x - Q1_x)(P1_y - P2_y) - (P1_x - P2_x)(Q2_y - Q1_y)} \\
&=& \frac{(Q1_y - Q2_y)(P1_x - Q1_x) + (Q2_x - Q1_x)(P1_y - Q1_y)}{(Q2_x - Q1_x)(P1_y - P2_y) - (P1_x - P2_x)(Q2_y - Q1_y)} \\

\therefore s &=& \frac{(P1_y - P2_y)(P1_x - Q1_x)}{(Q2_x - Q1_x)(P1_y - P2_y) - (P1_x - P2_x)(Q2_y - Q1_y)} + \frac{(P2_x - P1_x)(P1_y - Q1_y)}{(Q2_x - Q1_x)(P1_y - P2_y) - (P1_x - P2_x)(Q2_y - Q1_y)} \\
&=& \frac{(P1_y - P2_y)(P1_x - Q1_x) + (P2_x - P1_x)(P1_y - Q1_y)}{(Q2_x - Q1_x)(P1_y - P2_y) - (P1_x - P2_x)(Q2_y - Q1_y)} \\
\end{matrix} \\
$$

 

> 유니티 구현 코드

```C#
private void OnDrawGizmos()
{
    Gizmos.color = Color.red;
    Gizmos.DrawLine(P1.position, P2.position);
    Gizmos.color = Color.blue;
    Gizmos.DrawLine(Q1.position, Q2.position);

    Vector3 p1 = P1.position;
    Vector3 p2 = P2.position;
    Vector3 q1 = Q1.position;
    Vector3 q2 = Q2.position;

    Vector3 v = P2.position - P1.position;
    Vector3 w = Q2.position - Q1.position;

    float denominator = (q2.x - q1.x) * (p1.y - p2.y) - (p1.x - p2.x) * (q2.y - q1.y);

    if(denominator == 0)
    {
        Debug.Log("Overlap");
        return;
    }

    // t : P1->P2에서 교점의 비율, s : Q1->Q2에서 교점의 비율
    float t = ((q1.y - q2.y) * (p1.x - q1.x) + (q2.x - q1.x) * (p1.y - q1.y)) / denominator;
    float s = ((p1.y - p2.y) * (p1.x - q1.x) + (p2.x - p1.x) * (p1.y - q1.y)) / denominator;

    float x = v.x * t + p1.x;
    float y = v.y * t + p1.y;

    Debug.Log(t + ", " + s + ", " + denominator);

    if (t < 0.0f || t > 1.0f || s < 0.0f || s > 1.0f)
    {
        Debug.Log("No Collision");
    }
    else if (t == 0 && s == 0)
    {
        Debug.Log("Parallel");
    }
    else
    {
        Gizmos.color = Color.yellow;
        Gizmos.DrawWireSphere(new Vector3(x, y, 0), 1);
    }
}
```



## 선분과 구의 충돌

#### t를 사용하여 선분 위의 점 표현하기

> t는 0.0 ~ 1.0 사이의 값
>
> 시작점 P
>
> 시작점에서의 벡터 V
>
> 선분위의 점 (x, y, z)

$$
x = P_x + V_xt \\
y = P_y + V_yt \\
z = P_z + V_zt \\
$$



#### 구의 방정식

> 중심 : (a, b, c)
> 반지름 : r
> 구면 위의 점 : (x, y, z)

$$
\text{구의 방정식 표준형} \\
(a-x)^2+(b-y)^2+(c-z)^2=r^2
$$



$$
\text{구의 방정식 일반형(표준형의 전개)} \\
x^2 + y^2 + z^2 - 2ax - 2by - 2cz + a^2 + b^2 + c^2 - r^2 = 0 \\
x^2 + y^2 + z^2 + Ax + By + Cz + D = 0 
$$



#### 이차 방정식의 근의 공식

$$
ax^2 + bx + c = 0 \\
x = \frac{-b \pm \sqrt{b^2-4ac} }{2a}
$$



###### 일차항에 상수 2가 곱해진 경우의 근의 공식

$$
ax^2 + 2bx + c = 0 \\
x = \frac{-b \pm \sqrt{b^2-ac} }{a}
$$

###### 근의 공식의 판별식(Discriminant)

$$
D = b^2 - 4ac
$$

| D     | 의미                         |
| ----- | ---------------------------- |
| D > 0 | 서로 다른 두 근              |
| D = 0 | 중근(완전 제곱식, 근이 하나) |
| D < 0 | 근이 없다                    |



#### 선분과 구의 충돌 검출

> (a, b, c) : 구의 중심
>
> r : 구의 반지름

$$
(a - x)^2 + (b - y)^2 + (c - z)^2 = r^2 \\
\text{구의 방정식에 직선의 (x, y, z)를 대입} \\
(a - P_x + V_xt)^2 + (b - P_y + V_yt)^2 + (c - P_z + V_zt)^2 = r^2 \\
\text{다음과 같이 치환} \\
k_x = a - P_x \\
k_y = b - P_y \\
k_z = c - P_z \\
(k_x + V_xt)^2 + (k_y + V_yt)^2 + (k_z + V_zt)^2 = r^2 \\
\text{전개} \\
k_x^2 + 2k_xV_xt + V_x^2t^2 + k_y^2 + 2k_yV_yt + V_y^2t^2 + k_z^2 + 2k_zV_zt + V_z^2t^2 = r^2 \\
(V_x^2 + V_y^2 + V_z^2)t^2 + 2(k_xV_x + k_yV_y + k_zV_z)t + k_x^2 + k_y^2 + k_z^2 - r^2 \\
\text{다음과 같이 나타낼 수 있다} \\
at^2 + bt + c = 0 \\
\text{근의 공식으로 t값을 구할 수 있다} \\
t = \frac{-b \pm \sqrt{b^2-4ac} }{2a} \\
\therefore \text{t값을 구한 뒤 '선분 위의 점 방정식'에 대입하여 x, y, z 값을 구하면 된다.}
$$



###### t값의 의의

| t값의 개수 | t값의 범위          | 의미                                                         |
| ---------- | ------------------- | ------------------------------------------------------------ |
| 0          | -                   | 충돌 X                                                       |
| 1          | 0~1 사이            | 한 점에서 선분 충돌 O                                        |
| 1          | 0~1 벗어남          | 선분 충돌 X, 직선 충돌 O                                     |
| 2          | t값 하나만 0~1 사이 | 한 점에서 선분 충돌 O, 원에 걸침                             |
| 2          | t값 둘 다 0~1 사이  | 두 점에서 선분 충돌 O, 원을 관통<br />t값이 작은 쪽이 시작점에 가깝다. |

실제 프로그램에서는 판별식으로 직선이 충돌했는지를 먼저 계산하면 불필요한 계산을 줄일 수 있다.



## 선분과 평면의 충돌



> 유니티 구현 코드

```C#
private void OnDrawGizmos()
{
    /*
    법선 벡터 : N(Nx, Ny, Nz)
    평면상의 한 점 : P(Px, Py, Pz)
    평면의 방정식 : Nx*x + Ny*y + Nz*z + d = 0
                    d = -N·Q = -(Nx*Px + Ny*Py + Nz*Pz)
    */
    Vector3 n = Plane.up.normalized; // 평면의 법선 벡터
    Vector3 p = Plane.position; // 평면상의 한 점
    Vector3 s = SegmentStart.position; // 공간상의 한 점

    // d값은 변하지 않기 때문에 미리 계산하는게 좋다.
    float d = -(n.x * p.x + n.y * p.y + n.z * p.z);
    // 공간 상의 점과 평면의 거리
    float distance = n.x * s.x + n.y * s.y + n.z * s.z + d;
    // 공간 상의 점과 평면을 연결하는 가장 짧은 벡터
    Vector3 shortestVector = -n * distance;

    // 선분 벡터
    Vector3 segment = SegmentEnd.position - SegmentStart.position;
    // 평면의 법선 벡터와 선분의 각도
    float angle = Vector3.Dot(-n, segment.normalized);
    // 선분의 시작에서 평면까지의 거리
    float distanceFromStartToPlane = distance / angle;
    // 선분의 시작에서 평면까지의 벡터
    Vector3 toPlane = segment.normalized * distanceFromStartToPlane; 

    Gizmos.color = Color.yellow;
    Gizmos.DrawLine(SegmentStart.position, SegmentEnd.position);

    // 제곱근 연산은 부하가 크기 때문에 길이의 제곱으로 비교한다.
    //if(distanceFromStartToPlane <= segment.magnitude)
    if (Mathf.Pow(distanceFromStartToPlane, 2) <= segment.sqrMagnitude)
    {
        Gizmos.color = Color.cyan; // 선분과 평면이 충돌함
    } else
    {
        Gizmos.color = Color.red; // 선분과 평면이 충돌하지 않음
    }
    Gizmos.DrawLine(SegmentStart.position, SegmentStart.position + toPlane);
}
```

