### noexcept

​noexcept(true) or noexcept : 예외를 던질 가능성이 있는 함수

noexcept(false) : 예외를 던질 가능성이 있는 함수



### volatile

변수에 volatile을 붙이면 해당 변수를 최적화에서 제외하여 항상 메모리에 접근하도록 만든다.

```c++
int i = 0;
while (i < 10)
    i++;

// 컴파일러가 이렇게 만듦
int i = 10;

volatile int j = 0;
while(j < 10)
    j++;
// j변수는 volatile로 인해 컴파일러가 최적화하지 않음
```









