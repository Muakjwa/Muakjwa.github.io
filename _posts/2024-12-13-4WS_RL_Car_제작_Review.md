---
title: 4WS RL Car 제작 Review
author: Sunwoo Yu
date: 2024-12-13 14:10:00 +0900
categories: [Project]
tags: [Review, Project]
render_with_liquid: false
image: /assets/img/post/4WS_RL/simulation.gif
---

## Introduction
2024년 2학기, 공학적 설계라는 수업을 들었다.
해당 수업은 한 학기 동안 자율주행 자동차를 만드는 수업이다.
이 수업을 시작하고, 같은 팀원과 주제에 대해 생각해보았다.
기계트랙 과목이지만 팀원 중 2명이 컴퓨터공학 학생이었기 때문에 그 특성을 잘 살릴 수 있는 주제로 설정하였다.
물론, hardware적인 독창성도 챙기기 위해서 다음과 같은 주제를 선정하였다.
**4개의 독립적인 wheel을 사용한 강화학습 기반 자율주행**

일반적으로 4wheel steering을 사용하면 주행의 자율성이 더 광범위해진다.
이 광범위해진 주행을 일반적인 차량에서 사람이 4개의 wheel을 조작하며 주행할 수는 없다.
이러한 4wheel steering을 이용해서 더 효율적이고, 강력한 주행능력을 가진 차량을 만들기 위해 강화학습을 적용하게 되었다.
팀은 총 3명으로, 기계트랙 팀원이 하드웨어 제작을 주도하였고, 나는 강화학습 모델과 학습 환경을, 다른 컴공 팀원이 vision 처리를 담당하였다.


## Development
전체 시스템은 인지(Vision) → 의사결정(RL) → 제어(Action Control)의 흐름으로 구성된다.
1. 차량 전방의 4개 카메라로 주변을 촬영해 Bird's Eye View(BEV)를 생성하고, 차선·장애물까지의 거리를 계산한다. (Vision Perception)
2. 이 거리값들을 입력으로 받아 PPO 기반 강화학습 모델이 다음 action을 결정한다. (RL Model Decision)
3. 결정된 action을 4개 wheel의 Teensy로 전달해 실제 모터를 구동한다. (Action Control)
연산을 분산하기 위해 Raspberry Pi 2대를 역할별로 나누고, 고정 IP 기반 이더넷으로 연결했다. 한 대는 환경 인지를, 다른 한 대는 action 결정을 전담한다.

### Hardware
Hardware는 기계트랙을 전공하는 팀원이 주도해서 제작하였다.
4개의 독립적인 wheel을 작동시키기 위해 각각의 wheel에 명령을 내려줄 수 있는 teensy를 부여했다.
강화학습 모델에 적용될 input을 위한 camera data processing과 강화학습 모델을 이용한 action 결정을 위해 2개의 Raspberry Pi를 부착하였다.
이때 2개의 Raspberry Pi는 역할을 나누어, 한 대는 카메라로 환경을 인지하는 역할을, 다른 한 대는 강화학습 모델로 action을 결정하는 역할을 맡았고, 두 Pi는 이더넷으로 연결되어 통신하였다.
또한 각 motor의 전원을 제어하기 위해서 12V 배터리를 step-down converter를 사용해 7V로 낮춘다음, 각 모터에 5V를 할당해주었다.
그로써 설계한 3D모델과 실제 차량의 모습은 아래와 같다

<div style="display: flex; justify-content: space-around;">
    <img src="/assets/img/post/4WS_RL/car_3d.png" alt="3D Model" width="400"/>
    <img src="/assets/img/post/4WS_RL/car_total.png" alt="Implemented Car" width="400"/>
</div>

이 차량이 취할 수 있는 특징적인 action은 크게 3가지다.<br>
1. Straight Mode
2. Diagonal Mode
3. Zero Turn Mode
<div style="display: flex; justify-content: space-around;">
    <img src="/assets/img/post/4WS_RL/straight_mode.gif" alt="Straight Mode" width="270"/>
    <img src="/assets/img/post/4WS_RL/diagonal_mode.gif" alt="Diagonal Mode" width="270"/>
    <img src="/assets/img/post/4WS_RL/zero_turn_mode.gif" alt="Zero Turn Mode" width="270"/>
</div>

### Reinforcement Learning
차량을 자율주행시키기 위해서 주변 환경을 인지한 이후, 해당 환경에서 필요한 action을 결정해야 한다.
여기서 Action을 결정하기 위한 model로 우리는 강화학습 모델을 선택했고, 알고리즘으로는 PPO를 사용하였다.

처음에는 3D model을 바로 강화학습에 적용시키는 방안을 생각해보았지만,
시간적 제약, 3D 환경의 강화학습 제작시 실제 환경과의 차이점 때문에 발생하는 차이를 극복하기 위해 2D환경에서 강화학습 model을 학습시켰다.
2D환경에서 학습시킨 simulation 영상은 이와 같다.
(4Wheel Steering의 장점을 살리기 위해서 simulation부터 real world까지 실행가능한 동작을 Straight, Diagonal, Zero turn 3가지 모드로 제한하였다.)
![Simulation of 4WS RL Car]( /assets/img/post/4WS_RL/simulation.gif ){: .w-100}

이 model의 input으로는 차량으로부터 좌, 우, 대각선 좌, 대각선 우의 방향으로 차선까지의 거리를 준다.
이 거리는 camera에서 처리한 영상으로부터 얻게 되며, 얻어진 distance data는 RL model의 input으로 들어가 차량을 작동시킨다. 
<br>
calibration -> grayscale transform -> blurring -> Canny edge detection -> Hough Line Detection -> Distance Calculation<br>
과정을 거쳐서 얻게 된다.


### 문제 해결 과정
강화학습 model을 만드는 과정은 사실 마주친 문제를 하나씩 풀어가는 과정이었다.
먼저 알고리즘과 카메라(observation) 수를 정하기 위해, DDQN과 PPO를 두고 observation 수를 바꿔가며 어떤 조합이 가장 안정적으로 완주하는지 비교 실험을 진행했다.

카메라가 많을수록 환경을 더 정확히 인지할 수 있지만, 그만큼 연산 부하와 Raspberry Pi 메모리 부담이 커지는 trade-off가 있었다. 이를 고려해 카메라 4대 구성을 절충안으로 선택하였다.

다음으로 마주한 문제는 학습된 에이전트가 Zero Turn(제자리 회전)에 시간을 지나치게 많이 쓴다는 점이었다.
원인은 reward에 있었다. 모든 동작에 동일한 시간 페널티를 주다 보니 회전을 남발해도 손해가 크지 않았던 것이다. 그래서 회전 동작에만 더 큰 시간 페널티를 주도록 reward를 다시 설계했고, 이후 불필요한 회전이 줄어 더 효율적인 경로를 학습하게 되었다.

마지막으로 가장 까다로웠던 것은 simulation과 real world의 차이였다.
simulation에서는 아주 가까운 차선까지 인식되었지만 실제 카메라는 너무 가까운 차선을 잡지 못했다. 이를 극복하기 위해 model의 input을 raw 이미지가 아닌 '차선까지의 거리'로 추상화하고, 실제로 차선을 인식하지 못하는 상황을 일정한 값으로 통일해 처리했다. simulation 환경도 같은 기준으로 맞춰주어, simulation에서 학습한 정책을 실제 차량에 그대로 옮길 수 있었다.


## Result
실제 환경에서 구동 영상은 아래와 같다.

![Real World Driving of 4WS RL Car]( /assets/img/post/4WS_RL/self_driving.mp4 ){: width="300"}

실제로 실패도 한번씩 하게 되지만, 그 외의 상황에서는 상당히 차선을 따라서 잘 주행하는 모습을 볼 수 있다.

이와 같이 실제로 차선을 인식하여 자율주행이 가능한 모델과 차량을 제작해보았으며,<br>
결론적으로 공학적 설계 과목에서 수여하는 A1 Championship in 2024 대회에서 performance prize를 수상하였다.<br>
(performance prize와 design prize 중 performance prize 수상)

<div style="display: flex; justify-content: space-around;">
    <img src="/assets/img/post/4WS_RL/car_with_prize.jpg" alt="Car with Prize (performance)" width="400"/>
    <img src="/assets/img/post/4WS_RL/performance_prize.jpg" alt="A1 Championship Performance Prize" width="400"/>
</div>


## Closing
강화학습을 실제 하드웨어 위에서 동작시키는 전 과정을 직접 겪어본 첫 프로젝트였다.
알고리즘을 고르고, reward를 다듬고, simulation과 현실의 차이를 메우는 과정을 거치며, 강화학습을 단순히 학습시키는 것이 아니라 문제를 푸는 도구로 다뤄봤다는 점이 가장 크게 남았다.
물론 아쉬운 점도 있었다. 차량 무게 탓에 속도가 충분히 나지 않았고, 학습에는 세 가지 모드를 모두 사용했지만 실제 주행에서는 일부 모드에 치우치는 경향이 있었다. 더 정교한 simulation과 reward 설계로 풀어볼 수 있는 과제로, 다음 프로젝트의 숙제로 남겨두었다.

코드는 아래 링크에서 확인할 수 있다.
<a href = "https://github.com/Muakjwa/4WS_RLCar"> Github Link </a>
