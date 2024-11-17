---
title: Depth Foveated Compression Review
author: Sunwoo Yu
date: 2024-11-16 14:10:00 +0800
categories: [Project]
tags: [Review, Project, Research, Paper]
render_with_liquid: false
---

## Introduction
2023년 2학기, DGIST 좌훈승 교수님 연구실에서 학부생 연구원을 시작하게 되었다.

RTCL(Real Time Computing Lab)으로 컴퓨터 시스템에서 실시간과 관련된 광범위한 분야를 다루는 연구실이다.

학부생 연구원 기간동안 main project로 진행한 depth foveated compression에 대한 정리를 한다.
<br>

학부생 연구원을 시작하며, 앞으로 진행할 연구 주제를 찾아보게 되었다. <br>
랩미팅 과정에서 AR/VR 기술에서도 실시간처리가 중요하다는 사실을 알게 되었고, <br>
'AR/VR에서 어떻게 실시간 처리를 적용할 수 있을까?' 를 고민해보게 되었다.

학교 강의를 듣던 중, 앞에 앉아 있는 학생의 뒤통수를 보니 칠판의 판서를 읽을 수 없었다. <br>
초점을 맞춘 위치에서 멀어진 곳은, 사람이 제대로 인식할 수 없는 것이였다.

이러한 인간의 시력 모델을 AR/VR에 적용하면 더 빠른 속도를 낼 수 있을 것이라 생각하였다. <br>
이 현상을 바로 찾아보았는데 해당 내용은 Foveated Rendering이라 불리며, 이미 Meta의 Quest라는 모델에도 사용중인 기술이였다.

하지만 교수님에게 초점을 둘 때와, 바로 앞의 학생에 초점을 둘 때, 칠판의 판서의 흐릿함이 다르게 느껴졌다. <br>

실제 사람의 시력모델은 초점에서 상하좌우로 멀어질수록 흐릿하게 느끼지만, <br>
보고 있는 곳의 depth의 차이도 흐릿하게 느끼는데에 영향을 준다는 사실을 알 수 있었다.

## Related Works


## Method
기존의 Foveated Rendering은 2D 화면에서의 Rendering 효율을 높이기 위해 사용되는 기술이었지만, <br>
이제는 AR/VR을 사용하고, 여기서는 depth 정보도 중요한 정보로 활용될 수 있다.

AR/VR 기기에서 사용되는 영상은 Rendering 연산량이 많아 high-quality rendering은 cloud환경에서 진행될 수 있다. <br>
이렇게 rendering된 화면을 띄우기 위해서는 network 환경이 중요하고, 이 network 맞춰서 영상을 compress할 수 있다.

이미지를 압축하기 위해서 여러 방식을 적용할 수 있지만, <br>
일반적으로 이미지 압축에 사용되는 jpeg의 과정을 일부 수정하여 이 현상을 적용할 수 있었다.

jpeg의 encoding 과정 중, quantization 과정이 이미지의 압축률에 크게 관여한다.

이 quantization 과정에서 low pass filter를 통해 compression level을 결정하도록 정의하였다.

이러한 process를 구현하기 위해 opencv source code를 분석하여, jpeg encoding 과정을 수정할 수 있었다.

quantization level을 일반적인 level이 아니라 user의 초점에 따라 block마다 다른 level로 적용할 수 있었다. <br>
이를 위해 depth map이 같이 담겨있는 NYU Dataset을 사용해 test를 해보았다.


## Result
위의 방식으로 구현한 결과, 아래와 같이 depth에 따른 compression정도를 control knob으로 사용한 결과이다.

![Compression Result]( /assets/img/post/depth_foveated_compression/data_size_comparison.png ){: width="500"}

아래에는 원본 이미지와 depth parameter 500으로 적용한 이미지를 첨부한다. <br>
해당 이미지 가운데에 초점이 맞춰진 채 depth & foveated 압축되어, 47.2%의 압축률로 압축되었다.

<div style="display: flex; justify-content: space-around;">
    <img src="/assets/img/post/depth_foveated_compression/original_1448.jpg" alt="Original Image" width="400"/>
    <img src="/assets/img/post/depth_foveated_compression/DF_a500_1448.jpg" alt="Depth Foveated Compressed Image" width="400"/>
</div>

추가 이미지와 코드는 아래 링크에서 확인할 수 있다.
<a href = "https://github.com/Muakjwa/Depth_Foveated_Rendering"> Github Link </a>