# Busy Beaver

Busy Beaver Turing Machine, 줄여서 BB라고 하는 이 Concept은

"0으로 초기화 된 Tape에 **정지**하는 **n-state TM**이 가질 수 있는 **가장 많은 1의 수**" 를 구하는 것이다.

즉, n비트 길이의 프로그램 중 가장 복잡한 프로그램을 찾는 거다.

n-state TM이 가질 수 있는 TM의 갯수는

$$
Number \ of \ TM\ for \ n-state \ TM
\\
=(symbols(2, \{0,1\})\times direction(2,\{right,left\})\times(state+1))^{symbols \times states} \\
=[4(n+1)]^{2n}
$$

몇 개에 대해 테이블로 쓰면

|How Many TMs|n|BB(n)|
|------|---|---|
|64|1|1|
|20736|2|6|
|16777216|3|21|
|256*10^8|4|107|
|6.3*10^3|5|>47176870|


BB문제가 어려운 이유는, How many TMs, 저거를 TM중 정지하는 애들만 고려해야 하는데 이게 **halting problem**에 걸린다. 정지하지 않는 TM을 배제할 수 없고, 일일이 해봐야 한다...

[https://www.youtube.com/watch?v=CE8UhcyJS0I&ab_channel=Computerphile](https://www.youtube.com/watch?v=CE8UhcyJS0I&ab_channel=Computerphile)

[https://namu.wiki/w/바쁜 비버](https://namu.wiki/w/%EB%B0%94%EC%81%9C%20%EB%B9%84%EB%B2%84)

아니 근데 이게 뭐가 그렇게 의미가 있는 문제일까?

Scott Aaronson이 쓴 "큰 수 말하기"게임이 아주 잘 설명해놨다. 진짜, 말 그대로 아가들이 하는 큰 수 대기 게임. 물론 큰 수라기 보단 큰 수를 말하는 방법론인데 (큰 수 자체에 대해서는 아래 링크에 Graham Number, Skewes' number 등 재밌는 얘기를 많이 써놨다.) 이게 Ackermann Function이다.

덧셈을 반복하면 곱셈, 곱셈을 반복하면 제곱, 그럼 제곱을 반복하면? 그걸 또 반복하면? 이게 Hyperoperation이다. 4차 이상의 hyperoperation은 tetration, pentation등으로 부르고, 쓸 때는 $\uparrow, a\uparrow \uparrow b = a^{{a^{a^{\scriptstyle\cdot^{\scriptstyle\cdot^{\scriptstyle\cdot}}}}}}$저게 b개 있는거임. 그럼 Ackermann function은

$$
A(1) = 1+1=2 \\
A(2) = 2\times2=4 \\
A(3) = 3^3=27 \\
A(4) = 4^{4^{4^4}}= 3.blahblahblah...\times 10^{616}\\
$$

이렇다. 근데 이렇게 큰 수를 표기하는 법이 엄청 그 큰거로 생각했는데, 아예 그 체계를 바꾼거의 예제가 Busy Beaver이다!

처음은 이렇다.

"백 글자로 밝힐 수 있는 가장 큰 수"

이거는 자체로는 좀 명확한 정의가 아니여서 좀 더 바꾸어 쓰면

"1000 바이트 이하의 **TM**으로 **결정**되는 **가장 큰 수**"

큰 수를 표현하는, 묘사하는 방법을 아예 다른 식으로 생각하는 거가 Busy Beaver인거다. 오...

[https://pseudorandomstring.wordpress.com/2020/06/01/큰-숫자들-by-scott-aaronson/](https://pseudorandomstring.wordpress.com/2020/06/01/%ED%81%B0-%EC%88%AB%EC%9E%90%EB%93%A4-by-scott-aaronson/)

[https://namu.wiki/w/커누스 윗화살표 표기법](https://namu.wiki/w/%EC%BB%A4%EB%88%84%EC%8A%A4%20%EC%9C%97%ED%99%94%EC%82%B4%ED%91%9C%20%ED%91%9C%EA%B8%B0%EB%B2%95)