---
layout: post
title: "Windows - UNICODE vs ASCII"
description: ""
date: 2019-02-14 19:00:00+09:00
tags: [windows, unicode, ascii, c++]
comments: true
share: true
---

[TOC]



## ASCII

- 1Byte로 문자 표현



## Unicode

- 2Byte로 문자 표현
- 인코딩 종류
  - UTF-8
    - 영문 1바이트, 그 외는 2~4바이트
  - UTF-16
    - 모든 문자 2~4바이트
  - UTF-32
    - UCS-4와 동일하나 17개 언어만 정의한다는 점에서 UCS-4의 부분집합
  - UCS-2(Universal Character Set2(octets))
    - 한 문자를 2바이트로 고정하여 표현
    - 일반적으로 유니코드라고 불림
  - UCS-4(Universal Character Set4(octets))
    - 한 문자를 4바이트로 고정하여 표현
    - 인코딩 방법뿐만 아니라 문자코딩 자체임
    - 유니코드의 모든 문자열을 표현할 수 있음

#### octet

- 옥텟은 컴퓨팅에서 8개의 비트가 한데 모인것을 의미
- 초기 컴퓨터는 1바이트가 꼭 8비트를 의미하지 않았으므로 8비트를 명확하게 정의하기 위해 옥텟이라는 용어가 필요
- 현재는 바이트와 같은 의미



## 문자셋

약속된 문자의 표현방법

- SBCS(Single Byte Character Set)
  - ASCII
  - 모든 문자를 1byte로 표현
- MBCS(Multi Byte Character Set)
  - 다양한 Byte 수를 사용하여 문자를 표현
  - 아스키코드의 문자를 표현할 때는 1byte, 다른 문자를 표현할 때는 2byte로 처리
  - 윈도우는 기본적으로 문자를 MBCS 방식으로 처리한다.
- WBCS(Wide Byte Character Set)
  - Unicode
  - 모든 문자를 2byte로 표현



## MBCS 문제

- 문자열 길이를 일정하게 계산하기 힘들다
  - ascii 코드는 1
  - 그외는 2로 계산한다.



## WBCS

WBCS 방식은 모든 문자를 2바이트로 처리하기 때문에 MBCS 방식의 문제점이 나타나지 않는다.

- char -> wchar_t
  - char
    - 1byte
  - wchar_t
    - 2byte
    - Unicode 표현 가능
    - 선언 : typedef unsigned short wchar_t;
    - ANSI 표준에서 유니코드 지원을 위해서 정의한 표준 자료형
- "" -> L""
  - char str[] = "" -> wchar_t str[] = L"";
  - ""는 MBCS 기반의 문자열이다.
  - L은 유니코드 기반(WBCS)으로 표현하라는 의미
- 



## sizeof

sizeof는 함수가 아니라 연산자인다.



## Windows 자료형 조합원리

- LP = Long Pointer
- W = Wide
  - 2바이트 단위로 처리
- C = Const
- T = Template
  - TCHAR / _TCHAR를 사용하여 ANSI / Unicode에 호환되는 코드를 사용
- STR = Null Terminated
  - Null로 끝나는 문자열



## Windows 자료형 예

- char = 1byte
- wchar_t = 2byte
- char* = LPSTR = 1바이트 문자열
- const char* = LPCSTR = 1바이트 문자열 상수
- wchar_t* = WCHAR* = LPWSTR = wchar_t 단위의 Null로 끝나는 문자열
- 선언의 용이성과 확장성을 고려해서 typedef 기반으로 적절한 이름의 자료형을 정의하는 것은 좋은 프로그래밍 습관이다.



## 문자열 관련 함수

| SBCS   | WBCS                                                  |                                |
| ------ | ----------------------------------------------------- | ------------------------------ |
| printf | int wprintf(const wchar_t* format [, argument...]);   | Print formatted data to stdout |
| scanf  | int wscanf(wchar_t* format [, argument...]);          | Read formatted data from stdin |
| fgets  | wscanf* fgetws(wchar_t* string, int n, FILE* stream); | Get string from stream         |
| fputs  | int fputws(const wchar_t* string, FILE* stream);      | Write string to stream         |



#### 문자열 관련 함수에서 한글사용 시

```cpp
#include "locale.h"

_wsetlocale(LC_ALL, L"korean");
```



Windows2000 이상에서는 내부적으로 모든 문자열을 유니코드 기반으로 처리하므로 MBCS 방식으로 코드를 작성했다면 내부적으로 2바이트 유니코드 형식으로 변환하므로 프로그램 성능에 다소 영향을 미칠 수 있다.



## MBCS와 WBCS를 동시에 지원하기 위한 매크로

TCHAR, LPTSTR, LPCTSTR

```cpp
#ifdef UNICODE
	typedef 
#else
#endif
```



## main 함수를 유니코드 기반으로 작성하기

- main이라는 이름의 함수는 전달되는 문자열을 MBCS 기반으로 구성한다.
- wmain이라는 이름의 함수를 사용하면 전달되는 문자열이 유니코드 기반으로 구성된다. MS 확장.
- _tmain을 사용하면 유니코드 기능이 켜져있을 시 wmain을 사용하고 꺼져있으면 main을 사용한다. MS 확장.

```cpp
int wmain(int argc, wchar_t* argv[]);

int _tmain(int argc, _TCHAR* argv[]);
```





## 참고

- 뇌를 자극하는 윈도우즈 시스템 프로그래밍
- <https://s2junn.tistory.com/80>
- <http://dev.epiloum.net/487>

