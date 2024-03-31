---
title: Data Representation
author: sunwoo
date: 2024-03-24 00:00:00 +0800
categories: [Lecture, System Programming]
tags: [computer science]
math: true
comments: true
image: /assets/img/post/Data_Representation/Untitled1.png
---

# Data Representation

## 이진법

컴퓨터는 기본적으로 이진법으로 이루어져 있다.

이진법은 0 또는 1로 표현되고, 비트라 부른다.

8bit가 1byte가 된다.

## Memory Organization

프로그램은 virtual address라는 개념을 사용한다.

virtual address는 프로세스마다 1byte로 이루어진 2^64개의 가상 메모리를 자유롭게 쓸 수 있도록 해준다.

즉, 프로세스마다 크고 독립된 메모리를 사용한다고 느낄 수 있는 것이다.

(process는 프로그램이 실행돼서 cpu에서 작동하는 것을 의미한다.)

(또한 하나의 프로그램도 여러 번 실행되면 각각 다른 프로세스이다.)

## Machine Words

메모리 주소를 word라고 표현한다. 

word는 4byte 혹은 8byte의 크기를 갖는데, 일반적으로 4byte의 크기를 갖는다.

## Data Representation

자료형에 따라 다른 byte크기를 차지한다. 

이 크기는 ISA에 따라 다르게 설정되는데 그 표준은 다음과 같다.

![Untitled](/assets/img/post/Data_Representation/Untitled.png)

## Byte Ordering

컴퓨터 구조에서도 배우는 개념인 byte ordering은 크게 2가지 방식을 가진다.

1. Big Endian (Internet, Sun, PPC Mac)
LSB가 highest address를 갖는 방식이다.
**Casting과 같은 상황에서 복사를 해서 붙여야한다. → CPU 설계 입장에서는 litte endian 선호**
2. Little Endian (x86, ARM)

0x01234567의 숫자가 있을 때, 각 방식은 다음과 같이 숫자를 저장한다.

![Untitled](/assets/img/post/Data_Representation/Untitled1.png)

## Data Representation

```c
#include <stdio.h>

typedef unsigned char* pointer;

void show_bytes(pointer start, int len){
        int i;
        for (i =0; i<len; i++){
                printf("%p\t0x%.2x\n", start + i, start[i]);
        }
        printf("\n");
}

int main() {
        int a = 15213;  /* 0x3b6d */
        show_bytes((pointer) &a, sizeof(int));
        
        /* 출력
        0x11ffffcb8 0x6d
        0x11ffffcb9 0x3b
        0x11ffffcba 0x00
        0x11ffffcbb 0x00
						-> Little Endian 사용한다는 것을 알 수 있다.
				*/

        return 0;
}
```

```c
ouo#include <stdio.h>

typedef unsigned char* pointer;

void show_bytes(pointer start, int len){
        int i;
        for (i =0; i<len; i++){
                printf("%p\t0x%.2x\n", start + i, start[i]);
        }
        printf("\n");
}

// Casting?
// pointer 산술 연산

int main() {
        int a = 10;
        float b = 1.1f;
        long long c = (long long)65534;  // 0x00 00 00 00 00 00 FF FE

        int array[4] = {0,1,2,3}; // 16byte
        int* int_p = array;

        printf("%lu %p\n", sizeof(int_p), int_p);  // 8 0x7ffc0e9311b0
        printf("%lu %p\n", sizeof(array), array);  // 16 0x7ffc0e9311b0 
        // show_bytes((pointer)&c, sizeof(c));
        // printf("%p\n", array);
        // printf("%p\n", array+1);  // int type의 array에 +1이므로 4byte가 더해진다.
        show_bytes((pointer)&array, sizeof(array));
        
        /*  output
        0x7ffc0e9311b0  0x00
				0x7ffc0e9311b1  0x00
				0x7ffc0e9311b2  0x00
				0x7ffc0e9311b3  0x00
				0x7ffc0e9311b4  0x01
				0x7ffc0e9311b5  0x00
				0x7ffc0e9311b6  0x00
				0x7ffc0e9311b7  0x00
				0x7ffc0e9311b8  0x02
				0x7ffc0e9311b9  0x00
				0x7ffc0e9311ba  0x00
				0x7ffc0e9311bb  0x00
				0x7ffc0e9311bc  0x03
				0x7ffc0e9311bd  0x00
				0x7ffc0e9311be  0x00
				0x7ffc0e9311bf  0x00
        */
        
        printf("%p\n", ((pointer)array)+1);  // pointer type 에서 +를 하면 pointer 크기인 1이 더해진다.

        return 0;
}
```

## String

string은 어떻게 바이트를 표현할까? 

string은 char의 array 형태로 이루어져 있다. 따라서 1 byte가 sequential하게 이어져 있어서 Byte Ordering과는 상관이 없다.

또한 string의 마지막에는 \0 (null 값) 이 들어가야 하므로 주의해야한다.

```c
#include <stdio.h>

int main(){
        char c = 0x30;
        char s[8] = "Hello";  //6이상의 값이 들어갈 수 있다.
        char key[6] = "APPLE";
        char enc[6];
        char dec[6];

        for (int i = 0; i < 6; ++i){
                enc[i] = s[i] ^ key[i];
        }
        show_bytes((pointer)enc, sizeof(enc));
				/*
				0x7ffd61c490c4  0x09
				0x7ffd61c490c5  0x35
				0x7ffd61c490c6  0x3c
				0x7ffd61c490c7  0x20
				0x7ffd61c490c8  0x2a
				0x7ffd61c490c9  0x00
				*/
				
				// 아래와 같은 코드를 이용하여 기본적인 암호화를 해볼 수 있다.
        for (int i = 0; i <6; ++i){
                dec[i] = enc[i] ^ key[i];
        }
        printf("%s %s %s\n", s, enc, dec);  // Hello   5< * Hello

        c += 17;
        printf("%x %c\n", (int)c, c);  // 41 A
        show_bytes((pointer)%c, sizeof(c));  // 0x7ffd61c490b3  0x41

        printf("%s\n", s);  // Hello
        show_bytes((pointer)s, sizeof(s));
        /*
        0x7ffd61c490d0  0x48
				0x7ffd61c490d1  0x65
				0x7ffd61c490d2  0x6c
				0x7ffd61c490d3  0x6c
				0x7ffd61c490d4  0x6f
				0x7ffd61c490d5  0x00
				0x7ffd61c490d6  0x00
				0x7ffd61c490d7  0x00
        */
        return 0;
}
```

```c
char s[?] = "Hello";
// ?에는 6이 들어와야 한다. (\0위치도 포함해야하기 때문)
```

※ Unicode는 바이트를 묶어서 하나의 word를 표현하는 방식이다.

## Bit-level Manipulation

![Untitled](/assets/img/post/Data_Representation/Untitled2.png)

컴퓨터는 NAND와 NOR 연산만 가지고 모든 연산을 처리할 수 있다고 한다.

!, ~ 의 방식은 조금 다르다.

~0x41 = 0xBE

~0x00 = 0xFF

!0x41 = 0x00

!0x00 = 0x01

```c
#include <stdio.h>

int main()
{
        int a = 0x41;

        printf("%x %x\n", !a, ~a); // 0 ffffffbe

        int a = 0x4;
        int b = 0x1;

        // Logic operation
        if (a&&b){
                printf("1\n");  // 1
        } else{
                printf("2\n");
        }

        // bit operation
        if (a&b){
                printf("3\n");
        } else{
                printf("4\n");  // 4
        }

        int* p = NULL;

        printf("%d\n", *p);
        
        // pointer가 존재하는지 먼저 확인하고 pointer 위치에 값이 있는지 확인 
        // 반대로 if (*p && p)를 할 경우 p가 존재하지 않을 때, *p에서 에러가 발생
        if (p&& *p){
                printf("Exist\n");
        } else{
                printf("NULL\n");
        }

        return 0;
}
```

비트를 이용해서 set을 표현할 수도 있다.

ex) 01101001 의 정보를 갖는 set은 { 0, 3, 5, 6 } 의 원소를 갖는 set이라 여길 수 있다.

Left shift : x << y

Right shift : x >> y

Shift의 방법은 두 가지로 나뉜다.

1. Logical shift
왼쪽을 무조건 1로 채운다.
2. Arithmetic shift (정수의 부호를 유지하기 위한 방법)
right shift를 할 때, 맨 끝에 있던 숫자를 복사해 더한다.

```c
#include <stdio.h>
#include <stdlib.h>

int main(){
        signed int a = 0xF0000001;
        a = a <<2;

        printf("%d\n", a);  // -1073741820
        printf("%x\n", a);  // c0000004
        printf(" << %x\n", a<<2);  //  << 10
        printf(" >> %x\n", a>>2);  //  >> f0000001

        return 0;
}
```

## Integers

비트값에 따라 integer 값을 결정하는 방법은 다음과 같다.

$$
Unsinged : B2U(X) = \sum_{i=0}^{w-1}x_i*2^i
$$

$$
Singed : B2T(X) = -x_{w-1}*2^{w-1} + \sum_{i=0}^{w-2}x_i*2^i
$$

```c
#include <stdio.h>
#include <stdlib.h>
#include <limits.h>

int main() {
        // unsigned int a = 0x80000000;
        unsigned int a = 0xFFFFFFFF;

        // 실제로 실행될 때는 타입이 없다. (레지스터와 같은 곳)
        printf("%d\n", a); // 양수값이 나온다.? (%d가 integer를 출력하라는 의미여서 그렇다.)
        printf("%u\n", a); // %u가 unsigned를 출력하라는 의미

        char b = 127;
        printf("%d\n", b); // 127
        b += 1;
        printf("%d\n", b); // -128

        // unsigned 를 사용해 error를 배제할 수 있다.
        // for (unsigned int i = 0; i < 10; i++)

        unsigned int c = 0x80000000;
        int d = c; // c가 casting 되어 들어가서 양수가 음수로 바뀐다.

        printf("%u\n", c);
        printf("%d\n", d);

        return 0;
}
```

Unsigned int의 최대, 최소와 , 2의 보수의 최대, 최소는 다음과 같다.

$$
U_{Min}=0,\quad U_{Max}=2^w-1
$$

$$
T_{Min}=-2^{w-1},\quad T_{Max}=2^{w-1}-1
$$

따라서 다음과 같은 수식이 성립한다.

$$
|T_{Min}|=T_{Max}+1,\quad U_{Max} = 2*T_{Max}+1
$$

![Untitled](/assets/img/post/Data_Representation/Untitled3.png)

signed, unsigned integer는 같은 비트를 가지고 있을 때,
절반에 대해서는 같은 값을 절반에 대해서는 $2^n,\;n=\# \;of \;bit$만큼 차이가 난다.

```c
#include <stdio.h>
#include <stdlib.h>
#include <limits.h>

int main(){
        char a = 0xee;
        printf("%d\n", a);
        printf("%X\n", a); // FFFFFFEE 가 출력된다.
                           // a가 어떠한 type인지 모르므로 기본적으로 (int) type으로 본다.
                           // 그래서 가장 앞 비트가 1이므로 음수로 보고 int로 casting할 때 1로 가득 채운다.

        char b = -8;
        unsigned char c = (unsigned char)b;
        printf("%02X\n", (b & 0xff));    // F8
        printf("%02X\n", (c & 0xff));    // F8
        printf("%02X\n", ((b>>2) & 0xff));    //FE
        printf("%02X\n", ((c>>2) & 0xff));    //3E

        return 0;
}
```

## Code security

메모리 접근에 주의하지 않으면 FreeBSD의 getpeername()에서 발생했던 보안 제와 비슷한 오류가 발생할 수 있다.

```c
#include <stdio.h>

void foo(int* p){
        p += 1;   // 원래 a, b 주소 4차이 나는데
        *p = 30;    // p+1 위치에 30 지정하므로 b의 값이 변경되는 불상사가 일어남
}

int main(){
        int a = 10;
        int b = 20;

        foo(&a);

        printf("%p\n", &a);
        printf("%p\n", &b);
        printf("%d %d\n", a,b);
        // printf("%p\n", p);

        return 0;
}
```