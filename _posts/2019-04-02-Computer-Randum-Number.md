---
layout: post
title: "Computer - Random Number"
description: ""
date: 2019-04-02 19:00:00+09:00
tags: [computer]
comments: true
share: true
---

[TOC]





## 랜덤 숫자

#### 공통 변수

- min : 최소값
- max : 최대값
- range : 최소값, 최대값 사이의 범위
- raw_random : 시스템에서 반환한 랜덤값
- RAND_MAX : 시스템에서 지원하는 랜덤 최대값(0x7fff : 32,767)



#### 정수(int) 랜덤값

- 범위 정하기
  - max 포함 : range = max - min + 1
  - max 미포함 : range = max - min
- 나머지 연산으로 범위에 해당하는 랜덤값으로 만들고 최소값 더하기
  - min + (raw_random % range)

```cpp
void int_random() {
	srand(time(NULL));

	int min = 1;
	int max = 5;
	int range = max - min + 1;

	for (size_t i = 0; i < 10; i++)
	{
		int raw_random = rand();
		int random = min + (raw_random % range);
		cout << raw_random << "\t" << random << endl;
	}
}
```



#### 부동소수점(float) 랜덤값 - 기본

- 범위 정하기 
  - range = max - min : 부동소수점에서는 range로 max값 포함 여부를 결정하지 않는다.
- raw_random 정하기
  - max 포함 : 시스템에서 반환한 값을 그대로 사용
  - max 미포함 : 시스템에서 반환한 값에서 1을 빼준다.
- 비율 만들기
  - raw_random을 RAND_MAX로 나누어 0~1 또는 0~0.999... 사이의 비율로 만든다.
- 최종값 만들기
  - 비율에 range를 곱하여 범위를 적용하고 min값을 더하여 완성.

```cpp
void float_random() {
	srand(time(NULL));

	float min = 7.0;
	float max = 8.0;
	float range = max - min;

	for (size_t i = 0; i < 10; i++)
	{
		int raw_random = rand(); // max 포함
		//int raw_random = rand() % (RAND_MAX - 1); // max 미포함
		float random = min + (((float)raw_random / RAND_MAX) * range);
		cout << raw_random << "\t" << random << endl;
	}
}
```





#### 부동소수점(float) 랜덤값 - 범위 묶기

- 범위를 묶어줄 숫자 지정 
  - range_bunch_count : 여기에 지정한 숫자만큼 범위가 분할 된다.
- 범위 정하기 
  - range = max - min : 부동소수점에서는 range로 max값 포함 여부를 결정하지 않는다.
- raw_random 정하기
  - 시스템에서 반환한 값을 range_bunch_count 로 나머지 연산하여 0~(range_bunch_count-1) 사이의 값으로 만든다.
- 비율 만들기
  - max 포함 : raw_random을 range_bunch_count 로 나누어 0.0~1.0 사이의 비율로 만든다.
  - max 미포함 : raw_random을 (range_bunch_count-1) 로 나누어 0.0~0.999... 사이의 비율로 만든다.
- 최종값 만들기
  - 비율에 range를 곱하여 범위를 적용하고 min값을 더하여 완성.



```cpp
void float_random_bunch() {
	srand(time(NULL));

	float min = 7.0;
	float max = 8.0;
	float range = max - min;
	int range_bunch_count = 3;

	for (size_t i = 0; i < 100; i++)
	{
		int raw_random = rand() % range_bunch_count;
		//float random = min + (((float)raw_random / (range_bunch)) * range); // max 포함
		float random = min + (((float)raw_random / (range_bunch_count - 1)) * range); // max 미포함
		cout << raw_random << "\t" << random << endl;
	}
}
```



## 선형합동법(Linear Congruential)

난수를 발생하는 알고리즘으로 부하가 적지만 품질이 낮다.

최대 M가지의 경우가 있고 난수의 주기도 최대 M이다.

짝수, 홀수가 반복된다.

하위 비트 쪽 정밀도가 떨어지고 최하위에 가까울 수록 정밀도는 현저히 떨어진다.

결과를 오른쪽으로 몇 비트시프트 시켜서 회피할 수 있고 좁아진 난수 범위는 M을 크게 해서 만회한다.


$$
\begin{gather*}
\begin{array}{ c c c }
X_{0} & : & 시드값\\
X_{n} & : & n번째\ 의사\ 난수\\
A,\ B & : & 서로소인\ 두\ 수\\
M & : & 정밀도
\end{array}\\
\\
X_{n+1} \ =\ ( A\times X_{n} +B) \%M
\end{gather*}
$$

#### A, B, M 숫자 정하기

- M : 2의 거듭제곱
- A : (A - 1)이 M의 모든 소인수로 나누어 지는 수
  - M을 2의 거듭제곱으로 정했으므로 2로 (A - 1)이 2로 나누어지면 된다.
  - M이 4의 배수일 경우 (A - 1)도 4의 배수여야 한다.
- B : A에 따라 서로소인 수로 정한다.



#### 선형합동법 구현

```cpp
void linear_congruential() {
	int m = 16;
	int a = 5;
	int b = 3;
	
	for (size_t i = 0; i < 20; i++)
	{
		int r = (a * i + b) % m;
		cout << r << endl;
	}
}
```









