### noexcept

https://jacking75.github.io/C++11_noexcept/

noexcept(true) or noexcept : 예외를 던질 가능성이 없는 함수

noexcept(false) : 예외를 던질 가능성이 있는 함수



### volatile

`volatile : [ˈvɑːlətl] 1. [흔히 못마땅함]사람·기분이변덕스러운`

변수에 volatile을 붙이면 해당 변수를 최적화에서 제외하여 항상 메모리에 접근하도록 만든다.

https://dojang.io/mod/page/view.php?id=749

```c++
int i = 0;
while (i < 10)
    i++;

// 컴파일러가 이렇게 최적화함
int i = 10;

volatile int j = 0;
while(j < 10)
    j++;
// j변수는 volatile로 인해 컴파일러가 최적화하지 않고 매번 메모리에 접근하게 됨
```



### volatile function?





### template <class t>?

typename 대신 class가 들어가는 이유?



### Variadic template

가변인자 템플릿

unique_ptr을 위해 C++11에서 만들어졌다.

안쓰는게 가장 좋다.





