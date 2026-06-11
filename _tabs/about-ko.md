---
# the default layout is 'page'
title: About KR
icon: fas fa-info-circle
order: 5
---

<style>
    @page {
    size: letter;
    margin: 0.5in;
    }

    .bodies {
        font-family: 'Malgun Gothic', '맑은 고딕', 'Apple SD Gothic Neo', Calibri, sans-serif;
        font-size: 14px;
    }

    .download {
        text-align: right;
        font-size: 10px;
        margin: 0;
        padding: 0;
    }

    .spacer {
        margin: 0px auto;
    }

    .border {
        font-size: 15px;
        font-weight: bold;
        line-height: 150%;
    }

    .small {
        font-size: 12px;
        line-height: 100%;
    }

    .middle {
        font-size: 15px;
        line-height: 120%;
    }

    .title {
        border-bottom: 1px solid #ffffff;
        color: black;
        text-align: center;
        font-size: 28px;
        font-weight : bold;
        line-height: 150%;
        margin: 0;
        padding: 0;
    }

    .sub_title {
        border-bottom: 1px solid #000000;
        text-transform: uppercase;
        font-weight : bold;
        font-size: 16px;
        margin: 10px 0px;
        padding: 0;
    }

    .h3_content{
        display: flex;
        font-weight : bold;
        font-size: 15px;
        margin: 6px 0px;
        line-height: 150%;
    }

    p {
        margin: 0;
        padding: 0;
    }

    .paper {
        text-indent: 100px;
    }

    .info {
        text-align: center;
        display: flex;
        line-height: 100%;
        justify-content: space-between;
        align-items: center;
    }

    .info .text {
        flex: 1;
        text-align: center;
    }

    .info .download {
        text-align: right;
    }

    .indent {
        text-indent: 1em;
    }

    .ol {
        list-style-position: inside;
    }

    .li::marker {
        content: counter(list-item) ".";
    }

    .li {
        padding-left: 1em;
        text-indent: -2em;
    }
</style>

<body class = "bodies">
    <h1 class = 'title'>
        유선우
    </h1>
    <div class="info">
        <div class="text">
            대구경북과학기술원(DGIST) 융복합대학 기초학부
        </div>
    </div>
    <br>
    <h2 class = 'sub_title'>
        인적 사항
    </h2>
    <div>
        <span class = "border">전화</span> &emsp; &emsp; &emsp; &emsp; +82-10-5762-2205
        <br>
        <span class = "border">이메일</span> &emsp; &emsp; &emsp; ysw0920@dgist.ac.kr
        <br>
        <span class = "border">전공 </span> &emsp; &emsp; &emsp; &emsp; 컴퓨터공학
        <br>
        <span class = "border">평점 </span> &emsp; &emsp; &emsp; &emsp; 3.98/4.3
        &emsp; &emsp; &emsp; &emsp; &emsp; &emsp;
        <span class = "border">전공 평점 </span> &emsp; &emsp; 4.18/4.3
    </div><br>
    <h2 class = 'sub_title'>
    학력
    </h2>
    <h3 class = 'h3_content'>
    대구경북과학기술원(DGIST) <span class="spacer"></span> 2020.03 &mdash; 현재
    </h3>
    <p class = "small">
    융복합대학 기초학부 <br>
    <i>
    학사과정
    </i>
    </p>
    <br>
    <h3 class = 'h3_content'>
    University of California, Los Angeles (UCLA) <span class="spacer"></span> 2023.06 &mdash; 2023.08
    </h3>
    <p class = "small">
    <i>
    교환 프로그램
    </i>
    </p>
    <br>
    <h2 class = 'sub_title'>
    경력
    </h2>
    <div>
        <h3 class = 'h3_content'>
        LG AI Research <span class="spacer"></span> 2025.07 &mdash; 2026.05
        </h3>
        &emsp; Bio Intelligence Lab, ML Engineer <br>
        &ensp; <span class="small">
        &#10003; 대규모 데이터셋(TB 규모), 평가 및 추론 파이프라인 처리
        </span>
        <h3 class = 'h3_content'>
        Neuralscent <span class="spacer"></span> 2024.03 &mdash; 2024.12
        </h3>
        &emsp; 공동창업자 <br>
        &ensp; <span class="small">
        &#10003; 레이더 기반 수면 데이터셋 구축 및 수면 단계 탐지 AI 모델 개발 <br>
        </span>
    </div>
    <br>
    <h2 class = 'sub_title'>
    논문 및 발표
    </h2>
    <div class = "middle indent">
        * 공동 제1저자 <br>
    </div>
    <div>
        <ol reversed start="4" class ="ol">
            <li class = "middle li">
                &emsp;Jong Hyun Kim, <ins><b>Sunwoo Yu</b></ins>, Soonyoung Lee, Tae Hyun Hwang, Jongseong Jang, Janghyeon Lee, “Benchmarking gene expression foundation models on bulk RNA-Seq data”, Proceedings of the American Association for Cancer Research (AACR), Abstract, 2026.04.
            </li>
            <li class = "middle li">
                &emsp;Juseung Yun, <ins><b>Sunwoo Yu</b></ins>, Sumin Ha, Jonghyun Kim, Janghyeon Lee, Jongseong Jang, Soonyoung Lee, [Technical Report] “EXAONE Path 2.5: Pathology Foundation Model with Multi-Omics Alignment”, Arxiv, 2025.12.
            </li>
            <li class = "middle li">
                &emsp;Daewon Kim, <ins><b>Sunwoo Yu</b></ins>, Jaehyeon Lee and Seonghun Lee, “Development of a Driver Monitoring System Using the Capacitive Steering Wheel and FMCW Radar”, 한국통신학회 추계종합학술발표회, 2024.11.
            </li>
            <li class = "middle li">
                &emsp;Jaehyeon Lee*, <ins><b>Sunwoo Yu</b></ins>*, Daewon Kim, and Kiwon Choi, “Multi-patching: life-log Classification with the Reconstructed Representation of Multivariate Time Series”, The 15th International Conference on ICT Convergence (ICTC 2024), pp. 798-803, 2024.10.
            </li>
        </ol>
    </div>
    <br>
    <h2 class = 'sub_title'>
    연구 경험
    </h2>
    <div>
        <h3 class = 'h3_content'>
            - 학부생 공동연구 프로그램(UGRP) <span class="spacer"></span> 2024.02 &mdash; 2024.12
        </h3>
        &emsp; DGIST 뇌과학과 <br>
        &emsp; (최한경 교수, DGIST ABC-DGIST)
        <br>
        &ensp; <b>&#10003; 수면다원검사 실험에서 피험자 수면 중 레이더 데이터셋 수집 시스템 설계</b> <br>
        &ensp; <b>&#10003; 레이더 데이터를 활용한 심박/호흡수 예측 및 HR/RR 표현 기반 수면 단계 예측</b>
    </div>
    <br>
    <div>
        <h3 class = 'h3_content'>
        - 학부연구생 <span class="spacer"></span> 2023.09 &mdash; 2024.11
        </h3>
        &emsp; DGIST 전기전자컴퓨터공학과 <br>
        &emsp; (좌훈성 교수, DGIST RTCL)
        <br>
        &ensp; <b>&#10003; PyTorch Camp</b> : 아래 논문을 구현하며 PyTorch 사용법 학습 <br>
        &emsp; (LaLaRAND: Flexible Layer-by-Layer CPU/GPU Scheduling for Real-Time DNN Tasks) <br>
        &ensp; <b>&#10003; 프로젝트</b> : Foveated rendering을 활용한 실시간 스트리밍 시스템 <br>
        &ensp; <b>&#10003; PyTorch 및 OpenCV 소스코드 수정 경험</b>
    </div>
    <br>
    <h2 class = 'sub_title'>
    수상 및 장학
    </h2>
    <div>
        <h3 class = 'h3_content'>
        한국고등교육재단 인재림 장학생 <span class="spacer"></span> 2025.02 &mdash; 2026.02
        </h3>
        <h3 class = 'h3_content'>
        제22회 임베디드 소프트웨어 경진대회 장려상, KESSIA <span class="spacer"></span> 2024.11
        </h3>
        <h3 class = 'h3_content'>
        휴먼이해 인공지능 논문경진대회 2024 장려상, ETRI <span class="spacer"></span> 2024.10
        </h3>
        - 한국전자통신연구원장상
        <h3 class = 'h3_content'>
        성적우수상(DGIST) <span class="spacer"></span> 2024년 봄학기
        </h3>
        <h3 class = 'h3_content'>
        성적우수상(DGIST) <span class="spacer"></span> 2023년 가을학기
        </h3>
        <h3 class = 'h3_content'>
        성적우수상(DGIST) <span class="spacer"></span> 2023년 봄학기
        </h3>
    </div>
    <br>
    <h2 class = 'sub_title'>
    기술
    </h2>
    <div>
        <h3 class = 'h3_content'>
        TEPS: &emsp;&emsp;&ensp; 336/600 <span class="spacer"></span> 유효기간 : 2025.02 &mdash; 2027.02
        </h3>
        <h3 class = 'h3_content'>
        프로그래밍 언어: &emsp; Python, C/C++
        </h3>
        <h3 class = 'h3_content'>
        도구: &emsp;&emsp;&emsp; Git, Docker, PyTorch
        </h3>
    </div>
    <br>
</body>
