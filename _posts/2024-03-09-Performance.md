---
title: Computer Performance
author: sunwoo
date: 2024-03-09 00:00:00 +0800
categories: [Lecture, Computer Architecture]
tags: [computer science]
---

# Performance

컴퓨터 구조를 이해하고 잘 활용하기 위해서는 컴퓨터 작동 성능을 이해하고 비교할 수 있어야 한다.

execution time을 최소화함으로써 performance를 최대화할 수 있다.

$$
performance_x = 1/execution\_time_x
$$

$$
performance_x/performance_y = execution\_time_y/execution\_time_x = n
$$

위와 같은 수식을 적용시키면 X가 Y보다 n배 빠르다는 것을 의미한다.

## CPU Clocking

cpu는 clock주기에 맞춰서 연산을 진행한다.

즉, 연산을 계속해서 진행하며 cycle이 끝났을 때, 계산된 데이터를 반영하는 방식이다.

(* Clock은 항상 cycle 길이는 바꿀 수 있지만 바꾸지 않으면 매 cycle이 일정하다. *)

clock frequency (rate) : cycle per second

clock period (clock cycle time) : duration of a clock cycle

$$
Clock\_Cycle = 1 / Clock\_Rate
$$

![clock_cycle_rate_relation](/assets/img/post/Performance/clock_cycle_rate_relation.png)

## CPI (Clock Cycles per Instruction)

그렇다면 performance측정을 위한 execution time은 어떻게 구할 수 있을까?

$$
execution\_time = \#Clock\_Cycle * Clock\_Cycle\_Time
$$

$$
Clock\_Cycle\_Time = 1/ Clock\_Rate
$$

여기서 Clock Cycle과 Clock Cycle Time은 서로 tradeoff 관계이다.

CPI (Clock Cycles per instruction) : Computer 성능에 대한 또 다른 지표

- 주의 : CPI를 비교할 때는 같은 ISA, 같은 instruction set을 사용해야 한다.

$$
CPU\_Time = Instruction\_count *CPI*Clock\_Period
$$

$$
CPU\_Time = Instruction\_count*CPI/Clock\_rate
$$

위의 식을 이용하면 CPI를 제외한 나머지 값들을 측정할 수 있어 CPI값을 추론할 수 있다고 한다.

Instruction의 종류에 따라 CPI가 다르고, 종류에 따른 사용 빈도가 다르다.

CPI와 사용 빈도를 통해서 Overall effective CPI를 구할 수 있다.

$$
Overall\_effective\_CPI = ∑^n_{i=1} (CPI_i*IC_i)
$$

$$
(IC = instruction\_count)
$$

이 수식을 이용하면 branch prediction을 사용하거나 instruction의 병렬 연산이 가능할 때, overall effective CPI의 비교를 통해서 속도가 몇 % 향상되는지 확인할 수 있다.

## Reducing Power

컴퓨터에서 전력 소모는 항상 issue이다.

전력 사용량은 다음 함수로 구할 수 있다.

$$
Power ∝Capacity\_load*Voltage^2*Frequency
$$

여기서 cycle frequency를 증가시키면 voltage도 높아져야하고 전력 사용량이 급격히 증가하게 된다.

따라서 일반적인 컴퓨터에서는 DVFS(Dynamic Voltage Frequency Scaling)이 사용된다.

DVFS는 voltage와 frequency를 컴퓨터가 바쁠 때와 한가할 때, scheduling해줘서 전력 소모를 조절한다.

고정된 frequency를 사용할 때와 달리 DVFS를 사용해 컴퓨터가 한가할 때 각 factor 사용량을 15%씩만 줄여도 기존 대비 52%의 전력만으로 작동시킬 수 있다.

![performance_comparison](/assets/img/post/Performance/performance_comparison.png)

## Multi-core Processors

uniprocessor로는 컴퓨터 성능 향상에 한계가 있다.

최근에는 해당 문제를 해결하고자 multi-core processor를 사용한다.

※ instruction level parallelism : 하나의 코어 안에서 병렬적으로 instruction 처리하는 것을 의미

## Amdahl’s Law

![Amdahl's_law](/assets/img/post/Performance/Amdahl's_law.png)

목표하는 execution time을 달성하기 위해 해당하는 affected의 execution time이 얼마나 감소해야하는지 추론할 수 있다.

## 연습문제 1

![practice1](/assets/img/post/Performance/practice1.png)

## 연습문제 2

![practice2](/assets/img/post/Performance/practice2.png)

## 연습문제 1 해설

![practice1_ans](/assets/img/post/Performance/practice1_ans.png)

## 연습문제 2 해설

![practice2_ans](/assets/img/post/Performance/practice2_ans.png)