---
title:  "소박한 집합론의 역설"
excerpt: "뭐더라..."

categories:
  - QC
tags:
  - [QC, Math]

toc: true
toc_sticky: true
 
date: 2020-05-25
last_modified_at: 2020-05-25
---

# 소박한 집합론의 역설

집합론이 제대로 정의된 시절같지는 않다(아마도?). 

현대 수학의 모든 것은 집합으로 정의되는데, 연산도 집합이고 행력, 벡터 등도 집합이다.

고전적으로는, 집합은 직관 또는 사고의 대상이며, 명확히 확정되고 분명히 구별되는 것의 모임이다.

예를 들어 수학을 잘하는 사람의 모임은 집합이 될 수 없다. 기준이 없기 때문에.

여기서 칸토어의 역설이 나온다.

칸토어의 역설을 보기 전에, 칸토어의 정리를 보자.

**Cantor의 정리**

**임의의 집합 X에 대해, #X < #P(X)이다.**

여기서 정의를 먼저 주자면, #는 기수(원소의 갯수), P는 멱집합(원래 집합의 부분집합을 끌어모은 집합)이다.

증명은 X 가 공집합일 때, 아닐 때로 나눠서 한다.

1) $X = \phi$일 때, (공집합)

$X = \phi \rightarrow \#X = 0 \\ 
P(X) = \{\phi\} \rightarrow \#P(X) = 1, \ Q.E.D.$ 

2) $X\neq\phi$일 때, (공집합 아님)

이 경우는 '작거나 같다'라고 가정한 뒤 반증을 하여 귀류법으로 증명한다.

$\#X \leq \#P(X), \ e.g. \ X=\{\{x\}|x\in X\} \leq P(X)$

자 기수가 '같다'라는 뜻은, 두 집합 사이에 1대1 대응이 존재한다는 뜻이다(마치 칸토어 무한 기수 비교처럼).

여기서 '특정 원소'만 없는 집합을 S라고 하자. $e.g. \ S = \{x\in X|x \notin f(x)\}$

만약 a라는 원소가 S에 속해있다면, a는 f(a)의 원소가 아니다. $if \ a\in S \ then \ a \notin f(a)$

a가 S의 원소라면, a는 S의 정의상 f(a)의 원소가 아니라서 모순이다. 즉 a는 S의 원소로 있을 수 없다.

근데 a가 S의 원소가 아니라면, a는 f(a)의 원소가 아닌데, 이거는 S의 정의상 a는 S의 원소여야 해서 모순이다.

즉 첫 가정 $\#X = \#P(X)$가 귀류법에 의해 틀린것이고, 같지는 않다는게 증명된다.

$\therefore \#X < \#P(X)$

**Cantor의 역설**

칸토어의 역설은, 모든 집합의 집합이 없다는거다.(집합으로써 존재할 수는 없다는 뜻)

모든 집합들의 집합을 U라고 했을 때, 그 기수를 #U = q라고 하자.

칸토어 정리에 따라

$\#P(U) = 2^q >\#U=q$이지만, 우리는 U를 모든 집합의 집합으로 가정했잖아? 모든 집합의 집합보다 기수가 큰 집합이 있다니... 칸토어 정리에 따르면 저기에 등호가 들어갈 수 없어서 역설이 된다!

러셀의 역설은 타이핑하기 귀찮으니...

![Untitled](assets\my_images\NaiveSet.png)