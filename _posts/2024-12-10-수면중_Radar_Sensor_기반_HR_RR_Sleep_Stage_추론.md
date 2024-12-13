---
title: 수면중 RADAR Sensor 기반 HR, RR, Sleep Stage 추론
author: Sunwoo Yu
date: 2024-12-10 14:10:00 +0800
categories: [UGRP]
tags: [Review, UGRP, Research]
render_with_liquid: false
image: /assets/img/post/radar_sensor/flow.png
---

## Introduction

2024년도를 시작하면서, 창업을 시작하게 되었다.
창업 아이템은 수면에 도움이 되는 디퓨저를 만드는 것이다.

실제로 향이 수면에 영향을 끼친다는 다양한 연구가 있었고, 
이를 바탕으로 특정 향이 수면에 어떻게 영향을 끼치는지를 연구해 상품화하는 것이 목적이였다.

사용자의 수면상태에 실시간으로 반응하여 향을 전달하기 위해서는 수면 상태를 실시간으로 확인할 수 있는 기술이 필요했다.

1. 심전도 기술<br>
  첫번째로 찾아본 기술은 심전도 기술이다. <br>
  일반적으로 스마트워치에 많이 사용되는 기술로 접촉식 측정이 가능하며 성능이 높다.

2. 비접촉식 적외선 가스 영상 카메라<br>
  사람의 호흡과정을 적외선 가스 영상으로 확인할 수 있는 카메라이다.<br>
  이 기술은 비접촉식 측정이 가능하지만, 이제 개발되고 있는 기술로 천문학적인 가격을 갖고 있다.

3. FMCW 레이더<br>
  일반적으로 고주파 전파를 전달하는 방식으로 흉곽의 움직임을 판단해 심박과 호흡을 판단할 수 있다.<br>
  가격이 저렴하지만 레이더 센서에 대한 높은 이해와 활용력이 바탕되어야 한다.

위와 같은 기술들의 장단점을 고려하였을 때, <br>
사용자가 불편함을 느낄 수 있는 접촉식 방식과 가격적 측면을 고려하니 radar 센서를 사용하게 되었다.

## Development
레이더 기술을 사용하기 위해서 레이더로는 infineon의 BGT60TR13C 모델을 사용하였다.

실제로 레이더 센서를 바탕으로 수면 단계를 파악하기 위해서는 dataset이 필요했다.

이 데이터셋은 수면이 이뤄질 때의 data를 의미하며, 이에 맞는 정확한 HR(심박), RR(호흡), Sleep stage label이 필요했다.

### Data
radar의 paraemter에 따라 data의 값이 달라지고,<br>
실제 수면상의 data이다 보니 dataset을 수집하는 것이 유일한 방법이였다.

dataset을 수집하기 위해서 창업을 진행하는 팀에서 수면다원검사센터와 협약을 맺었으며,<br>
실제 수면이 진행될 때, radar를 설치하여 radar dataset과 정확한 HR, RR, Sleep stage label을 동시에 얻을 수 있었다.

실험 환경은 아래와 같이 구성되었다.

<div style="display: flex; justify-content: space-around;">
    <img src="/assets/img/post/radar_sensor/radar_pos_fig.png" alt="expected environment" width="400"/>
    <img src="/assets/img/post/radar_sensor/radar_pos.png" alt="actual environment" width="400"/>
</div>


### Model
Radar를 통해 수집한 data를 바탕으로 심박, 호흡, 수면 stage를 판단할 수 있다.

이를 위해서 가장 기본적인 방식으로는 신호처리 기법을 사용해서 분석하는 것이다.

하지만 최근 AI가 발전하다보니 data를 바탕으로 신호처리 기법으로 의미 있는 부분을 추출한 후,<br>
해당 부분을 deep learning을 사용하여 분석할 수 있었다.

이를 위해서 신호처리 기법으로 아래와 같은 flow를 통해 처리하였으며,<br>
처리된 data를 ResNet를 이용해 심박, 호흡을 판단하고,<br>
해당 ResNet에서 추출된 feature를 GRU에 넣어 수면 stage를 판단할 수 있는 모델을 구성하였다.

![Preprocessing & AI Model]( /assets/img/post/radar_sensor/flow.png ){: .w-70}

이 과정중 preprocessing을 마친 데이터를 시각화하면 아래와 같다.

![Visualization of preprocessed data]( /assets/img/post/radar_sensor/radar_graph.gif ){: .w-70}

## Result
결론적으로 preprocessing과 ResNet을 처리하면 아래와 같이 심박수와 호흡수의 예측이 가능했다.

<div style="display: flex; justify-content: space-around;">
    <img src="/assets/img/post/radar_sensor/heartrate.png" alt="HeartRate" width="400"/>
    <img src="/assets/img/post/radar_sensor/respiratoryrate.png" alt="RespiratoryRate" width="400"/>
</div>

하지만 sleep stage를 판단한 결과,<br>
잠에 들었는지 안들었는지는 90%이상의 정확도로 예측함을 확인했지만,<br>
sleep stage를 판단하는 일에 있어서 정확도가 낮게 나옴을 알 수 있었다.

이 낮은 정확도는 심박수와 호흡수를 판단하는 과정에서부터 부족한 feature extraction 때문이라라 예상된다.

다음에 이 과제를 다시 수행하게 된다면 preprocessing 과정에 더 초점을 맞춰서 진행해볼 것이다.