#defined로 싱글턴 만들기
템플릿 함수 만들기

stl vector, list
vector<class Stage*> var // class를 왜쓰지?
// 전방선언으로 타입이 존재함을 알려주기 위해 class을 쓴다
// 여기서 하지 않으려면 상단에 class Stage를 선언해주고 vector<Stage*> 이렇게 쓰면 된다.

가상 소멸자

<map>은 느리다
<unordered_map>은 해시테이블로 저장해서 빠르다
<string> 그닥 빠르진 않다.




일반 함수에는 const 한정자를 지정할 수 없다.



배열 변수는 포인터지만 바꿀수 없으므로 자동으로 const이다.


$$
\begin{matrix}
	sp1, sp2 &:& \text{구의 중심점(sphere point)} \\
	v &:& \text{두 구의 중심점을 잇는 벡터(vector)} \\
	r1, r2 &:& \text{구의 반지름(radius)} \\
	\\
\end{matrix} \\

\begin{matrix}
	v = sp2 - sp1 \\
	\\
\end{matrix} \\

\begin{matrix}
	\therefore \rVert v \lVert < r1 + r2 \Rightarrow 충돌 \\
	\\
	\text{컴퓨터에서 제곱근 연산을 피하려면 제곱하여 비교한다.} \\
	v_x^2 + v_y^2 + v_z^2 < (r1 + r2)^2 \Rightarrow 충돌 \\
	\\
\end{matrix}\\

\text{충돌한 만큼 밀어내기} \\
\begin{matrix}
	idst &:& \text{침범한 거리(invasion distance)} \\
	nsp &:& \text{밀려난 새로운 위치(new sphere point)} \\
	\\
\end{matrix} \\

\begin{matrix}
	\therefore nsp = -\hat{v} \times idst \\
	\\
\end{matrix}
$$
