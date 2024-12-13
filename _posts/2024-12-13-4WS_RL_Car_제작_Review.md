---
title: 4WS RL Car 제작 Review
author: Sunwoo Yu
date: 2024-12-13 14:10:00 +0800
categories: [Project]
tags: [Review, Project]
render_with_liquid: false
image: /assets/img/post/4WS_RL/simulation.gif
---

## Introduction
2024년 2학기, 공학적 설계라는 수업을 들었다.

해당 수업은 1학기동안 자율주행 자동차를 만드는 수업이다.

이 수업을 시작하고, 같은 팀원과 주제에 대해 생각해보았다.

기계트랙 과목이지만 팀원중 2명이 컴퓨터공학 학생이었기 때문에 그 특성을 잘 살릴 수 있는 주제로 설정하였다.

물론, hardware적인 독창성도 챙기기 위해서 다음과 같은 주제를 선정하였다.<br>
4개의 독립적인 wheel을 사용한 강화학습 기반 자율주행

일반적으로 4wheel steering을 사용하면 주행의 자율성이 더 광범위해진다.

이 광범위해진 주행을 일반적인 차량에서 사람이 4개의 wheel을 조작하며 주행할 수는 없다.

이러한 4wheel steering을 이용해서 더 효율적이고, 강력한 주행능력을 가진 차량을 만들기 위해 강화학습을 적용하게 되었다.

## Development
### Hardware
Hardware는 기계트랙을 전공하는 팀원이 주도해서 제작하였다.

4개의 독립적인 wheel을 작동시키기 위해 각각의 wheel에 명령을 내려줄 수 있는 teensy를 부여했다.

강화학습 모델에 적용될 input을 위한 camera data processing과 강화학습 모델을 이용한 action 결정을 위해 2개의 Raspberry Pi를 부착하였다.

또한 각 motor의 전원을 제어하기 위해서 12V 배터리를 step-down converter를 사용해 7V로 낮춘다음, 각 모터에 5V를 할당해주었다.

그로써 설계한 3D모델과 실제 차량의 모습은 아래와 같다.

<div style="display: flex; justify-content: space-around;">
    <img src="/assets/img/post/4WS_RL/car_3d.png" alt="3D Model" width="400"/>
    <img src="/assets/img/post/4WS_RL/car_total.png" alt="Implemented Car" width="400"/>
</div>

이 차량에서 특징적으로 취할 수 있는 action은 크게 3가지가 있다.<br>
1. Straight Mode
2. Diagonal Mode
3. Zero Turn Mode
<div style="display: flex; justify-content: space-around;">
    <img src="/assets/img/post/4WS_RL/straight_mode.gif" alt="Straight Mode" width="270"/>
    <img src="/assets/img/post/4WS_RL/diagonal_mode.gif" alt="Diagonal Mode" width="270"/>
    <img src="/assets/img/post/4WS_RL/zero_turn_mode.gif" alt="Zero Turn Mode" width="270"/>
</div>

### Software
차량을 자율주행시키기 위해서 주변 환경을 인지한 이후, 해당 환경에서 필요한 action을 결정해야한다.<br>
여기서 Action을 결정하기 위한 model로 우리는 강화학습 모델을 선택했다.

처음에는 3D model을 바로 강화학습에 적용시키는 방안을 생각해보았지만,<br>
시간적 제약, 3D 환경의 강화학습 제작시 실제 환경과의 차이점 때문에 발생하는 차이를 극복하기 위해 2D환경에서 강화학습 model을 학습시켰다.

2D환경에서 학습시킨 simulation 영상은 이와 같다.<br>
(4Wheel Steering의 장점을 살리기 위해서 simulation부터 real world까지 실행가능한 동작을 Straight, Diagonal, Zero turn 3가지 모드로 제한하였다.)<br>
![Simulation of 4WS RL Car]( /assets/img/post/4WS_RL/simulation.gif ){: .w-100}

이 model의 input으로는 차량으로부터 좌, 우, 대각선 좌, 대각선 우의 방향으로 차선까지의 거리를 준다.<br>
이 거리는 camera에서 <br>
calibration -> grayscale transform -> blurring -> Canny edge detection -> Hough Line Detection -> Distance Calculation<br>
과정을 거쳐서 얻게 된다.

얻어진 distance data는 RL model의 input으로 들어가 차량을 작동시킨다.


## Result
실제 환경에서 구동 영상은 아래와 같다.

![Real World Driving of 4WS RL Car]( /assets/img/post/4WS_RL/self_driving.mp4 ){: .w-70}

실제로 실패도 한번씩 하게 되지만, 그 외의 상황에서는 상당히 차선을 따라서 잘 주행하는 모습을 볼 수 있다.

이와 같이 실제로 차선을 인식하여 자율주행이 가능한 모델과 차량을 제작해보았으며,<br>
결론적으로 공학적 설계 과목에서 수여하는 A1 Championship in 2024 대회에서 performance prize를 수상하였다.<br>
(performance prize와 design prize 중 performance prize 수상)

<div style="display: flex; justify-content: space-around;">
    <img src="/assets/img/post/4WS_RL/car_with_prize.jpg" alt="Car with Prize (performance)" width="400"/>
    <img src="/assets/img/post/4WS_RL/performance_prize.jpg" alt="A1 Championship Performance Prize" width="400"/>
</div>
