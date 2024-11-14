---
# the default layout is 'page'
icon: fas fa-info-circle
order: 4
---

@page {
  size: letter;
  margin: 0.5in;
}

/* You can poke around this CSS if you want to customize your formatting / styling further */
/* You can even import custom fonts! */

/* fonts */
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@500;600;700&display=swap');

/* meta */
body {
    font-family: 'Calibri';
    font-size:  14px;
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

/* ordering of content */
h1 {
    order: 0;
}

.headerInfo {
    order: 1;
}

/* styling content */
h1, h2, h3, p, a, li {
    color: black;
}

h2 {
    margin: 10px 0px;
}

h3 {
    margin: 6px 0px;
    line-height: 120%;
}

h1 {
    color: black;
    text-align: center;
    font-size: 28px;
    margin: 0;
    padding: 0;
}

h2 {
    border-bottom: 1px solid #000000;
    text-transform: uppercase;
    font-size: 16px;
    padding: 0;
}

h3 {
    display: flex;
    font-size: 15px;
    padding: 0;
    justify-content: space-between;
}

p {
    margin: 0;
    padding: 0;
}

a {
    color: black;
}

ul {
    margin: 4px 0;
    padding-left: 24px;
    padding-right: 24px;
}

/* header info content */
.headerInfo > ul {
    display: flex;
    text-align: center;
    justify-content: center;
    margin: 6px auto 0px !important;
    padding: 0;
}

.headerInfo > ul > li {
    display: inline;
    white-space: pre;
    list-style-type: none;
}

.headerInfo > ul >li:not(:last-child) {
    margin-right: 8px;
}

.headerInfo > ul > li:not(:last-child):after {
    content: "•";
    margin-left: 8px;
}

<!--
Welcome to resume.lol !

This is the template you can use to get started.

More documentation can be found in the docs section
>>> https://resume.lol/docs
-->
@REDACTED=false
@SCHOOL = School of Undergraduate Studies, College of Transdisciplinary studies
@SCHOOL_FULL = Daegu Gyeongbuk Institute of Science and Technology (DGIST)

<!-- @NAME=My Name||Hidden Name -->
<!-- @EMAIL=ysw0920@dgist.ac.kr||fake@email.com -->
<!-- @PHONE=(123) 123-REAL||(555) 123-5555 -->
<!-- @LOCATION=Los Angeles, CA -->
<!-- @WEBSITE=mysite.com||example.com -->

# Sunwoo Yu
</br>

<div class="section headerInfo">

- School of Undergraduate Studies, College of Transdisciplinary studies 
  Daegu Gyeongbuk Institute of Science and Technology (DGIST)
<!-- - Daegu Gyeongbuk Institute of Science and Technology (DGIST) -->
<!-- - {EMAIL} -->
<!-- - {PHONE} -->
<!-- - [{WEBSITE}](https://{WEBSITE}) -->
<!-- - {LOCATION} -->

</div>

## Research Interest
### &emsp; - Deep Learning
### &emsp; - Representation Learning
### &emsp; - Efficient Data Compression

</br>

## Personal Data
<span class = "border">Phone</span> &emsp; &emsp; &emsp; &emsp; +82-10-5762-2205
</br>
<span class = "border">E-mail</span> &emsp; &emsp; &emsp; &emsp; ysw0920@dgist.ac.kr
</br>
<span class = "border">Major </span> &emsp; &emsp; &emsp; &emsp; Computer Science
</br>
<span class = "border">GPA </span> &emsp; &emsp; &emsp; &emsp; &emsp;3.98/4.3 
&emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp; &emsp;
<span class = "border">Major GPA </span> &emsp; &emsp; &emsp; 4.18/4.3
</br></br>

## Education
### Daegu Gyeongbuk Institute of Science and Technology (DGIST) <span class="spacer"></span> Mar.2020 &mdash; Present
<span class = "small">
School of Undergraduate Studies, College of Transdisciplinary studies

*Bachelor Student* 
</span>

</br>

### University of California, Los Angeles (UCLA) <span class="spacer"></span> Jun.2023 &mdash; Aug.2023
<span class = "small"> *Exchange Program*
</span>

</br>

## Publications
&emsp; \* Equal contributor
</br></br>

&emsp;<span class = "middle"> 1. &emsp;Jaehyeon Lee<sup>\*</sup>, <ins>**Sunwoo Yu**</ins> <sup>\*</sup>, Daewon Kim, and Kiwon Choi, “Multi-patching: life-log Classification 
with the 
&emsp;&emsp;&emsp;Reconstructed Representation of Multivariate Time Series”, The 15th International 
Conference on ICT 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Convergence (ICTC 2024), pp. 798-803, Oct. **2024**.</span>

</br>

## Research Experience
### • Undergraduate Group Research Program (UGRP) <span class="spacer"></span> Feb.2024 &mdash; Dec.2024
&emsp; at Department of Brain Sciences, DGIST 

&emsp; ( Prof. Hankyoung Choe, DGIST ABC-DGIST)
</br></br>

&ensp; **✓ Design of a radar dataset collection system** for subjects’ sleep in polysomnography experiments

&ensp; **✓ predicting Heart Rate/Respiratory Rate with radar data & predicting sleep stage using representation from HR/RR**

</br></br>

### • Undergraduate Research Assistant <span class="spacer"></span> Sep.2023 &mdash; Nov.2024
&emsp; at Department of Electrical Engineering & Computer Science, DGIST

&emsp; ( Prof. Hoonsung Chwa, DGIST RTCL)
</br></br>

&ensp; **✓ PyTorch Camp** : Learning how to use pytorch by implementing below paper

&emsp; (LaLaRAND: Flexible Layer-by-Layer CPU/GPU Scheduling for Real-Time DNN Tasks)

&ensp; **✓ Project** : Real-Time streaming system using foveated rendering

&ensp; **✓ Experience of editing PyTorch & OpenCV source code**


</br></br></br>

## Awards and Honors

### Encouragement Prize, The World Embedded Software Contest 2024, KESSIA <span class="spacer"></span> Nov.2024

### Encouragement Prize, Human Understanding AI Paper Challenge 2024, ETRI <span class="spacer"></span> Oct.2024
- Director of ETRI(Electronics and Telecommunications Research Institute) Award

### Academic Excellence Award (DGIST) <span class="spacer"></span> Spring Semester, 2024

### Academic Excellence Award (DGIST) <span class="spacer"></span> Fall Semester, 2023

### Academic Excellence Award (DGIST) <span class="spacer"></span> Spring Semester, 2023

</br>

## Skills

### TOEIC: &emsp;&emsp;&ensp; 810/990 <span class="spacer"></span> valid : Aug.2022 &mdash; Aug.2024
### Language: &emsp; Python, C/C++
### Tools: &emsp;&emsp;&emsp;Git, Docker, PyTorch, OpenAI Gym, ModusToolBox


> Add Markdown syntax content to file `_tabs/about.md`{: .filepath } and it will show up on this page.
{: .prompt-tip }
