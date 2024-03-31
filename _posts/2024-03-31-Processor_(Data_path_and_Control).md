---
title: Processor (Data path and Control)
author: sunwoo
date: 2024-03-31 00:00:00 +0800
categories: [Lecture, Computer Architecture]
tags: [computer science]
math: true
comments: true
image: /assets/img/post/Processor_(Data_path_and_Control)/Untitled.png
---

# Processor (Data path and Control)

프로세서의 기본적인 구현은 PC를 update하면서 PC에 해당하는 instruction을 
fetch → decode → execution 하는 과정으로 이루어져 있다.

이 과정에서 j를 제외한 instruction은 register를 읽은 이후 ALU를 사용해야 한다.

(lw, sw는 address를 계산하기 위해, add, sub는 arithmetic 연산 위해, beq, bne는 비교를 위해)

clocking method는 모든 state가 clock이 끝나는 순간 update되도록 한다.

이 과정이 일어나는 순서는 다음과 같다.

- state element 읽기 → combinational logic을 통해 value 보내기 → 
결과를 하나 이상의 state element에 작성하기 (결과 update)

- Multiplexer <br>
&emsp; 회로 상에서 2가지 선택지가 있을 때, 0, 1의 데이터로 둘 중 하나의 선택을 하게 해준다.

- Control <br>
&emsp; Mux (multiplexor)나 RegWrite, Branch, MemWrite, MemRead, ALU operation 등이 어떻게 동작할지에 대한 signald을 생성한다.

모든 instruction에 대한 hardware 구조는 다음과 같다.

![Untitled](/assets/img/post/Processor_(Data_path_and_Control)/Untitled.png)

한 번에 모든 과정을 이해하기 힘드니 각 과정을 쪼개서 살펴본다.

1. Fetching instruction

주소를 읽어 instruction memory에서 instruction을 fetch해오고, PC의 값을 +4 update한다.

(*** control signal 필요 없다 ***)

![Untitled](/assets/img/post/Processor_(Data_path_and_Control)/Untitled1.png)

2. Decoding Instruction

fetch된 instruction의 opcode와 function field bit를 control unit에 전달한다. (Decoding)

Register file에서 2개의 값을 읽는다. 
(어떤 값을 사용할지는 control signal로 결정)

![Untitled](/assets/img/post/Processor_(Data_path_and_Control)/Untitled2.png)

3. Executing R Format (add, sub, slt, and, or)

ALU에서 연산을 진행 후, register에 결과를 
저장한다.

![Untitled](/assets/img/post/Processor_(Data_path_and_Control)/Untitled3.png)

4. Executing Load and Store Operation

16비트 signed extended offset에 base register를 더해 memory address를 구하고, 해당 주소에 value를 저장 or 로드한다.

![Untitled](/assets/img/post/Processor_(Data_path_and_Control)/Untitled4.png)

5. Executing Branch Operation

Register file에서 읽은 operand를 비교한다. <br>
(0인지 아닌지 = eqaulity) <br>
PC + signed-extended offset으로 branch한다.

![Untitled](/assets/img/post/Processor_(Data_path_and_Control)/Untitled5.png)

6. Executing Jump Operation

PC의 상위 4비트와 address 2 left shift를 합쳐 jump address로 사용한다.

![Untitled](/assets/img/post/Processor_(Data_path_and_Control)/Untitled6.png)

7. Full Datapath

![Untitled](/assets/img/post/Processor_(Data_path_and_Control)/Untitled7.png)

- Single cycle design <br>
fetch, decode, execute가 1 cycle에 완료되는 design을 의미한다.<br>
( 어떤 datapath도 instruction마다 1번 이상 갈 수 없다.<br>
 → 따라서 instruction memory, data memory, several adders로 분리하여 사용한다.)

→ cycle time은 longest path의 길이에 의해 결정된다.

위의 7. Full Datapath에서 control signal이 추가되어야 한다.

1. rt 영역은 R에서는 무조건 읽히지만, I에서는 읽힐 수도 있고, 쓰일 수도 있다.
이와 같은 RegWrite or RegRead의 signal을 결정한다.
2. opcode의 앞의 2bit를 보고 ALU가 add할지 subtract할지 그 외의 동작을 할지 결정한다.

![Untitled](/assets/img/post/Processor_(Data_path_and_Control)/Untitled8.png)