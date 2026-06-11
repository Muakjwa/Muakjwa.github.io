---
title: LG AI 연구원 Internship
author: Sunwoo Yu
date: 2026-05-15 14:10:00 +0900
categories: [Intership]
tags: [Review, Bio AI, Internship]
render_with_liquid: false
image: /assets/img/post/LG_AI_Research/certificate.jpg
---

## Introduction
취업과 대학원을 고민하던 사이, LG AI 연구원 Bio Intelligence Lab에 ML Engineer로 인턴십의 기회가 생겼다.
Life-Log dataset을 다루는 AI 대회에서 수상하고, 창업을 하며 수면다원검사-radar pair dataset을 구축한 경험을 거치며 Bio domain dataset을 더 깊게 다뤄보고 싶다는 생각이 있었고, 10개월간 인턴십에 참여하게 되었다.

처음으로 기업에서 인턴으로 생활하며 많은 것을 배웠고, 앞으로 어떤 방향으로 나아가야 할지에 대해서도 큰 도움을 받았다.
이 글에서는 회사에서 수행한 task들을 정리하고, 배우고 느낀 점을 회고하고자 한다.


## What I Did
### Training-Evaluation Automation Pipeline
2025년 7월, Foundation Model Squad에 합류했다.
ML Engineer로서 처음 담당한 task는 EXAONE Path 개발을 위한 모델 학습-평가 자동화 파이프라인 구축이었다.
EXAONE Path는 giga-pixel 크기의 병리학 이미지인 whole slide image(WSI)를 다루는 Foundation Model(FM)이다.
데이터 특성상 patch-level FM의 output을 slide-level FM이 aggregate하고, 이를 바탕으로 downstream task evaluation을 수행하는 구조를 가지며, 세 단계 각각이 개별 학습을 필요로 하면서 서로 종속적인 관계에 있다.

자동화 이전에는 각 stage의 학습이 끝날 때마다 사람이 결과를 확인해 best checkpoint를 선별하고, 이를 다음 stage에 수동으로 연결해야 했다.
단계 사이마다 대기와 개입이 발생하는 구조였기에, daemon process가 전체 파이프라인을 관리하며 stage별 최적 checkpoint를 자동으로 선택해 다음 stage로 이어주는 framework를 설계하고 구현했다.
그 결과 실험 설정만 정의하면 사람의 개입 없이 patch-level 학습부터 downstream evaluation까지 end-to-end로 실험이 이어지고, 야간이나 주말에도 실험이 끊기지 않으며, checkpoint 선별 기준이 코드로 정의되어 반복 실험의 재현성을 확보할 수 있었다.

### EXAONE Path V2.5
이후 EXAONE Path V2.5 개발에 참여했다.
나는 모델의 성능을 입증하고 검증하는 evaluation·analysis·benchmark 체계 구축을 담당했다.
EXAONE Path V2.5를 발표할 때 기존 모델들과 공정하게 비교하기 위해, public dataset 기반의 patho-bench 방식으로 개발 모델과 기존 모델들을 동일 선상에서 평가했다.
또한 내부적으로 구축한 dataset을 활용해 public benchmark가 다루지 못하는 out-of-distribution case에 대한 평가까지 수행했다.
이 기여를 통해 EXAONE Path V2.5의 <a href = "arxiv.org/abs/2512.14019"> Technical Report </a>에 2저자로 이름을 올릴 수 있었다.
또한 LG에서 진행하는 <a href = "event.lgresearch.ai/"> LG AI Insight </a> 행사에서 "EXAONE Path 2.5: Pathology Foundation Model with Multi-Omics Alignment"라는 제목으로 포스터 세션 발표도 경험했다.

<div style="display: flex; justify-content: space-around;">
    <img src="/assets/img/post/LG_AI_Research/exaonepathv25.gif" alt="EXAONE Path V2.5" width="400"/>
    <img src="/assets/img/post/LG_AI_Research/LG_AI_Insight.jpg" alt="LG AI Insight" width="400"/>
</div>

### Bulk RNA-seq Foundation Model
이후에는 Bulk RNA-seq Foundation Model 개발에 참여했다.
해당 연구는 현재 **Nature Communications**에 **under review** 중이며, 게재 이후 이 글에 상세한 내용을 업데이트할 예정이다.


## Closing
대학교, 연구실, 창업처럼 학생 신분으로 다양한 경험을 해보았지만, 기업에서 10개월간 사회생활과 회사 업무를 수행해본 것은 처음이었다.
훌륭한 분들이 모인 연구원이었기에, 논리적인 사고 과정과 더 큰 틀을 보는 시야를 강화할 수 있었다.

모델 하나를 발표하기까지 평가의 공정성을 집요하게 따지는 과정, 실험 하나를 설계할 때도 그 결과가 어떤 주장을 뒷받침할 수 있는지부터 논의하는 문화 속에서, 좋은 연구와 좋은 엔지니어링이 어떻게 만나는지를 가까이서 배웠다.
이전부터 가진 생각이지만, 어떤 사람들과 함께하는지가 가장 중요한 요소인 것 같다.
덕분에 LG AI 연구원에서의 인턴 생활도 많은 분들의 도움과 사랑을 받으며 감사히 마무리할 수 있었다.

<div style="display: flex; justify-content: space-around;">
    <img src="/assets/img/post/LG_AI_Research/certificate.jpg" alt="certificate" width="400"/>
    <img src="/assets/img/post/LG_AI_Research/team_picture.jpg" alt="FM tech cell" width="400"/>
</div>