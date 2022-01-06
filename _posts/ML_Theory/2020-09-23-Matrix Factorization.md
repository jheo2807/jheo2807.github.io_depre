---
title:  "Matrix Factorization"
excerpt: "Matrix Factorization의 이론을 정리한 글"

categories:
  - Background in Machine Learning
tags:
  - [ML, Recommender, Mathematics]

toc: true
toc_sticky: true
use_math: true 

date: 2020-09-23
last_modified_at: 2020-09-23
---

# Matrix Factorization 이론 정리

논문이랑 블로그 글 읽고 정리한거임. 개소리일수도 있음...

내가 원래 가지고 있던 궁금증이, 매트릭스 $R$ 과 최대한 근접할 (rmse측면에서) $\hat R$을 만들바엔, 차라리 그냥 $R$을 쓰면 되는거 아닌가?  $R$을 쓰면 overfitting이고 missing value interpolation이 안된다면서 왜 $\hat R$은 최대한 $R$과 가깝게 하는 것인가? 최적으로 되서 $R$ = $\hat R$이 되면 오버피팅인데?? 라는 의문이 들었음

자 행렬 $R$을 singular value decomposition하면 $R = U \Sigma V^T$로 쪼갤 수 있다.

$R = m*n$ 이면 $U = m*l, \Sigma = l*l, V^T = l*n$ 매트릭스가 될 거다.

그치만 우리에게 할당된 문제는 쪼개는게 아니라 matrix completion이다. missing value들, 사용자가 아직 평가하지 않은 데이터들을, 즉 매트릭스에서 비어있는 부분의 값을 예측하는 문제다.

그럼 우리에게 할당된 문제는 아래의 식이 된다. 여기서 $\hat R$이 "예측한" 행렬이다. 그리고 비어있지 않은 곳에 대해서만 저 obj. func.를 계산한다.

$$
\min_{\mathbf{\hat{R}}} \left\|
\mathbf{\hat{R}}-\mathbf{R}
\right\|^2_F
$$

우리의 메트릭스의 기본 전제는 missing value가 엄청 많다 (matrix 가 sparse하다) & matrix의 data가 매우 redundant 하다다.  ($R$ 이 low rank matrix다)

matrix가 redundant하다는게 뭔가? 예전에 선형 대수학에서 Gaussian Elimination을 배웠다. 같은 행을 지워서 nullity 행이나 redundant하는 행이 없게 matrix를 reduce해주는거다. 

그러면 missing value외의 element에 대해서만, 최대로 reduce해주는게 목표가 된다(missing value는 reduce하고 자시고 할 기준이 없으니). 이러한 문제를 constrained optimization 문제라고 하고 식으로는

$$
min \ rank(\hat{R}) \ s.t. \ 
\Omega(r_{ui}-\hat{r}_{ui}) =0 \ {} \ \forall u,i
$$

로 표현할 수 있다. 여기서 $\Omega$ 는 $r_{ui}, \ \hat r_{ui}$ 둘 다 element가 있는 거만 신경쓴다는 뜻이다. 즉 저 문제는 위 SVD에서 $\Sigma$최소, 즉 최소한의 latent feature를 사용하여 $U$ 와 $V$를 표현하라는 것이다.

그런데 저기서 이 rank condition(missing value 많은거, sparse) 가 convex optimization이 아니라서 이 문제를 optimal로 풀 수가 없단다. 

그러나 이런 rank-minimization은 NP-hard문제로 there is no efficient way to solve this problem.

[http://citeseerx.ist.psu.edu/viewdoc/download;jsessionid=D59578D6141F1F00F48AD3D4632A7FF9?doi=10.1.1.365.8055&rep=rep1&type=pdf](http://citeseerx.ist.psu.edu/viewdoc/download;jsessionid=D59578D6141F1F00F48AD3D4632A7FF9?doi=10.1.1.365.8055&rep=rep1&type=pdf) - 관련 논문

근데 왜 이런 문제가 optimal이 불가일까? 자 convexity의 필요 조건은 Hessian matrix가 positive semidefinite 가 돼야 한다. (Convex 함수라는거 자체가 Hessian matrix가 positive semidefinite인 함수를 뜻한다. 그리고 모든 local minima가 곧 global minima임을 보장받는다.)  Positive semidefinite란 (참조: [https://be-favorite.tistory.com/46](https://be-favorite.tistory.com/46))

$$
M\ is\ positive\ definite\ =\ x^T Mx > 0 for\ all\ x \in \R^n
$$

$$
M\ is\ positive\ semi-definite\ =\ x^T Mx \geq 0 for\ all\ x \in \R^n
$$

$$
M\ is\ negative\ definite\ =\ x^T Mx < 0 for\ all\ x \in \R^n
$$

$$
M\ is\ semi-negative\ definite\ =\ x^T Mx \leq 0 for\ all\ x \in \R^n
$$

라는 크거나 bounded된 거여야 한다.

근데 이제 우리꺼가 Non-negative matrix factorization인데, 이거의 Hessian이 positive semidefinite가 아니다.

Q: [https://math.stackexchange.com/questions/393447/why-does-the-non-negative-matrix-factorization-problem-non-convex](https://math.stackexchange.com/questions/393447/why-does-the-non-negative-matrix-factorization-problem-non-convex)

$$
Supposing \ 
\mathbf{X} \in \mathbb{R}^{m \times n}_{+}, \ 
\mathbf{Y} \in \mathbb{R}^{m \times r}_{+}, \ 
\mathbf{W} \in \mathbb{R}^{r \times n}_{+}, \ 
the \ non-negative \ matrix \ factorization \ problem \ is \ defined \ as: 
\\ {}
\\
\min_{\mathbf{Y},\mathbf{W}} \left\|
\mathbf{X}-\mathbf{Y}\mathbf{W}
\right\|^2_F
\\ {}
\\
Why \ is \ this \ problem \ non-convex?
$$

A:

$$
Consider \ the \ scalar \ case; \ that \ is, \ m=n=1. \ Then \ the \ problem \ is
\\ {}
\\
\min_{y,w \ge0}(x-yw)^2
=
\min_{y,w \ge0}x^2
-
2xyw
+y^2w^2
\\ {}
\\
(Definition)\ The \ gradient \ \nabla f \ and \ Hessian \ \nabla^2 f \ of \ a \ function \ f \ is
\\ {}
\\
\nabla f = 
\begin{pmatrix}
{\partial f \over \partial{x_1}}
\\
{\partial f \over \partial{x_2}}
\\
\vdots
\\
{\partial f \over \partial{x_n}}
\end{pmatrix}
,
 \ and \ 

\nabla^2 f = 
\begin{pmatrix}
{\partial^2 f \over \partial{x_1^2}}
&
{\partial^2 f \over \partial{x_1}\partial{x_2}}
&
\cdots
&
{\partial^2 f \over \partial{x_1}\partial{x_n}}

\\

{\partial^2 f \over \partial{x_2}\partial{x_1}}
&
{\partial^2 f \over \partial{x_2^2}}
&
\cdots
&
{\partial^2 f \over \partial{x_2}\partial{x_n}}

\\
\vdots  & \vdots  & \ddots & \vdots
\\
{\partial^2 f \over \partial{x_n}\partial{x_1}}
&
{\partial^2 f \over \partial{x_n^2}\partial{x_2}}
&
\cdots
&
{\partial^2 f \over \partial{x_n^2}}
\end{pmatrix}

\\ {}
\\
Then \ the \ gradient \ and \ Hessian \ of \ \phi_x(y,w)=x^2-2xyw-y^2w^2 \ is
\\ {}
\\
\nabla \phi_x(y,w)
=
\begin{bmatrix}
2yw^2-2xw \\
2y^2w-2xy
\end{bmatrix}
\\
\nabla^2 \phi_x(y,w)
=
\begin{bmatrix}
2w^2 & 4yw-2x \\
4yw-2x & 2y^2
\end{bmatrix}

\\ {}
\\

The \ Hessian \ is\ not \ positive \ semidefinite \ for \ all \ x,y,w\ge0. \ For \ example, \\
\nabla^2 \phi_1(2,1)
=
\begin{bmatrix}
2 & 6 \\
6 & 8
\end{bmatrix}
,
 \ 
\lambda_{min}(\nabla^2\phi_1(2,1))
=
-1.7082

$$

자 위에꺼는 솔직히 자기 만족인데, 이제 우린 sparse matrix의 factorization문제가 non-convex np-hard문제여서 global optimum을 찾을 수 없다는걸 알았다.

사실 처음의 의문에 답이, bias를 통해서 $R$ = $\hat R$를 막는건가? 했는데 bias는 interaction tern과의 integration을 통해 columns(or row) bias를 막고 generalization 하는거지 (overfitting 방지) 내가 생각한 이유는 아니다. [https://stats.stackexchange.com/questions/113390/the-role-of-the-bias-terms-in-matrix-factorization-formulas](https://stats.stackexchange.com/questions/113390/the-role-of-the-bias-terms-in-matrix-factorization-formulas)

왜 저 rank condition이 non-convex condition인지에 대한 다른 설명이 있다. 일단 어떤 행렬의 rank는 missing value가 아닌 singular value들의 갯수, 즉 $l_0 \ norm$으로 표현할 수 있다. 즉 다른 말로

$$
min \sum_l \| \sigma_l (\hat R) \|_0 \ s.t.\ \Omega (r_{ui} - \hat r_{ui}) = 0 \ \forall u,i
$$

이다. 여기서 $\sigma_i(A)$는 A의 i번째 singular value이다. 근데 이 $l_0 \ norm$자체가 non convex norm이다. 놈에 대한 설명은 [https://bskyvision.com/825](https://bskyvision.com/825) 를 참조하면 되겠다. 

> 대부분이 2-norm의 제곱인 Euclidean distance를 사용한다. 때문에 이는 데이터의 제곱에 루트를 씌운 것에 또 제곱을 취하기 떄문에 그냥 절대값을 더하는 l1 norm등에 비해 outlier에 더 취약하다. 가장 robust한 norm은 l0 norm이지만 이것은 non-convex하기 때문에 보통 l1 norm으로 relax시켜서 계산을 하게 된다.
> 

[http://hnwoo.egloos.com/5870010](http://hnwoo.egloos.com/5870010)

[https://light-tree.tistory.com/125](https://light-tree.tistory.com/125)

저 $l_0 \ norm$을 $l_1 \ norm$으로 relaxation해서 풀 수도 있는데, 대부분 MF방법론은 non-convex 문제에 regularization term을 집어넣어서 overfitting을 피한 뒤 pair-wise optimization문제로 바꿔쓰고 gradient descent method로 local minima를 찾는 방법을 쓴다.

그 다음은 [https://teamlab.github.io/jekyllDecent/blog/basics for ml / dl/Matrix-factorization](https://teamlab.github.io/jekyllDecent/blog/basics%20for%20ml%20/%20dl/Matrix-factorization) 참조

주 참조: [http://sanghyukchun.github.io/73/](http://sanghyukchun.github.io/73/)