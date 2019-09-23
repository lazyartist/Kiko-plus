---
layout: post
title: "Math - Linear Transformation"
description: ""
date: 2019-03-22 19:00:00+09:00
tags: [math]
comments: true
share: true
---

[TOC]



## 선형 변환의 벡터

선형 변환에 쓰이는 벡터는 x, y, z에 w가 추가된 4개의 성분은 갖는 벡터를 사용한다.

$$
\begin{pmatrix} 
x \\ y \\ z \\ w 
\end{pmatrix}
$$

### 좌표로 쓰이는 벡터

평행이동을 위해 w성분이 1이다.

$$
\begin{pmatrix} 
x \\ y \\ z \\ 1 
\end{pmatrix}
$$

### 벡터로 쓰이는 벡터

평행이동을 하지 않기(무의미 하기) 때문에 w성분이 0이다.

$$
\begin{pmatrix} 
x \\ y \\ z \\ 0 
\end{pmatrix}
$$

## 좌표와 벡터

|      | 크기 변환 | 회전 변환 | 평행 이동 |
| :--: | :-------: | :-------: | :-------: |
| 좌표 |     ○     |     ○     |     ○     |
| 벡터 |     ○     |     ○     |     ×     |

벡터는 실체(위치)가 없기 때문에 위치를 이동시키는 평행이동은 무의미하다.



## 평행 이동(Translation)

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



#### 



## 크기변환(Scaling) 행렬

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



## 회전 변환(Rotation)

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



## 행렬의 합성

여러 행렬을 한번에 곱해서 결과를 내야하는 경우 값이 고정된 행렬들을 미리 계산하여 하나의 행렬로 만들어 계산 횟수를 줄일 수 있다.

단, 행렬곱은 교환법칙이 성립하지 않으므로 순서를 변경하면 안된다.

$$
\begin{matrix}
V_{result} &=& M_t \times M_r \times M_s \times V \\
&=& M_{trs} \times V
\end{matrix} \\
\text{(일반적으로 크기 -> 회전 -> 이동 순으로 행렬을 적용한다.)}
$$



## 크기, 회전, 이동 행렬 구현

참고 : <https://www.euclideanspace.com/maths/algebra/matrix/functions/inverse/fourD/index.htm>

```csharp
// Matrix4 구조체 정의
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public struct Matrix4
{
    public float
            m00, m01, m02, m03,
            m10, m11, m12, m13,
            m20, m21, m22, m23,
            m30, m31, m32, m33;

    public Matrix4(
        float m00, float m01, float m02, float m03,
        float m10, float m11, float m12, float m13,
        float m20, float m21, float m22, float m23,
        float m30 = 0f, float m31 = 0f, float m32 = 0f, float m33 = 1f)
    {
        this.m00 = m00;
        this.m01 = m01;
        this.m02 = m02;
        this.m03 = m03;

        this.m10 = m10;
        this.m11 = m11;
        this.m12 = m12;
        this.m13 = m13;

        this.m20 = m20;
        this.m21 = m21;
        this.m22 = m22;
        this.m23 = m23;

        this.m30 = m30;
        this.m31 = m31;
        this.m32 = m32;
        this.m33 = m33;
    }

    public static Matrix4 operator /(Matrix4 m, float s)
    {
        return new Matrix4(
            m.m00 / s, m.m01 / s, m.m02 / s, m.m03 / s,
            m.m10 / s, m.m11 / s, m.m12 / s, m.m13 / s,
            m.m20 / s, m.m21 / s, m.m22 / s, m.m23 / s,
            m.m30 / s, m.m31 / s, m.m32 / s, m.m33 / s);
    }

    public static Matrix4 operator *(Matrix4 m, float s)
    {
        return new Matrix4(
            m.m00 * s, m.m01 * s, m.m02 * s, m.m03 * s,
            m.m10 * s, m.m11 * s, m.m12 * s, m.m13 * s,
            m.m20 * s, m.m21 * s, m.m22 * s, m.m23 * s,
            m.m30 * s, m.m31 * s, m.m32 * s, m.m33 * s);
    }

    public static Vector3 operator *(Matrix4 m, Vector3 v)
    {
        return new Vector3(
            m.m00 * v.x + m.m01 * v.y + m.m02 * v.z + m.m03 * 1f,
            m.m10 * v.x + m.m11 * v.y + m.m12 * v.z + m.m13 * 1f,
            m.m20 * v.x + m.m21 * v.y + m.m22 * v.z + m.m23 * 1f);
    }

    public static Matrix4 operator *(Matrix4 m0, Matrix4 m1)
    {
        return new Matrix4(
            m0.m00 * m1.m00 + m0.m01 * m1.m10 + m0.m02 * m1.m20 + m0.m03 * m1.m30,
            m0.m00 * m1.m01 + m0.m01 * m1.m11 + m0.m02 * m1.m21 + m0.m03 * m1.m31,
            m0.m00 * m1.m02 + m0.m01 * m1.m12 + m0.m02 * m1.m22 + m0.m03 * m1.m32,
            m0.m00 * m1.m03 + m0.m01 * m1.m13 + m0.m02 * m1.m23 + m0.m03 * m1.m33,

            m0.m10 * m1.m00 + m0.m11 * m1.m10 + m0.m12 * m1.m20 + m0.m13 * m1.m30,
            m0.m10 * m1.m01 + m0.m11 * m1.m11 + m0.m12 * m1.m21 + m0.m13 * m1.m31,
            m0.m10 * m1.m02 + m0.m11 * m1.m12 + m0.m12 * m1.m22 + m0.m13 * m1.m32,
            m0.m10 * m1.m03 + m0.m11 * m1.m13 + m0.m12 * m1.m23 + m0.m13 * m1.m33,

            m0.m20 * m1.m00 + m0.m21 * m1.m10 + m0.m22 * m1.m20 + m0.m23 * m1.m30,
            m0.m20 * m1.m01 + m0.m21 * m1.m11 + m0.m22 * m1.m21 + m0.m23 * m1.m31,
            m0.m20 * m1.m02 + m0.m21 * m1.m12 + m0.m22 * m1.m22 + m0.m23 * m1.m32,
            m0.m20 * m1.m03 + m0.m21 * m1.m13 + m0.m22 * m1.m23 + m0.m23 * m1.m33,

            m0.m30 * m1.m00 + m0.m31 * m1.m10 + m0.m32 * m1.m20 + m0.m33 * m1.m30,
            m0.m30 * m1.m01 + m0.m31 * m1.m11 + m0.m32 * m1.m21 + m0.m33 * m1.m31,
            m0.m30 * m1.m02 + m0.m31 * m1.m12 + m0.m32 * m1.m22 + m0.m33 * m1.m32,
            m0.m30 * m1.m03 + m0.m31 * m1.m13 + m0.m32 * m1.m23 + m0.m33 * m1.m33
            );
    }

    public Matrix4 Inverse()
    {
        //m00, m01, m02, m03,
        //m10, m11, m12, m13,
        //m20, m21, m22, m23,
        //m30, m31, m32, m33)

        //   0 1 2 3
        // 0 a b c d
        // 1 e f g h
        // 2 i j k l
        // 3 m n o p

        float det = 
              (m00 * m11 * m22 * m33) // +afkp
            - (m00 * m11 * m23 * m32) // -aflo
            - (m00 * m12 * m21 * m33) // -agjp
            + (m00 * m12 * m23 * m31) // +agln
            + (m00 * m13 * m21 * m32) // +ahjo
            - (m00 * m13 * m22 * m31) // -ahkn
            - (m01 * m10 * m22 * m33) // -bekp
            + (m01 * m10 * m23 * m32) // +belo
            + (m01 * m12 * m20 * m33) // +bgip
            - (m01 * m12 * m23 * m30) // -bglm
            - (m01 * m13 * m20 * m32) // -bhio
            + (m01 * m13 * m22 * m30) // +bhkm
            + (m02 * m10 * m21 * m33) // +cejp
            - (m02 * m10 * m21 * m31) // -celn
            - (m02 * m11 * m20 * m33) // -cfip
            + (m02 * m11 * m23 * m30) // +cflm
            + (m02 * m13 * m20 * m31) // +chin
            - (m02 * m13 * m21 * m30) // -chjm
            - (m03 * m10 * m21 * m32) // -dejo
            + (m03 * m10 * m22 * m31) // +dekn
            + (m03 * m11 * m20 * m32) // +dfio
            - (m03 * m11 * m22 * m30) // -dfkm
            - (m03 * m12 * m20 * m31) // -dgin
            + (m03 * m12 * m21 * m30) // +dgjm
            ;

        Matrix4 m = new Matrix4(
            m12 * m23 * m31 - m13 * m22 * m31 + m13 * m21 * m32 - m11 * m23 * m32 - m12 * m21 * m33 + m11 * m22 * m33,
            m03 * m22 * m31 - m02 * m23 * m31 - m03 * m21 * m32 + m01 * m23 * m32 + m02 * m21 * m33 - m01 * m22 * m33,
            m02 * m13 * m31 - m03 * m12 * m31 + m03 * m11 * m32 - m01 * m13 * m32 - m02 * m11 * m33 + m01 * m12 * m33,
            m03 * m12 * m21 - m02 * m13 * m21 - m03 * m11 * m22 + m01 * m13 * m22 + m02 * m11 * m23 - m01 * m12 * m23,
            m13 * m22 * m30 - m12 * m23 * m30 - m13 * m20 * m32 + m10 * m23 * m32 + m12 * m20 * m33 - m10 * m22 * m33,
            m02 * m23 * m30 - m03 * m22 * m30 + m03 * m20 * m32 - m00 * m23 * m32 - m02 * m20 * m33 + m00 * m22 * m33,
            m03 * m12 * m30 - m02 * m13 * m30 - m03 * m10 * m32 + m00 * m13 * m32 + m02 * m10 * m33 - m00 * m12 * m33,
            m02 * m13 * m20 - m03 * m12 * m20 + m03 * m10 * m22 - m00 * m13 * m22 - m02 * m10 * m23 + m00 * m12 * m23,
            m11 * m23 * m30 - m13 * m21 * m30 + m13 * m20 * m31 - m10 * m23 * m31 - m11 * m20 * m33 + m10 * m21 * m33,
            m03 * m21 * m30 - m01 * m23 * m30 - m03 * m20 * m31 + m00 * m23 * m31 + m01 * m20 * m33 - m00 * m21 * m33,
            m01 * m13 * m30 - m03 * m11 * m30 + m03 * m10 * m31 - m00 * m13 * m31 - m01 * m10 * m33 + m00 * m11 * m33,
            m03 * m11 * m20 - m01 * m13 * m20 - m03 * m10 * m21 + m00 * m13 * m21 + m01 * m10 * m23 - m00 * m11 * m23,
            m12 * m21 * m30 - m11 * m22 * m30 - m12 * m20 * m31 + m10 * m22 * m31 + m11 * m20 * m32 - m10 * m21 * m32,
            m01 * m22 * m30 - m02 * m21 * m30 + m02 * m20 * m31 - m00 * m22 * m31 - m01 * m20 * m32 + m00 * m21 * m32,
            m02 * m11 * m30 - m01 * m12 * m30 - m02 * m10 * m31 + m00 * m12 * m31 + m01 * m10 * m32 - m00 * m11 * m32,
            m01 * m12 * m20 - m02 * m11 * m20 + m02 * m10 * m21 - m00 * m12 * m21 - m01 * m10 * m22 + m00 * m11 * m22
        );

        return m * (1f / det);
    }

    public static Matrix4 CreateScale(float x, float y, float z)
    {
        return new Matrix4(
        x, 0, 0, 0,
        0, y, 0, 0,
        0, 0, z, 0,
        0, 0, 0, 1);
    }

    public static Matrix4 CreateRotation(float x, float y, float z)
    {
        Matrix4 rx = new Matrix4(
            1, 0, 0, 0,
            0, Mathf.Cos(x), -Mathf.Sin(x), 0,
            0, Mathf.Sin(x), Mathf.Cos(x), 0,
            0, 0, 0, 1);

        Matrix4 ry = new Matrix4(
            Mathf.Cos(y), 0, Mathf.Sin(y), 0,
            0, 1, 0, 0,
            -Mathf.Sin(y), 0, Mathf.Cos(y), 0,
            0, 0, 0, 1);

        Matrix4 rz = new Matrix4(
            Mathf.Cos(z), -Mathf.Sin(z), 0, 0,
            Mathf.Sin(z), Mathf.Cos(z), 0, 0,
            0, 0, 1, 0,
            0, 0, 0, 1);

        return rx * ry * rz;
    }

    public static Matrix4 CreateTranslation(float x, float y, float z)
    {
        return new Matrix4(
        1, 0, 0, x,
        0, 1, 0, y,
        0, 0, 1, z,
        0, 0, 0, 1);
    }
}


// Matrix4 구조체 활용하여 박스 변형 테스트
using System;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class MatrixTest : MonoBehaviour
{
    public float BoxSize; // Box Size
    public Transform Position;
    public Vector3 Scale = new Vector3(1f, 1f, 1f);
    [Range(0, 360)]
    public float RotationX = 0f;
    [Range(0, 360)]
    public float RotationY = 0f;
    [Range(0, 360)]
    public float RotationZ = 0f;


    private void OnDrawGizmos()
    {
        Vector3 pos = new Vector3(0f, 0f, 0f);
        float hSize = BoxSize / 2;
        Vector3[] boxVertecis = new Vector3[]
        {
            new Vector3(pos.x - hSize, pos.y- hSize, pos.z- hSize),
            new Vector3(pos.x + hSize, pos.y- hSize, pos.z- hSize),
            new Vector3(pos.x + hSize, pos.y + hSize, pos.z- hSize),
            new Vector3(pos.x- hSize, pos.y + hSize, pos.z- hSize),

            new Vector3(pos.x- hSize, pos.y- hSize, pos.z + hSize),
            new Vector3(pos.x + hSize, pos.y- hSize, pos.z + hSize),
            new Vector3(pos.x + hSize, pos.y+ hSize, pos.z + hSize),
            new Vector3(pos.x- hSize, pos.y + hSize, pos.z + hSize),
        };

        Matrix4 sm = Matrix4.CreateScale(Scale.x, Scale.y, Scale.z);
        Matrix4 rm = Matrix4.CreateRotation(RotationX * Mathf.Deg2Rad, RotationY * Mathf.Deg2Rad, RotationZ * Mathf.Deg2Rad);
        Matrix4 tm = Matrix4.CreateTranslation(Position.position.x, Position.position.y, Position.position.z);

        Matrix4 tsrm = tm * rm * sm;  // 변환 행렬의 적용 순서 반대로 곱해준다.
        Matrix4 tsrim = tsrm.Inverse();  // 역행렬


        // multifly matrix
        for (int i = 0; i < boxVertecis.Length; i++)
        {
            boxVertecis[i] = tsrm * boxVertecis[i];
        }

        // draw vertecis
        Color[] colors = new Color[] { Color.white, Color.yellow, Color.blue, Color.cyan };
        for (int i = 0; i < boxVertecis.Length; i++)
        {
            Color color = colors[(uint)i / 2];
            Gizmos.color = color;
            Gizmos.DrawWireSphere(boxVertecis[i], 0.1f);
        }

        // multifly matrix
        for (int i = 0; i < boxVertecis.Length; i++)
        {
            // 역행렬 곱해서 원래 좌표계로 돌림
            boxVertecis[i] = tsrim * boxVertecis[i];
        }

        // draw vertecis
        for (int i = 0; i < boxVertecis.Length; i++)
        {
            Color color = colors[(uint)i / 2];
            Gizmos.color = color;
            Gizmos.DrawWireSphere(boxVertecis[i], 0.1f);
        }
    }
}

```



## 좌표계 변환

### 로컬 좌표계

오브젝트에 붙어 있는 좌표계.



### 월드 좌표계

오브젝트가 놓여질 공간의 좌표계



### 뷰 좌표계

카메라가 원점인 좌표계

카메라를 월드에 배치하는 행렬의 역행렬은 카메라를 원점에 배치하는 행렬이된다. 

따라서 뷰 좌표계 변환 행렬은 카메라를 월드에 배치하는 행렬의 역행렬이다.



### 투영 좌표계

카메라에서 바라본 3D 오브젝트를 투영행렬을 이용하여 2D 스크린에 투영한 좌표계

- 투시투영(Perspective)
  - 원근감 적용
  - 4행이 (0, 0, 0, 1)이 아니라 (0, 0, 1, 0) 이다.
  - M_p를 곱한 후 w 성분으로 x, y, z를 나눈다.
- 정사투영(Orthographic)
  - 원근감 미적용



### 좌표계 변환 행렬 처리

로컬 -> 월드 -> 뷰 -> 투영 행렬을 하나로 합쳐서 처리한다.

$$
M_{wvp} = M_p \times M_v \times M_w \\
\grave{P} = M_{wvp} \times P \leftarrow \text{w성분으로 나눈다}
$$

위의 공식은 오브젝트 하나에 대한 변환 행렬이다.

따라서 각각의 오브젝트 마다 변환 행렬을 하나씩 만들어 줘야하는데 M_vp는 모든 오브젝트가 같기 때문에 물체마다 M_w를 계한하고 미리 계산한 M_vp와 계산하면 된다.



## 쿼터니온(사원수 - Quaternion)

회전만 필요한 곳의 정보는 쿼터니언으로 표시한다.

짐벌락을 피할 수 있다.

4개의 수로 회전을 표현한다.(변환 행렬의 1/4)

$$
쿼터니언의 표현 방식 \\
스칼라 :s, 허수 : i, j, k \\
q = (s; u, v, w) = s + ui + vj + wk
$$
