---
title: Blur and Disparity are Complementary Cues to Depth
author: sunwoo
date: 2024-02-17 00:00:00 +0800
categories: [Research, Sight Model]
tags: [blur]
---

# 논문 요약

가까운 거리에 있는 물체의 depth를 인지할 때는 diparity가 더 좋은 성능, 
먼 거리에 있는 물체의 depth를 인지할 때는 blur가 더 좋은 성능을 내서

안구는 disparity와 blur가 depth를 인지하는데 서로 상호 보완적인 역할을 한다.

# Background Concept

- Disparity와 Blur의 차이
1. Disparity

disparity는 주로 양안시차(binocular disparity)로 언급된다.
이는 눈이 서로 다른 위치에 있기 때문에 같은 장면을 조금씩 다른 각도에서 보게 되는 현상을 말한다.

이러한 각 눈의 이미지 간의 차이는 우리 뇌가 공간적 깊이와 3D 형태를 인지하는데 사용된다.

양안 시차는 3차원 공간에서 물체의 상대적 위치와 거리를 인식하는데 중요한 역할을 한다.

1. Blur

blur는 이미지나 물체의 가장자리가 선명하지 않고 부드럽게 퍼져 보이는 현상을 의미한다.

눈이나 카메라 렌즈가 특정 거리에 초점을 맞추고 있을 때, 그 초점 거리에서 벗어난 물체들은 흐릿하게 보인다. 이를 **Defocus Blur**라고 한다.

이 현상은 깊이 인식에 도움을 줄 수 있고, 사진이나 영상에서 배경과 주요 피사체를 구분하는데 사용된다.

# Theorical result

![Figure 1. Geometry of Disparity and Blur ](/assets/img/post/Geometry_of_Disparity_and_Blur(1).png)

Figure 1. Geometry of Disparity and Blur 

![Untitled](/assets/img/post/Geometry_of_Disparity_and_Blur(2).png)

User가 초점을 두고 있는 곳과의 거리 : $z_0$

User가 초점을 두고 있는 물체와 떨어져 있는 물체와의 거리 : $z_1$

interocular distance (안구간 거리를 의미하며 일반적으로 62mm다.) : $l$ 

optical center와 retina 사이의 거리 (figure 1 참조) : $s$

![Equation 1](/assets/img/post/Equation_of_Disparity_and_Blur(1).png)

Equation 1

이 방정식의 output인 $d$는 *units of distance*이다*.*

이 방정식을 small-angle approximation하면 다음과 같은 식을 얻을 수 있다.

(small-angle approximation로 $d$를 radians인 $\delta$로 변환하였다.)

![Equation 2](/assets/img/post/Equation_of_Disparity_and_Blur(2).png)

Equation 2

논문의 저자는 blur를 $z_1$의 point가 망막에 맺히는 원의 지름으로 정의한다.

$A$는 pupil(동공)의 지름을 의미한다.

![Equation 3](/assets/img/post/Equation_of_Disparity_and_Blur(3).png)

Equation 3

이렇게 만들어진 blur의 정도는 diffraction이나 high-order aberration이 아닌 defocus로 인해 발생한 blur를 의미한다.

$\delta와 d$는 disparity를 $\beta$는 blur를 표현하기 위해 사용된 기호이고,
disparity와 blur는 서로 relationship을 갖는다. 이를 equation으로 표현하면 다음과 같다.

![Equation 4](/assets/img/post/Equation_of_Disparity_and_Blur(4).png)

Equation 4

# Experimental result

위의 이론적 결과를 설명하기 위해 이 논문에서는 4명의 피실험자에게 실험을 진행하였다.

3가지 조건의 상황에서 피험자가 depth를 판단하고

depth의 오차가 적은 상황에서 depth를 잘 판단한다고 볼 수 있다.

- 조건 1: Blur만 있는 경우 (단안 시야로 초점 거리가 다른 자극 관찰)
- 조건 2: Disparity만 있는 경우 (양안 시야로 초점 거리가 동일한 자극 관찰)
- 조건 3: Disparity와 Blur가 모두 있는 경우 (양안 시야로 초점 거리가 다른 자극 관찰)

해당 조건들에 대해서 실험을 진행하였을 때,

![Untitled](/assets/img/post/Result_of_Disparity_and_Blur.png)

해당 피규어와 같은 결과가 나온다.

논문의 저자는 이 결과로부터
Disparity는 가까운 거리의 물체의 depth를 잘 판단하고,
Blur는 먼 거리의 물체의 depth를 잘 판단한다고 결론을 지었다.