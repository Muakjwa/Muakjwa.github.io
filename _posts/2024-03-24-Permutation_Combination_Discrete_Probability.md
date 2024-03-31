---
title: 순열, 조합, 이산 확률
author: sunwoo
date: 2024-03-24 00:00:00 +0800
categories: [Lecture, Discrete Mathematics]
tags: [computer science]
math: true
comments: true
image: /assets/img/post/Permutation_Combination_Discrete_Probability/Untitled.png
---

# 순열, 조합, 이산 확률

# The rules of Sum and Product

- rule of product
    - 두 사건이 동시에 발생할 때, m*n outcome이 나온다.
    - ex) 학생이 아침, 오후 수업을 선택할 때
- rule of sum
    - 두 사건 중 하나의 사건만 발생할 때, m+n outcome이 나온다.
    - ex) 학생이 오전, 오후 중 하나의 수업만 선택할 때

# Permutation

ex) 빨강, 파랑, 흰 공을 서로 다른 10개의 상자에 넣는 방법의 수는?

10 X 9 X 8 = 720

ex) r개의 공을 서로 다른 n개의 상자에 넣는 경우의 수는?

$$
_nP_r \quad 또는 \quad P(n,r)
$$

ex) r개의 공을 서로 다른 n개의 상자에 중복을 허용하여 넣는 경우의 수는?

$$
n^r
$$

ex) 숫자가 1개 이상 반복되도록 10진수 4자리 숫자를 만드는 경우의 수는?

$$
9*10*10*10-9*9*8*7
$$

4자리 숫자를 만들 수 있는 모든 경우의 수에서 4자리 모두 다 다른 숫자가 나오는 경우의 수를 제외해준다.

ex) 상하좌우로 뒤집었을 때를 포함하여 만들 수 있는 distinct한 5자리 숫자들의 경우의 수는? 

(0, 1, 6, 8, 9가 뒤집었을 때, 숫자가 나온다)

$$
10^5-\frac{5^5-3*(5^2)}{2}
$$

상하좌우로 뒤집었을 때 숫자가 나오는 경우의 수인 $5^5/2$를 빼주는데 이 경우 중에서 상하좌우로 뒤집었을 때 자기 자신이 나오는 경우의 수를  $5^5$에서 빼준다.

ex) 학생이 하루에 한 과목씩 공부하는 일주일 계획을 세우려 한다. 학생은 4과목을 수강할 때, 각 과목을 적어도 하루씩 공부하는 경우의 수를 구하라.

전체 경우의 수에서 각 과목이 각자 포함되지 않을 경우의 합집합을 빼주면 된다.

$$
4^7-|A_1\cup A_2\cup A_3\cup A_4|
$$

# Combination

ex) r개의 색공에서 $q_1$개는 첫 번째 색, $q_2$개는 두 번째 색, …을 가진 공들을 n개의 박스에 넣는 경우의 수는?

$$
P(n,r)/(q_1!q_2!...q_r!)
$$

ex) 같은 색 공 r개를 n개의 상자에 넣는 경우의 수는?

$$
 _nC_r \quad 또는\quad C(n,r)
$$

ex) 11명의 후보 중 5명을 뽑는 경우의 수 : $C(11,5)$

(*** 1명을 당선 확정일 때 ***) : $C(10,4)$

(*** 1명은 뽑히지 못 할 때 ***) : $C(10,5)$

적어도 A or B 중 한 명은 당선될 경우의 수는?

$$
A뽑힘 +B뽑힘-A,B뽑힘\\
C(10,4)+C(10,4)-C(9,3)
$$

ex) 같은 색 공 r개를 n개의 상자들 속에 원하는 만큼 넣는 경우의 수는?

partition : n-1개이므로 n-1개의 partition과 r개의 공을 나열할 때, r개의 공의 위치만 정하면 되므로

$$
C(n+r-1,r)
$$

ex) 7일 중 3일을 고르는 경우의 수는?

7일의 partition : 6개, 3일 고르기

$$
C(9,3)
$$

ex) 3개의 주사위를 굴렸을 때 나올 수 있는 결과의 수는?

6개의 결과의 partition : 5개, 3개의 결과

$$
C(8,3)
$$

ex) 서로 다른 12개의 좌석에 서로 다른 5명의 학생이 앉는 경우의 수는?

$$
P(12,5)
$$

ex) 2t+1개의 공을 서로 다른 3개의 상자에 담을 때,\ 2개의 상자가 나머지 한 개의 상자보다 더 많은 공을 갖는 경우의 수는?

$$
C(2t+3,2t+1)-3C(t+2,t)
$$

# Catalan Numbers

![Untitled](/assets/img/post/Permutation_Combination_Discrete_Probability/Untitled.png)

다음과 같은 경로의 경우의 수를 구하는 문제는 $_{2n}C_n$의 경우의 수를 갖는다.

하지만 일부 경로를 지나지 못할 때의 경우의 수는 어떻게 구하는가?

Catalan Numbers 방식을 사용하면 된다.

# Discrete Probability

ex) 8명의 학생이 일렬로 서있을 때, 정확히 2명씩 서있을 확률은?

$$
8!/(2!2!2!2!)/4^8
$$

ex) 10명이 파티 후 랜덤으로 모자를 돌려받을 때, 모든 사람이 본인 모자를 돌려받지 못할 확률은?

$$
\frac{10!-|A_1\cup A_2\cup ... \cup A_{10}|}{10!}
$$

ex) n명의 학생 중 적어도 2명의 생일이 같을 확률은?

$$
1-\frac{P(365,n)}{365^n}
$$

# Conditional Probability

$$
P(A|B)
$$

이 수식은 B가 일어났을 때, A가 일어날 확률이란 의미를 갖는다.

조건부 확률은 pattern recognition을 잘하기 때문에 머신러닝에 많이 적용된다.

가장 유명한 이론으로 Bayes Theorem이 있다.

$$
P(C_j|F) =\frac{ P(F|C_j)P(C_j)}{\Sigma^n_{i=1}P(F|C_i)P(C_i)}
$$

몇몇 특징을 가진 동물이 어떤 종류인지를 예측할 때, bayes theorem을 이용하면, 각 동물들이 특징을 갖고 있는 확률을 알고 있으면 된다.

그러면 bayes theorem 공식을 이용해 특정 특징들에 대해 가능한 동물들의 확률을 output으로 얻을 수 있다.

이 공식은 유명한 Monty Hall Problem에도 사용될 수 있다.

(하나의 방에 차, 두 개의 방에 염소가 들어 있을 때, 선택자가 차가 있는 방을 고르면 차를 갖게 되는 게임이다. 진행자는 선택자가 방을 골랐을 때, 염소가 있는 방 하나를 열어줘 선택자에게 재선택의 기회를 준다.)

1) 선택자가 A 방을 선택했다고 가정한다.

2) 사회자가 i 번째 방을 열 확률을 $P(O_A)$라 가정한다.

3) $P(O_A|A)=0,\quad P(O_B|A)=\frac12, \quad P(O_C|A)=\frac12$

    $P(O_A|B)=0,\quad P(O_B|B)=0, \quad P(O_C|B)=1$

    $P(O_A|C)=0,\quad P(O_B|C)=1, \quad P(O_C|C)=0$

 

선택자가 A 방을 유지했을 때, 차를 가질 확률은 다음과 같다.

→ $P(A|O_B)=\frac{P(A\cap O_B)}{P(O_B)}=\frac{P(A)P(O_B|A)}{P(A)P(O_B|A)+P(B)P(O_B|B)+P(C)P(O_B|C)}=\frac13$

→ 선택을 바꿨을 경우는 위 선택의 여집합인 $\frac23$의 확률로 차를 갖게 된다.