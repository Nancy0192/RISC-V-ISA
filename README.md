# RISC-V
This repository takes you through the RISC - V ISA. 

## Overview

**Day 1 - Introduction to RISC-V ISA And GNU compiler toolchain**
- Installation
- Introduction
- Integer Number Representation
- Labwork

**Day 2 - Introduction to ABI and basic verification flow**
- Application Binary Interface




## Day 1 - Introduction to RISC-V ISA And GNU compiler toolchain

## Installation
<details><summary>Steps For Instastallation</summary>
Before you can build the RISC-V toolchain, you'll need to install some software dependencies:

```
sudo apt update
sudo apt install autoconf automake autotools-dev curl python3 libmpc-dev libmpfr-dev libgmp-dev gawk build-essential bison flex texinfo gperf libtool patchutils bc zlib1g-dev libexpat-dev git
```
Now clone the RISC-V GNU Toolchain Repository

```
git clone --recursive https://github.com/riscv/riscv-gnu-toolchain
```

Navigate into the toolchain directory and initiate the build:

```
cd riscv-gnu-toolchain
./configure --prefix=/opt/riscv
make
```

After installing, you'll want to add the toolchain binaries to your PATH:

```
echo 'export PATH=$PATH:/opt/riscv/bin' >> ~/.bashrc
source ~/.bashrc
```

Now you can test the installation by checking the version of the GCC compiler:

```
riscv64-unknown-elf-gcc --version
```
  
</details>

## Introduction
<details> <summary>RISC - V</summary>
<br>
RISC-V is an open-source instruction set architecture (ISA) used for the development of custom processors targeting a variety of end applications.RISC-V ISA is considered the fifth generation of processors built on the concept of the reduced instruction set computer (RISC). Due to its openness and its technical merits, it has become very popular in recent years.
  The royalty-free RISC-V ISA features a small core set of instructions upon which all the design’s software runs. Its optional extensions allow designers to tailor the architecture for a variety of different end markets. Essentially, the RISC-V architecture allows designers to customize and build their processor in a way that’s tailored to their target end applications, so they can optimize the power, performance, and area (PPA) for those applications. The RISC-V ISA also provides the flexibility to pick and choose from available features, rather than having to use the full feature set.


</details>

<details><summary>GNU Compiler toolchain</summary>
<br>
The GNU compile toolchain is a set of programming tools in LINUX system that can be use for compiling a code to generate certain executable program, library and debugger and whose detail can be found in references. RISC-V is one such toolchain which supports C and C++ cross compiler. It supports two build modes: a generic ELF/Newlib toolchain and a more sophisticated Linux-ELF/glibc toolchain and the github link for the same can be found in references.
  
</details>

## Integer Number Representation

<details><summary><strong>Number System For Unsigned Numbers</strong></summary>

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/da5efeb2-d882-4a4c-b9c8-e6ce14ebd837)


As the above image illustrates in RISC-V architecture, the terms "bits," "bytes," and "words" have specific meanings related to data representation and memory organization.

- Bits: Bits are the fundamental units of information in computing. In RISC-V, as in most architectures, a bit can represent one of two values: 0 or 1. Bits are used to encode all types of data, including instructions, numbers, characters, and more.<br>
- Byte :  byte is a group of 8 bits. It's a common unit of storage and data representation in computing. Bytes are often used to represent characters and small data values. In RISC-V, memory is typically addressed at the byte level, meaning that each byte of memory has a unique address.<br>
- Word :     In the context of RISC-V, the term "word" refers to the natural unit of data that a processor can operate on in a single instruction. The size of a word in RISC-V is determined by the architecture's specification, which can vary between different versions and implementations of RISC-V.

Common word sizes in RISC-V include:
   - 32-bit Word (RV32): In RISC-V RV32 architecture, a word is 32 bits or 4 bytes in size. This is the most common word size for embedded systems and lower-end processors.
   - 64-bit Word (RV64): In RISC-V RV64 architecture, a word is 64 bits or 8 bytes in size. This architecture provides larger addressable memory and increased precision for floating-point operations.
   - 128-bit Word (RV128): Some extensions to the RISC-V architecture, such as the RV128 extension, introduce support for 128-bit data types and operations.




</details>

<details><summary><strong>Number System For Signed Numbers</strong></summary>
  <br>
To represent negative numbers using two's complement, follow these steps:
  - Take the binary representation of the positive counterpart of the negative number.
  - Invert (flip) all the bits (change 0s to 1s and vice versa).
  - Add 1 to the inverted value.


  
  ![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/1badef67-6a70-459d-94b1-50fc5f83830e)

</details>

## Labwork
<details><summary><strong>LAB 1 : C Program To Compute From 1 to n</strong></summary>
  <br>
C code for sum from 1 to n:

```
#include <stdio.h>

int main(){
       int i, sum=0, n=5;
       for (i=1; i<=n; ++i){
       sum+=i;
        }
       printf("Sum of numbers from 1 to %d is %d\n", n, sum);
       return 0;
}
```

Commands to compile:

```
gcc sum1ton.c
./a.out
```

Output:

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/09b6a1cf-643a-413a-94b9-19f2e0a79421)



</details>

<details><summary><strong>LAB 2 : RISCV GCC Compile And Disassemble</strong></summary>
  <br>
Commands to compile using RISC -V GCC compiler:

```
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
```

We can also run usin the -Ofast command which will reduce our instruction as shown below:

```
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
```


Now check the contents of the object file created:

```
ls -ltr sum1ton.o
```

You will observe the following contents on your terminal

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/1e03563b-9f1d-46c8-9db5-fcf546d3ce69)


To check the assembly code using the following command:

```
 riscv64-unknown-elf-objdump -d sum1ton.o | less
```


![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/ea7f6659-a20d-4abf-8054-3bb4285f2bb2)



</details>

<details><summary><strong>LAB 3 : Spike Simulation And Debug</strong></summary>
<br>
To get the output for the riscv compiler use the following command:

```
spike pk sum1ton.o
```

Now to debug open the debugger:

```
spike -d pk sum1ton.o
```

Some of the commands used in debugger:
- until pc 0 100b0 : to execute till 100b0 address.
- reg 0 a0 : to load the contents of a0.

  
</details>


<details><summary><strong>LAB 4 : Unsigned Number</strong></summary>
<br>
Code for UnsignedHighest

```
#include <stdio.h>
#include <math.h>
int main() {
unsigned long long int max = (unsigned long long int) (pow(2,64) -1);
printf("highest number represented by unsigned long long int is %llu\n", max);
return 0;
}
```

Compile it to see:

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/ef660e23-fee7-438c-81d0-dbcc9c0ac50c)


<br>
<br>
Code for UnsignedLowest

```
#include <stdio.h>
#include <math.h>
int main() {
unsigned long long int max = (unsigned long long int) (pow(2,64)*-1);
printf("highest number represented by unsigned long long int is %llu\n", max);
return 0;
}
```

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/b19d71cc-58f2-4ea8-9995-b7eda74fc247)



</details>

<details><summary><strong>LAB 4 : Signed Number</strong></summary>
<br>
Code for signed highest and lowest:

```
#include <stdio.h>
#include <math.h>
int main() {
long long int max = (long long int) (pow(2,63) -1);
long long int min = (long long int) (pow(2,63) * -1);
printf("highest number represented by long long int is %lld\n", max);
printf("lowest number represented by long long int is %lld\n", min);
return 0;
}
```




![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/aceb08b2-cede-4a9b-887d-fee20cd677ee)



</details>



## Day 2 - Introduction to ABI and basic verification flow
## Application Binary Interface
<details><summary><strong>ABI</strong></summary>
<br>
The Application Binary Interface (ABI) in the context of computer architecture refers to the set of rules and conventions that dictate how software components (such as compiled binaries and libraries) interact with each other at the binary level. The ABI defines various aspects such as parameter passing, register usage, memory layout, and system call invocation. Each architecture, including RISC-V, has its own ABI that software must adhere to in order to ensure compatibility and interoperability.

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/8cd557fa-3f0f-4ba2-9a98-ae74e259db02)

- The application programmer can access some part of the RISC-V processor or any other processor via registers.
- In Risc-V architecture we have 32 registers whose length is defined by "XLEN". It is 32 for RV32 and 64 for RV64.

</details>

<details><summary><strong>Memory Allocation</strong></summary>
  <br>
There are 2 ways to load the data into the registers either the data is directly loaded in the registers or it is first stored in the memory and then the memory address is stored into the register as illustrated by the image.
<br>

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/430ae82d-2f14-4334-9f51-1952923f5f66)

<br>
- Little-endian memory addressing system means that the least significant group of 8-bits will be stored in the lowest memory address.
  
</details>


<details><summary><strong>Load, Add and Store Instruction</strong></summary>
  
- Load Instruction:   
The RISC-V assembly instruction ld x8, 16(x23) is used to load a 64-bit value from memory into a register. Let's break down the components of this instruction:<br>
  ld: This is the mnemonic for the "Load Doubleword" instruction, which is used to load a 64-bit value from memory.<br>
  x8: This is the destination register. The value loaded from memory will be stored in register x8.<br>
  16(x23): This is the memory address where the value is located. x23 is a register, and 16 is an immediate offset added to the value in x23 to calculate the memory address.<br>
  
- Add Instruction: Similarly, the instruction "add x8, x24, x8" in RISC-V performs the operation of adding the values in registers x24 and x8, and then stores the result back in register x8.

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/c7575049-4d90-4fe8-be64-f2c4c20cd7a6)

  
- Store Instruction: The instruction "sd x8, 8(x23)" in RISC-V performs the operation of storing the value in register x8 into memory at an address calculated by adding an offset of 8 bytes to the base address stored in register x23.
<br>
Lets see how it fits within the RISC-V 32-bit instruction format:<br>
  Opcode (7 bits): The opcode field specifies the operation of the instruction. For the load instruction, the opcode might be a specific value that indicates a load operation.<br>
  Rd (5 bits): In this instruction, x8 is the destination register where the loaded value will be stored. The register x8 is encoded using a 5-bit field that represents the destination register.<br>
  Immediate (12 bits): The immediate field in this instruction is used to specify the offset from the base address stored in register x23. In the example instruction, the immediate value is 16, which is encoded using a 12-bit field. This immediate value represents the offset in bytes from the base address in register x23.<br>
  Rs1 (5 bits): The source register x23 is used as the base address for the memory access operation. The register x23 is encoded using a 5-bit field that represents the source register.<br>
  Opcode Extension (3 bits): This might indicate the specific extension or variant of the instruction. For example, for the "ld" instruction, the extension might specify the size of the loaded data (byte, halfword, word, doubleword).<br>

  ![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/b1c8909f-980f-4e4b-8a5e-bfebf876588b)

  
</details>

<details><summary><strong>Register's ABI Names</strong></summary>

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/b2f92695-55a6-41b4-b665-18a1e048324d)



</details>


## Labwork
<details><summary><strong>Lab 1</strong></summary>
<br>
C Code :

```
#include<stdio.h>

extern int load(int x,int y);
int main(){

	int result=0;
	int count =9;
	result=load(0x0,count+1);
	printf("sum of number from 1 to %d is %d\n",count,result);
}
```

Load file :

```
.section .text
.global load
.type load,@function

load:
	add a4, a0, zero
	add a2, a0, a1
	add a3, a0, zero
loop:	add a4, a3, a4
	addi a3, a3, 1
	blt a3, a2, loop
	add a0, a4,zero
	ret
```
Compile it using following commands:

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/92d9049e-5703-4d07-bf21-32d5ff6cb0ac)

  
</details>

<details><summary><strong>Lab 2 - Run C Program On RISC-V CPU</strong></summary>

Commands to be executed:

```
git clone https://github.com/kunalg123/riscv_workshop_collaterals.git
cd ~/riscv_workshop_collaterals/labs/
chmod 777 rv32im.sh
./rv32im.sh
```

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/add4782f-2748-406f-ba01-b074fdea39ff)



</details>











