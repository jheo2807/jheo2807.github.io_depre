# Halting Problem

다른 예는 [https://www.youtube.com/watch?v=crK01_Mc5Nw&ab_channel=김필산의사이언스비치](https://www.youtube.com/watch?v=crK01_Mc5Nw&ab_channel=%EA%B9%80%ED%95%84%EC%82%B0%EC%9D%98%EC%82%AC%EC%9D%B4%EC%96%B8%EC%8A%A4%EB%B9%84%EC%B9%98)

이거에 어떻게 $input+1=output$이라는 알고리즘이 Turing Machine에서 작동하는지를 설명한다.

그러한 알고리즘 또한 0101010...로 나타낼 수 있다. 예를 들어 숫자에 1을 더하는 Turing Machine은 101011010111101010으로 나타내어진다. 이거는 십진법으로는 177642이다.

숫자를 2배하는 튜링머신은? 십진법으로 나타내면 1456581339이다.

그럼 여기서, 더 작은 튜링머신은 있을까? 만능 튜링머신은 그럼 십진법으로 표현할 수 있을까?

있다!

가장 작은 튜링머신, 0인 튜링머신은 그냥 오른쪽으로 쭉 간다. 노쓸모다. 버그가 있는 튜링머신(4)도 있다.

만능튜링머신은? +1을 하는 테이프를 읽으면 만능튜링머신은 그 기능을 복제하고, 인풋에 1을 더하는 행동을 복제한다. 이런 만능튜링머신의 코드 숫자는 10^1650자리수라고 한다. [https://www.youtube.com/watch?v=Aki_ix248ro&ab_channel=김필산의사이언스비치](https://www.youtube.com/watch?v=Aki_ix248ro&ab_channel=%EA%B9%80%ED%95%84%EC%82%B0%EC%9D%98%EC%82%AC%EC%9D%B4%EC%96%B8%EC%8A%A4%EB%B9%84%EC%B9%98)

자 여기서 또 문제. 전 페이지의 테이블 예에서 나온 튜링 머신은 H, 정지하는 부분이 있다. 그러나 작은 튜링머신, 코드 숫자 0짜리 놈은 그냥 오른쪽으로 쭉 간다. 정지하지 않는다.

정지 할 지 안할지, 어떤 튜링 머신이 정지 할 지 안 할 지 알 수 있을까?

예를 들어서, 어떤 프로그램(그지같이 안 열리는 MS Onenote를 생각하면 된다)의 튜링 머신을 Head가 읽고, 그것이 끝나는 지 안끝나는지 알 수 있는 어떤 **H** Turing Machine이 있다고 가정해보자.

그 다음 테이프에 끝나면 0을, 끝나지 않으면 1을 기록한다.

![image](assets\my_images\HaltingProblem.png){: .align-center}


H Turing Machine의 output을 input으로 받는, 어떤 **N** Turing Machine이 있다고 하자. H, 즉 정지하는 것을 안 N Turing Machine은 끝난다. 정지하지 않는다는거를 안 N Turing Machine은 끝나지 않는다. 즉 끝난다/끝나지 않는다 의 결과를 반대로 출력한다.

이 두개를 이어붙인 머신을 HN Turing Machine이라고 한다.

이 HN Turing Machine의 코드 숫자를 HN Turing Machine이 받는다고 하자. 이것의 목적은, HNTM이 멈추는지 안 멈추는지를 HTM이 말해줄 수 있는가이다. 

그리고 얘가 멈춘다고 가정하자.

HNTM 이 멈춘다: H가 멈춘다 → N이 멈추지 않는다 → HN은 멈추지 못한다.(가정 위반, 모순)

HNTM이 멈추지 않는다: H가 멈추지 않는다는 결과 출력 → N이 멈춘다 (가정 위반, 모순)

[https://www.youtube.com/watch?v=o34u3Ya_00k&ab_channel=김필산의사이언스비치](https://www.youtube.com/watch?v=o34u3Ya_00k&ab_channel=%EA%B9%80%ED%95%84%EC%82%B0%EC%9D%98%EC%82%AC%EC%9D%B4%EC%96%B8%EC%8A%A4%EB%B9%84%EC%B9%98)

이게 Halting Problem이다.

근데 이거 자기 자신을 포함해서 모순난거 아닌가...?

칸토어 방법으로 Halting Problem을 설명한 것도 있다. [https://www.youtube.com/watch?v=CXXB1bXckGQ&ab_channel=필스교양](https://www.youtube.com/watch?v=CXXB1bXckGQ&ab_channel=%ED%95%84%EC%8A%A4%EA%B5%90%EC%96%91)

모든 계산 기계, 심지어 양자 컴퓨터도 Turing Machine이 풀지 못하는 문제는 풀 수 없다. 계산 속도를 빠르게 해주는 것 뿐임. 즉 Turing Machine은 계산의 한계를 정의한거다.

Halting Problem같은, Turing Machine이 할 수 없는 것은 그럼 **계산이 아니다.**

Church-Turing Thesis에 따르면, 모든 계산은 오직 Turing Machine이나 Turing Machine의 발전형만이 할 수 있고, Turing Machine은 오직 계산밖에 못한다고 서술한다.

[https://www.youtube.com/watch?v=xIEB-BO6LT0&ab_channel=김필산의사이언스비치](https://www.youtube.com/watch?v=xIEB-BO6LT0&ab_channel=%EA%B9%80%ED%95%84%EC%82%B0%EC%9D%98%EC%82%AC%EC%9D%B4%EC%96%B8%EC%8A%A4%EB%B9%84%EC%B9%98)

Halting Problem에 대해서 가장 쉬운 visualization은

[https://www.youtube.com/watch?v=92WHN-pAFCs&ab_channel=udiprod](https://www.youtube.com/watch?v=92WHN-pAFCs&ab_channel=udiprod)

여기서 볼 수 있다. FAQ도!