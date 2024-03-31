---
title: 집합과 명제
author: sunwoo
date: 2024-03-09 00:00:00 +0800
categories: [Lecture, Discrete Mathematics]
tags: [computer science]
math: true
comments: true
image: /assets/img/post/Set_and_Proposition/Untitled.png
---

# 집합과 명제

# Set

- a collection of distinct objects
- Notation
    - $\{a, b,c\}$
    - $S = \{a,b,c\}$
    - $S1=\{x|x\;is\;a\;student\;at\;DGIST\}$
- Venn diagram (집합을 이해하는 시각적 표현이다.)
→ 모든 것을 표현하지 못하는 한계 존재
ex) 원 4개를 이용해 A와 C, B와 D의 교집합을 동시에 그릴 수 없다.
- 기본 개념
    - Set S가 a를 가지고 있을 때 : $a\in S$
    - Set에서는 순서 상관 X : $\{a,b,c\} = \{b,a,c\}$
    - element 없는 건 Empty set : $\{\} \; or \; \phi$
    - 모든 element set은 Universal set : $U$
    - set은 set의 member가 될 수 있다. :  $\{\{a,b,c\},d\}$, $\{a,\{a\},\{\{a\}\}\}$, $\{\{\}\}$
    - Q의 모든 element가 P에 있을 때 Q는 P의 subset : 
    $Q \subseteq P$
    - 두 set이 같은 element를 가질 때 equal 관계 : $S1 = \{a,b,c\},\;S2=\{a,c,b\}$
    - $Q \subseteq P$ 이며 $P \; is\; not\; equal\; to \; Q$ 일 때 proper subset : $Q \subset P$
    - 두 set의 합집합 (Union) : $P\cup Q$
    - 두 set의 교집합 (Intersection) : $P\cap Q$
    - $((...((P_1\cup P_2)\cup P_3)...)\cup P_{k-1})\cup P_k$ 는 
    $P_1$부터 $P_k$까지에 존재하는 element set을 의미하므로 $P_1\cup P_2\cup P_3...\cup P_k$와 같다.
    - $((...((P_1\cap P_2)\cap P_3)...)\cap P_{k-1})\cap P_k$ 는 
    $P_1$부터 $P_k$ 모두에 존재하는 element set을 의미하므로 $P_1\cap P_2\cap P_3...\cap P_k$와 같다.
    - 교집합이 없는 두 set은 disjoint set이라고 한다. : $X\cap Y =\phi$
    - $P-Q :diffrence\;of\;two\;sets\quad ex)\;\{a,b,c\}-\{a,b\}=\{c\}$
    - $P\oplus Q:Symmetric \;Diffrence\quad ex)\;\{a,b,c\}\oplus\{a,c,d\}=\{b,d\}$
    - $\bar{Q} : complement\;of\;Q = U-Q$
    - $P(A) : power\;set\;of\;a\;set\;A$
    ex) $P(\{a,b\}) =\{\{\},\{a\},\{b\},\{a,b\}\}$
- Properties of Sets
    - Associativity : $(A\cup B)\cup C=A\cup (B\cup C)$
    - Commutativity : $A\cup B = B\cup A$
    - Distributive laws : $A\cap (B\cup C)=(A\cap B)\cup (A\cap C)$
    $R\cap (P_1\cup P_2...\cup P_k)=(R\cap P_1)\cup (R\cap P_2)...\cap(R\cup P_k)$
    - Identity laws : $A\cap U = A \quad and \quad A\cup \phi = A$
    - Complement laws : $A\cup \bar{A} =U \quad and \quad A\cap\bar{A}=\phi$
    - Idempotent laws : $A\cup A=A\quad and\quad A\cup A=A$
    - Bound laws : $A\cup U=U \quad and \quad A\cap \phi = \phi$
    - Absorption laws : $A\cup(A\cap B) = A \quad and \quad A\cap(A\cup B) = A$
    - Involution law : $\bar{\bar{A}} = A$
    - 0/1 laws : $\bar{\phi} = U \quad and \quad \bar{U}=\phi$
    - De Morgan’s laws :
    
    ![Untitled](/assets/img/post/Set_and_Proposition/Untitled.png)
    

set에서 distinct한 것들의 수를 Cardinality라고 한다.

ex) {a,b,c}의 cardinality는 3, $\phi$의 cardinality는 0이 된다.

※ {a, $\phi$, c}의 cardinality는 3이다. ※

set인 A에 대해서 $A: A^+=A\cup \{A\}$라고 할 수 있고, 

$A^+$는 succesor of A라고 할 수 있다.

ex) 폰 노이만 방식은 $\phi$ = 0,       $\phi \cup \{\phi\}=\{\phi\}$ = 1로 자연수를 정의한다.

$$
\mathbb{N}=\{0, ...,n,n^+,...\}
$$

이처럼 자연수를 정의할 수 있다. 

직관적으로 봤을 때, n은 무한히 뻗어나갈 수 있으므로 $\mathbb{N}$은 infinite set이다.

하지만 특정 set A이 $\mathbb{N}$의 임의의 원소 n과 one-to-one correspondence 관계라면 A는 finite set이라 정의된다.

infinite set의 정의는 finite 하지 않은 set을 의미한다. (finite set의 여집합이다)

infinite은 countably infinite과 uncountably infinite으로 나뉜다.

countably infinite set은 $\mathbb{N}$과 1-1 correspondence를 갖는 set을 의미한다.

ex) odd set $\mathbb{O}$와 even set $\mathbb{E}$는 $\mathbb{N}=\mathbb{O}\cup\mathbb{E}$를 만족하고 even, odd set은 모두 countably infinite set이다.

따라서 실수 set은 uncountably infinite set이지만 다음 set들은 countably infinite set이고,

이 set들의 cardinality는 모두 같다고 볼 수 있다.

$$
|\mathbb{N}|=|\mathbb{E}|=|\mathbb{O}|=|\mathbb{Z}|=|\mathbb{Q}|
$$

uncountably infinite set은 infinite set의 정의와 같이 countably infinite set의 여집합이다.

- Principle of Inclusion and Exclusion
$|P| : set\;P의 \;cardinality$
    - 1) $|P\cup Q| \le |P|+|Q|$
    - 2) $|P\cup Q| \le min(|P|,|Q|)$
    - 3) $|P\bigoplus Q|=|P|+|Q|-2|P\cap Q|$
    - 4) $|P-Q| \ge |P|-|Q|$

$$
|A_1\cup ...\cup A_n|=\sum_{i=1}^n|A_i|-\sum_{1\le i < j\le n}|A_i\cap A_j|+\sum_{1\le i<j<k\le n}|A_i\cap A_j\cap A_k|-...+(-1)^{n-1}|A_1\cap ... \cap A_n|
$$

# Multiset

multiset은 set과 다르게 distinct하지 않은 object들의 collection이 가능하다.

ex) S = {a, a, a, b, b, c}

multiplicity는 multiset의 특정 원소의 개수를 의미한다.

ex) S에서 a의 multiplicity = 3이 된다.

multiset의 Cardinality는 multiset의 원소 개수와 같다.

- Union
    - $P=\{a,a,a,c,d,d\},\quad Q=\{a,a,b,c,c\}$
    - $P\cup Q=\{a,a,a,b,c,c,d,d\}$
- Intersection
    - $P\cap Q=\{a,a,c\}$
- Difference
    - $P-Q=\{a,d,d\}$
- Sum
    - $P+Q=\{a,a,a,a,a,b,c,c,c,d,d\}$

# n-Tuple

튜플은 순서를 갖는 정렬된 데이터를 의미한다.

$(x,y)$와 같이 표현할 수 있고, x, y의 순서를 갖는다.

- Cartesian product
    - $X=\{1,2,3\}, \; Y=\{a,b\}$
    - $X\;\mathrm{x}\;Y=\{(1,a),(1,b),(2,a),(2,b),(3,a),(3,b)\}$
    - $Y\;\mathrm{x}\;X=\{(a,1),(a,2),(a,3),(b,1),(b,2),(b,3)\}$

n-Tuple과 같이 n이 붙어있는 튜플은 finite한 ordered list를 의미한다.

# Proposition

명제는 참, 거짓만을 갖는 평서문이다.

- Tautology : 항상 참인 명제
- Contradiction : 항상 거짓인 명제

명제 p와 q가 logically equivalent하다는 것은 p가 true이면 q도 true이고, p가 false이면 q도 false임을 의미한다.     ( $p\equiv q$)

- Disjunction $(P\lor Q)$

![Untitled](/assets/img/post/Set_and_Proposition/Untitled 1.png)

- Conjunction $(P\land Q)$

![Untitled](/assets/img/post/Set_and_Proposition/Untitled 2.png)

- Negation $(\bar{P})$

![Untitled](/assets/img/post/Set_and_Proposition/Untitled 3.png)

- if P then Q $(P\to Q)$

![Untitled](/assets/img/post/Set_and_Proposition/Untitled 4.png)

- P if and only if Q $(P \leftrightarrow Q)$

![Untitled](/assets/img/post/Set_and_Proposition/Untitled 5.png)

compound propostion을 풀 때, 연산자 적용 순서는 다음과 같다.

$$
\lor,\quad \land,\quad \bar{}\;\;,\;\;\to,\quad\leftrightarrow
$$

![Untitled](/assets/img/post/Set_and_Proposition/Untitled 6.png)

위의 compound propostion 예시는 $P\lor Q$와 같은 결과를 가지고,

두 proposition은 logically equivalent 관계이다.

- Quantifier
    - universal quantifier : $\forall$
        - 모든 $x\in D$에 대해 $P(x)$가 true이면 $P(x)$는 true이다.
        - 모든 $x\in D$에 대해 $P(x)$가 false이면 $P(x)$는 false이다.
    - existential quantifier : $\exist$
        - $\exist x\;P(x)$ : P(x)가 true인 x가 존재한다.
    - Counter example
        - P(x)가 false임을 보이려면 모든 x에 대해 볼 때, true가 아닌 false 하나만 찾으면 된다.

# Mathematical Induction

ex) 자식이 0명이거나 2명인 tree에서 leaf node는 internal node보다 항상 1개 더 많다 증명

→ 

1. $n = n_0$
n=1일 때, root node만 있으므로 명제 true
2. $true \quad for\quad n=k+1\quad (n_0\le n\le k)$
1~k에서 true라 가정하고 k+1을 확인해본다. 

$$
L_1=I_1+1\\
L_2=I_2+1일 \;때,\\
k+1의 \;상황에서는\\
L=L_1+L_2=I_1+I_2+2=I+1
$$