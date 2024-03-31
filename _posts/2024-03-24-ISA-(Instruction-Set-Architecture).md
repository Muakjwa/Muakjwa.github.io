---
title: ISA (Instruction Set Architecture)
author: sunwoo
date: 2024-03-24 00:00:00 +0800
categories: [Lecture, Computer Architecture]
tags: [computer science]
math: true
comments: true
image: /assets/img/post/ISA_(Instruction_Set_Architecture)/Untitled 4.png
---

# ISA (Instruction Set Architecture)

## ISA (Instruction Set Architecture)

ISA는 프로그래머와 하드웨어와의 계약이라 볼 수 있다.

1. Instruction은 binary 형태로 표현되어야 한다.
(ex. add r1, r2, r3 → 01000110…)
2. 프로그램은 data처럼 메모리에 저장되고, 읽고, 쓰인다.

(ISA가 하는 일 중 하나는 Memory State를 visible하게 만드는 일이다.)

※ 다른 ISA를 가진 컴퓨터에서는 binary file이 실행되지 못한다.

ISA에 대해서는 가전제품과 같이 임베디드 시스템에 많이 사용되는 MIPS를 기준으로 설명한다.

instruction은 다음과 같이 나뉠 수 있다.

- Computational
- Load/Store
- Jump and Branch
- Etc

Instruction은 크게 3가지 format으로 나타낼 수 있다.
(R format, I format, J format)

![Untitled](/assets/img/post/ISA_(Instruction_Set_Architecture)/Untitled.png)

instruction은 registor에서 작동되고, registor는 32bit의 공간을 갖는다.

![Untitled](/assets/img/post/ISA_(Instruction_Set_Architecture)/Untitled 1.png)

MIPS instruction의 field는 다음과 같다.

![Untitled](/assets/img/post/ISA_(Instruction_Set_Architecture)/Untitled 2.png)

## Register Operands (Arithmetic instruction)

왜 Arithmetic instruction 작동을 위해 register를 사용할까?

- 다른 메모리(cache, memory)보다 빠르다
compiler는 최대한 많은 변수를 register에 저장해야 한다.
따라서 less frequently used variable들만 메모리에 저장한다.
→ Register optimization이 중요하다.
- compiler가 사용하기 더 쉽다
- 변수를 담을 수 있어서 code density가 증가한다

MIPS는 32 X 32-bit register를 갖고 있다.

레지스터는 2개의 read port와 1개의 write port를 갖는다.

![Untitled](/assets/img/post/ISA_(Instruction_Set_Architecture)/Untitled 3.png)

registor operand는 3가지 principle로 디자인 되었다.

1. Simplicity favors regularity
간결함을 위해 규칙적으로 만든다.
적은 수의 format과 항상 첫 6비트를 opcode로 사용한다.
regularity → simplicity → higher performance at lower cost
2. Smaller is faster
레지스터가 커지면 비용이 늘어나고, 성능이 떨어진다.
따라서 레지스터를 32개로 제한한다.
addressing modes의 수도 제한한다.
3. Make the common case fast
small constant 사용은 일반적인 경우이므로 더 빠르게 사용할 수 있도록 만드는게 좋다.
ex) addi $s3, $s3, 4
4. Good design demands good compromises
register format을 최대한 비슷하게 유지하는 것이 좋다. (3개의 format만을 사용한다.)
다른 format은 decoding을 복잡하게 하지만, 32bit instruction을 균일하게 해준다.

## Byte Addresses

대부분의 구조는 메모리에서 바이트 단위로 주소를 가리킨다.

메인 메모리에는 composite data(Array, structure)이 저장된다.

Arithmetic operation을 수행할 때는 memory → register, 저장할 때는 register → memory

1개의 word (= 4byte)에 어떤 순서로 byte를 저장할 수 있는가?

1. Big Endian
: MSB (most significant byte) - MIPS
→ Good for comparison
2. Little Endian
: LSB (least significant byte) - x86, DEC
→ Good for calculation

![Untitled](/assets/img/post/ISA_(Instruction_Set_Architecture)/Untitled 4.png)

## Number of Operands 동작

1. 3 operands
1 result + 2 inputs
ex) R1 = R2 + R3 → Add R1, R2, R3
2. 2 operands
1 result/first input + 1 second input
R1 = R1 + R2 → Add R1, R2
3. 1 operands
implicit accumulator + 1 input
accumulator = accumulator + R1 → Add R1
4. 0 operands
add top two elements of the stack → Add 

## 2의 보수

unsigned binary integer : $0\;to \;2^{n}-1$ 범위를 갖는다.

signed binary integer : $-2^{n-1}\;to\;+2^{n-1}-1$ 범위를 갖는다.

이진수에서 첫 번째 비트가 1이면 음수, 0이면 양수가 된다.

그래서 음수와 양수의 각각 최소, 쵀댓값은 다음과 같다.

- Most-negative : 1000 0000 …. 0000
- Most-positive : 0111 1111 …. 1111

그렇다면 부호 변환은 어떻게 할 수 있을까?

→ Complement를 구하고 +1을 해주면 부호 변환이 된다.

proof) $x+\bar{x}=1111...111_2 = -1$ 이므로 $-x = \bar{x}+1$이 된다.

부호를 가진 숫자의 비트 수를 늘리는 casting을 할 때는 부호 변환에 유의해야한다.

음수는 비트를 추가할 때 모두 1으로 늘려주고, 양수는 0으로 늘려주면 된다.

ex) +2 : 0000 0010 ⇒ 0000 0000 0000 0010

       -2 : 1111 1110 ⇒ 1111 1111 1111 1110

## Arithmetic Operation

몇 가지 MIPS 기본 연산 코드를 살펴본다.

```c
add a, b, c    // a gets b+c

// f = (g + h) - (i + j); 코드를 다음과 같이 표현할 수 있다.
add t0, g, h    // temp t0 = g + h
add t1, i, j    // temp t1 = i + j
sub f, t0, t1    // f = t0 - t1

// g = h + A[8]; 코드를 다음과 같이 표현할 수 있다.
lw $t0, 32($3)    // load word (s3를 기준으로 32바이트 떨어진 주소를 t0로 load)
add $s1, $s2, $t0

// A[12] = h + A[8]; 코드를 다음과 같이 표현할 수 있다.
lw $t0, 32($s3)    // load word
add $t0, $s2, $t0
sw $t0, 48($s3)    // store word

addi $s3, $s3, 4    // $s3와 4의 합을 $s3에 저장
// -1을 사용하면 되므로 addi는 존재하지만 subi는 존재하지 않는다.
addi $s2, $s1, -1    // $s1과 -1의 합을 $s2에 저장

// $zero register를 정의해놓음으로써 move와 같은 추가적인 instruction을 줄여준다.
add $t2, $s1, $zero   

##### Logical Operations #####
// sll : (왼쪽으로 shift후 빈공간 0으로 채운다.) unsigned에 대해서 2를 곱해주는 효과
// srl : (오른쪽으로 shift후 빈공간 0으로 채운다.) unsigned에 대해서 2로 나눠주는 효과
// and, andi, or, ori, nor(Not인 ~의미)
and $t0, $t1, $t2    // t1과 t2의 비트 연산자를 t0에 저장
or $t0, $t1, $t2    // t1과 t2의 비트 연산자를 t0에 저장
nor $t0, $t1, $zero    // t1과 zero를 nor 연산하면 t1을 not 연산한 것과 같은 동작을 한다.
--------------> 최대한 instruction을 적게 가져간다. <------------
##############################

##### Conditional Operations #####
beq rs, rt, L1    // if(rs==rt) goto label L1의 동작을 한다.
bne rs, rt, L1    // if(rs!=rt) goto label L1의 동작을 한다.
j L1    // goto L1의 동작을 한다.
slt rd, rs, rt    // if(rs<rt) rd = 1; else rd = 0;
slti rt, rs, constant    // if(rs<constant) rt = 1; else rt = 0;
// sltu, sltui : unsigned에 대해서 comparison하는 함수이다.

※※※※※※ blt, bgt는 왜 없을까?
-> equal을 비교하는 것보다 대소 비교가 더 오래걸려서 다른 instruction에 비해 속도가 느리다.
-> instruction마다 속도가 크게 차이나면 instruction이 실행되는데 걸리는 1번의 clock 시간이 길어져 전반적인 instruction 속도가 느려지게 된다.
##################################

jal ProcedureAddress    // jump and link
jr $ra    // return

// byte, half word를 load, store할 수도 있다.
lb rt, offset(rs)    // signed의 경우이며 sign extend한다.
lh rt, offset(rs)
lbu rt, offset(rs)    // unsigned를 의미하며 zero extend한다.
lhu rt, offset(rs)
sb rt, offset(rs)
sh rt, offset(rs)
```

```c
ex) C code에서 다음과 같은 코드는 아래 MiPS 코드로 바꿀 수 있다.
##### C code:
if (i==j) f = g+h;
else f = g-h;
#####

##### MIPS:
			bne $s3, $s4, Else
			add $s0, $s1, $s2
			j Exit
Exit: sub $s0, $s1, $s2
Exit: ....
#####
```

```c
##### C code:
while(save[i] == k) i+=1;
#####

##### MIPS:
Loop: sll $t1, $s3, 2
			add $t1, $t1, $s6
			lw $t0, 0($t1)
			bne $t0, $s5, Exit
			addi $s3, $s3, 1
			j Loop
Exit: ....
#####
```

## Instruction formats

MIPS instruction은 Regularity를 가지고 32bit binary number로 encoding된다.

1. R-format
산술 연산에서 주로 사용되는 instruction이다.
ex) add $t0, $s1, $s2

![Untitled](/assets/img/post/ISA_(Instruction_Set_Architecture)/Untitled 5.png)

1. I-format
즉각적인 arithmetic 연산이나 load/store을 담당하는 instruction format이다.
Constant위치는 16비트를 할당받아 $-2^{n-1}\;to\;+2^{n-1}-1$ 범위를 갖는다.

![Untitled](/assets/img/post/ISA_(Instruction_Set_Architecture)/Untitled 6.png)

## Procedure

 Call이 불리면 함수의 local variable을 메모리에 저장한다.

각 procedure call은 stack frame을 만들고 함수가 끝나면 SP(stack pointer)를 옮겨서 stack frame을 제거한다.

( SP는 general purpose register가 아닌 특별 register에 저장된다. )

- pocedure 실행 순서 (main routine = caller, procedure = callee라 본다)
1. caller는 callee가 접근할 수 있는 곳에 parameter를 둔다.
2. caller는 callee에게 제어권을 넘긴다.
3. callee는 필요한 저장공간 자원을 얻는다 (stack memory 할당)
4. callee는 업무를 수행한다.
5. callee는 결과값을 caller가 접근할 수 있는 곳에 둔다. ($v0 - $v1 : two value register for result)
6. callee는 caller에게 제어권을 넘긴다. ($ra : return arddress register)

- MIPS procedure call instruction

jal : register $ra에 다음 instruction의 위치인 PC+4를 저장한다.

procedure이 끝나면 jr instruction을 통해서 $ra에 저장된 위치로 jump한다.

register에 할당되어 있는 argument, return value를 위한 공간보다 더 많은 공간이 필요할 수 있다.

( ex. 함수가 연속적으로 call 되었을 때, return value는 계속 증가한다. )

→ 이와 같이 register 공간이 부족해지는 경우 stack에 push, pop하여 저장한다.
    ($sp는 stack pointer로써 현재 stack의 위치를 갖는다.)
    (push할 때는 $sp -= 4, pop할 때는 $sp += 4  ******stack은 아래로 쌓인다.*****)*

```c
##### C code:
int leaf_example(int g, h, i, j)
{
	int f;
	f = (g + h) - (i + j);
	return f;
}
#####

##### MIPS:
leaf_example:
	addi  $sp, $sp, -4
	sw  $s0, 0($sp)
	add  $t0, $a0, $a1
	add  $t1, $a3, $a3
	sub  $s0, $t0, $t1
	add  $v0, $s0, $zero    // v0가 return값이다.
	lw  $s0, 0($sp)
	addi  $sp, $sp, 4
	jr  $ra
#####
```

함수를 사용할 때, procedure을 호출하는 procedure이 여러번 연결되어 있으면 nested call이 발생하고, 이러한 경우에 register가 다 저장하지 못하는 정보를 stack에 저장하게 된다.

```c
##### C code:
int fact (int n)
{
	if (n < 1) return 1;
	else return n * fact(n-1);
}
#####

##### MIPS:
fact:
	addi  $sp, $sp, -8
	sw  $ra, 4($sp)
	sw  $a0, 0($sp)
	slti  $t0, $a0, 1
	beq  $t0, $zero, L1
	addi  $v0, $zero, 1
	addi  $sp, $sp, 8
	jr  $ra
L1: addi  $a0, $a0, -1
	jal fact
	lw  $a0, 0($sp)
	lw  $ra, 4($sp)
	addi  $sp, $sp, 8
	mul  $v0, $a0, $v0
	jr  $ra
#####
```

array와 같은 customatic 변수도 stack에 저장되는데 이러한 공간을 stack frame이라 한다.

→ frame pointer라는 추가적인 pointer를 사용하는데 stack frame의 top을 의미하며
    이전 함수의 stack pointer라 볼 수 있다.

- Text : program code
- Static data : global variable
- Dynamic data : heap (동적 할당)
- Stack : function call, automatic storage
- Reserved : 커널이나 예외처리를 위해 확보된 공간

![Untitled](/assets/img/post/ISA_(Instruction_Set_Architecture)/Untitled 7.png)

Memory address를 저장, 사용하는 방법으로는 여러 가지가 있지만 MIPS는 displacement mode를 사용한다.

ex) R4 ← Mem[ R1 + Disp ]

```c
##### C code:
void strcpy(char x[], char y[])
{
	int i;
	i = 0;
	while ((x[i] = y[i]) != '\0')
		i += 1;
}
#####

##### MIPS:
strcpy:
	addi  $sp, $sp, -4
	sw  $s0, 0($sp)
	add  $s0, $zero, $zero
L1: 
	add  $t1, $s0, $a1    // $a1 = y 주소
	lbu  $t2, 0($t1)
	add  $t3, $s0, $a0    // $a0 = x 주소
	sb  $t2, 0($t3)
	beq  $t2, $zero, L2
	addi  $s0, $s0, 1
	j  L1
L2:
	lw  $s0, 0($sp)
	addi  $sp, $sp, 4
	jr  $ra
#####
```

대부분의 constant는 작아서 16비트 이내에서 표현 가능하다.

하지만 때때로 32비트로 표현해야 하는 경우, 
lui는 왼쪽 16비트에 constant를 copy하고 오른쪽 16비트는 0으로 설정한다.
이 후 or 연산을 하는 ori 명령어를 사용해서 오른쪽 16비트를 추가 설정해줄 수 있다.

branch 명령어의 경우, opcode, two register, target address를 저장한다.

주로 branch target이 branch 근처에 있어 앞,뒤로 이동할 offset을 16비트에 저장한다.

→ Target address = PC + offest * 4 (*** PC는 이미 +4가 되어있는 상태 ***)

j와 jal은 op code로 6비트, address로 26비트를 저장하며,
PC의 상위 4비트와 address를 *4한 28비트를 연결하여 target address로 사용한다.

![Untitled](/assets/img/post/ISA_(Instruction_Set_Architecture)/Untitled 8.png)

```c
##### C code:
void swap(int v[], int k)
{
	int temp;
	temp = v[k];
	v[k] = v[k+1];
	v[k+1] = temp;
}
#####

##### MIPS:
swap:
	sll  $t1, $a1, 2
	add  $t1, $a0, $t1    // $t1 = v + (4*k)
	lw  $t0, 0($t1)
	lw  $t2, 4($t1)
	sw  $t2, 0($t1)
	sw  $t0, 4($t1)
	jr  $ra
#####
```

```c
##### C code:
void sort(int v[], int n)
{
	int i, j;
	for (i = 0; i < n; i+=1){
		for (j = i-1; j>=0 && v[j] > v[j+1]; j-=1){
			swap(v,j);
		}
	}
}
#####

##### MIPS:
	move  $s2, $a0
	move  $s3, $a1
	move  $s0, $zero
for1tst:
	slt  $t0, $s0, $s3
	beq  $t0, $zero, exit1
	addi  $s1, $s0, -1
for2tst:
	slti  $t0, $s1, 0
	bne  $t0, $zero, exit2
	sll  $t1, $s1, 2
	add  $t2, $s2, $t1
	lw  $t3, 0($t2)
	lw  $t4, 4($t2)
	slt  $t0, $t4, $t3
	beq  $t0, $zero, exit2
	move  $a0, $s2
	move  $a1, $s1
	jal  swap
	addi  $s1, $s1, -1
	j  for2tst
exit2:
	addi  $s0, $s0, 1
	j  for1tst
exit1:
#####
```

위의 sort 함수를 완벽하게 표현하려면 stack에 저장하고, load하는 과정을 모두 포함하여야 한다.

- 성능 비교

clock cycles = CPI * isntruction count라 볼 수 있는데

compiler quantization과 같은 기법을 사용한 경우, CPI는 변화가 거의 없지만, instruction count는 현저히 감소한다. 

이처럼 CPI나 instruction count 각각만을 보고 성능에 대한 metric으로 사용할 수는 없다.

( *** 또한 compiler optimization은 알고리즘에 민감해 코드를 잘 짜야한다;;; *** )

- 성능 향상

성능 향상을 위해 for문 사용시 array의 index를 증가시키는 것보다 pointer 값을 증가시키는게 더 효율적이다.

![Untitled](/assets/img/post/ISA_(Instruction_Set_Architecture)/Untitled 9.png)

이처럼 index를 사용했을 때는 loop 내부에서 shift 과정이 일어나 추가적인 load가 생긴다.

- pseudoinstruction

대부분의 instruction은 machine code에 one-to-one이지만 pseudoinstruction은 아래와 같이 2개의 machine instruction으로 치환되어서 사용된다.

![Untitled](/assets/img/post/ISA_(Instruction_Set_Architecture)/Untitled 10.png)