---
title:  "Turing Machine"
excerpt: "튜링 머신에 대해"

categories:
  - QC
tags:
  - [QC, Math]

toc: true
toc_sticky: true
 
date: 2020-05-25
last_modified_at: 2020-05-25
---

# Turing Machine

Hibert: Definition과 Axiom을 입력하면 모든 Mathematical Theorem을 Deduce할 수 있는 만능 기계가 있지 않을까?

Godel: [https://www.notion.so/Incompleteness-Theorem-3eb7e41375d242a096423003e4273910](https://www.notion.so/Incompleteness-Theorem-3eb7e41375d242a096423003e4273910) 그런건 없어요~ 페아노 공리계가 포함된 모든 Non-paradoxical set of Axiom은 True인 일부 Theorem을 증명할 수 없다! → Deterministic 한 방법으로는, 모든 Mathematical Theorem을 deduce할 수 없다!

Alan Turing: 모든 Mathematical Theorem을 deduce하는 Universal Compute Machine을 만들었는데, 그 기계가 풀 수 없는 문제(Halting Problem)이 있다! 저 기계가 Computer의 원형 (On computable numbers, with an application to the Entscheidungsproblem(결정문제)) →계산 이론

Turing Machine?

수학적 도구, 기록을 할 수 있는 무한의 tape(memory), tape에 기록을 할 수 있는 기호, 기호를 읽거나 쓸 수 있는 head로 구성. Turing Machine은 추상적인 Automata이다.

[Automata](https://www.notion.so/Automata-d5b849054f5b4f8298a996d9a7c700fb)

![TuringMachine03](https://user-images.githubusercontent.com/48908914/148714112-ff4b0ed1-cdd0-4b88-81b0-20d0dfdb930f.png)

head는 state를 가지고 있다.

Tape: 기호 하나를 읽고 쓸 수 있는 Cell이 무한히 연결된 기억 장치

Head: 현재 위치한 셀을 읽고 쓰거나 좌우로 이동 가능한 제어장치

기호 집합: 테이프에 읽고 쓸 수 있는 기호들의 집합(정보, 숫자, 문자, 그림...)

상태 집합: Turing Machine이 가질 수 있는 state들의 집합

명령 테이블: 현재 상태와 기호에 따라 해야 할 일을 지정하는 명령 목록

Turing Machine은 무엇을 할까?

예를 들어보자.

기호 집합 $X = \{0,1\},$ 상태 집합 $S = \{s_0, s_1, H \}, s_0 : initial \ state, H:halting \ state$ 라고 하자. 명령 테이블이

![TuringMachine01](https://user-images.githubusercontent.com/48908914/148714051-ef891bbd-6abf-4751-8f94-e32e22346994.png)


이렇게 있을 때, 전부 0으로 초기화 된 테이프의 한 점에 헤드가 있으면 왔다 갔다 하면서 1 1 1 1, 15를 출력한다. [https://youtu.be/BOr1waCdv3U?t=863](https://youtu.be/BOr1waCdv3U?t=863)

이게 원시적으로 메모리에 15를 기록하는 튜링 머신인거다(가장 효율적인 튜링머신, 2개의 state로 4개의 1을 쓸 수 있는 가장 효율적인 알고리즘임)

다른 예 + 이 쪽에서 중요한 문제인 Halting 문제를 보려면 아래 페이지를 보자.

[Halting Problem](2011-01-11-HaltingProblem.md)

하여튼 이런 거를 The n-state Busy Beaver Problem이라고 하고, 이거를 더 멋있게 설명하는게 Finite State Automata이다.

[Busy Beaver](2011-01-11-BusyBeaver.md)

이런 식으로 튜링머신을 설계하면, (이론적으로)계산 가능한 모든 것을 할 수 있다.

즉 Computable하다는 뜻은 Turing Machine으로 풀 수 있다는 뜻이다. 실제 컴퓨터는 memory limit가 있고 state가 infinite하지 않아서 못함.

Shannon: 정보의 최소 단위는 비트이고, 고로 모든 정보는 0,1로 표현 가능하다.

그런데 튜링 머신이 0↔1을 바꿀 수 있다 → and, or, not(Bool)이 가능하다 → 사칙 연산이 가능하다 → 모든 연산이 가능하다.

보편적이다.

즉 Universal Turing Machine이다.

:임의의 Turing Machine M의 명령 테이블을 보고, 그것을 따라하는 Turing Machine UTM을 만들 수 있다.

그리고 이 Universal Turing Machine을 차용한게 현재의 컴퓨터다

![TuringMachine02](https://user-images.githubusercontent.com/48908914/148714101-ca2bdc95-d182-4330-8dab-3c2696abe73f.png)