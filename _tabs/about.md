---
# the default layout is 'page'
icon: fas fa-info-circle
order: 1
---


<style>
    @page {
    size: letter;
    margin: 0.5in;
    }

    /* You can poke around this CSS if you want to customize your formatting / styling further */
    /* You can even import custom fonts! */

    /* fonts */
    /* @import url('https://fonts.googleapis.com/css2?family=Inter:wght@500;600;700&display=swap'); */
    @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

    /* meta */
    .bodies {
        font-family: Calibri, sans-serif;
        /* font-family: 'Calibri'; */
        font-size:  14px;
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
        content: counter(list-item) "."; /* 숫자 뒤에 공백 추가 */
    }

    .li {
        padding-left: 1em;
        text-indent: -2em;
    }
</style>

<body class = "bodies">
    <h1 class = 'title'>
        Sunwoo Yu 
    </h1> 
    <div class="info">
        <div class="text">
            School of Undergraduate Studies, College of Transdisciplinary studies <br>
            Daegu Gyeongbuk Institute of Science and Technology (DGIST)
        </div>
        <!-- <a class="download" href="https://github.com/Muakjwa/Muakjwa.github.io/blob/main/_tabs/about.pdf" download = "sunwoo's_CV">Download</a> -->
    </div>
    <h2 class = 'sub_title'>
        Research Interest
    </h2>
    <h3 class = 'h3_content'>
        &emsp; - Deep Learning <br>
        &emsp; - Representation Learning <br>
        &emsp; - Efficient Data Compression
    </h3>
    <br>
    <h2 class = 'sub_title'>
        Personal Data
    </h2>
    <div>
        <span class = "border">Phone</span> &emsp; &emsp; &emsp; &emsp; +82-10-5762-2205
        <br>
        <span class = "border">E-mail</span> &emsp; &emsp; &emsp; &emsp; ysw0920@dgist.ac.kr
        <br>
        <span class = "border">Major </span> &emsp; &emsp; &emsp; &emsp; Computer Science
        <br>
        <span class = "border">GPA </span> &emsp; &emsp; &emsp; &emsp; &emsp;3.98/4.3 
        &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp;
        <span class = "border">Major GPA </span> &emsp; &emsp; &emsp; 4.18/4.3
    </div><br>
    <h2 class = 'sub_title'>
    Education
    </h2>
    <h3 class = 'h3_content'>
    Daegu Gyeongbuk Institute of Science and Technology (DGIST) <span class="spacer"></span> Mar.2020 &mdash; Present
    </h3>
    <p class = "small">
    School of Undergraduate Studies, College of Transdisciplinary studies <br>
    <i>
    Bachelor Student
    </i>
    </p>
    <br>
    <h3 class = 'h3_content'>
    University of California, Los Angeles (UCLA) <span class="spacer"></span> Jun.2023 &mdash; Aug.2023
    </h3>
    <p class = "small">
    <i>
    Exchange Program
    </i> 
    </p>
    <br>
    <h2 class = 'sub_title'>
    Publications
    </h2>
    <div class = "middle indent">
        * Equal contributor <br> 
    </div>
    <div>
        <ol reversed start="2" class ="ol">
            <li class = "middle li">
                &emsp;Daewon Kim, <ins><b>Sunwoo Yu</b></ins>, Jaehyeon Lee and Seonghun Lee, “Development of a Driver Monitoring System Using the Capacitive Steering Wheel and FMCW Radar”, The Korean Institute of Communications and Information Sciences (KICS) Conference (Fall), Nov. <b>2024</b>. (Expected)
            </li>
            <li class = "middle li">
                &emsp;Jaehyeon Lee*, <ins><b>Sunwoo Yu</b></ins>*, Daewon Kim, and Kiwon Choi, “Multi-patching: life-log Classification with the Reconstructed Representation of Multivariate Time Series”, The 15th International Conference on ICT Convergence (ICTC 2024), pp. 798-803, Oct. <b>2024</b>.
            </li>
        </ol>
    </div>
    <br>
    <h2 class = 'sub_title'>
    Research Experience
    </h2>
    <div>
        <h3 class = 'h3_content'>
            • Undergraduate Group Research Program (UGRP) <span class="spacer"></span> Feb.2024 &mdash; Dec.2024
        </h3>
        &emsp; at Department of Brain Sciences, DGIST <br>
        &emsp; ( Prof. Hankyoung Choe, DGIST ABC-DGIST)
        <br>
        &ensp; <b>✓ Design of a radar dataset collection system</b> for subjects’ sleep in polysomnography experiments <br>
        &ensp; <b>✓ predicting Heart/Respiratory Rate with radar data & predicting sleep stage using representation from HR/RR</b>
    </div>
    <br>
    <div>
        <h3 class = 'h3_content'>
        • Undergraduate Research Assistant <span class="spacer"></span> Sep.2023 &mdash; Nov.2024
        </h3>
        &emsp; at Department of Electrical Engineering & Computer Science, DGIST <br> 
        &emsp; ( Prof. Hoonsung Chwa, DGIST RTCL)
        <br>
        &ensp; <b>✓ PyTorch Camp</b> : Learning how to use pytorch by implementing below paper <br> 
        &emsp; (LaLaRAND: Flexible Layer-by-Layer CPU/GPU Scheduling for Real-Time DNN Tasks) <br> 
        &ensp; <b>✓ Project</b> : Real-Time streaming system using foveated rendering <br> 
        &ensp; <b>✓ Experience of editing PyTorch & OpenCV source code</b>
    </div>
    <br>
    <h2 class = 'sub_title'>
    Awards and Honors
    </h2>
    <div>
        <h3 class = 'h3_content'>
        KFAS 人才林 Scholarship <span class="spacer"></span> Feb.2025 &mdash; Feb.2026
        </h3>
        <h3 class = 'h3_content'>
        Encouragement Prize, The World Embedded Software Contest 2024, KESSIA <span class="spacer"></span> Nov.2024
        </h3>
        <h3 class = 'h3_content'>
        Encouragement Prize, Human Understanding AI Paper Challenge 2024, ETRI <span class="spacer"></span> Oct.2024
        </h3>
        - Director of ETRI(Electronics and Telecommunications Research Institute) Award
        <h3 class = 'h3_content'>
        Academic Excellence Award (DGIST) <span class="spacer"></span> Spring Semester, 2024
        </h3>
        <h3 class = 'h3_content'>
        Academic Excellence Award (DGIST) <span class="spacer"></span> Fall Semester, 2023
        </h3>
        <h3 class = 'h3_content'>
        Academic Excellence Award (DGIST) <span class="spacer"></span> Spring Semester, 2023
        </h3>
    </div>
    <br>
    <h2 class = 'sub_title'>
    Skills
    </h2>
    <div>
        <h3 class = 'h3_content'>
        TEPS: &emsp;&emsp;&ensp; 336/600 <span class="spacer"></span> valid : Feb.2025 &mdash; Feb.2027
        </h3>
        <h3 class = 'h3_content'>
        Language: &emsp; Python, C/C++
        </h3>
        <h3 class = 'h3_content'>
        Tools: &emsp;&emsp;&emsp;Git, Docker, PyTorch, OpenAI Gym, ModusToolBox
        </h3>
    </div>
    <br>
</body>