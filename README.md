# RISC-V
This repository takes you through the RISC - V ISA. 

## Overview

**Day 1 - Introduction to RISC-V ISA And GNU compiler toolchain**
- [Installation](#installation)
- [Introduction](#introduction)
- [Integer Number Representation](#integer-number-representation)
- [Labwork](#labwork)

**Day 2 - Introduction to ABI and basic verification flow**
- [Application Binary Interface](#application-binary-interface)
- [Labs](#labs)

**Day 3 - Digital Logic with TL-Verilog and Makerchip**
- [Combinational logic in TL-Verilog using Makerchip](#combinational-logic-in-tl-verilog-using-makerchip)
- [Sequential Logic](#sequential-logic)
- [Pipelined Logic](#pipelined-logic)
- [Validity](#validity)
- [Wrap-up](#wrap-up)

**Day 4 - Basic RISC-V CPU micro-architecture**
- [Simple RISC-V Micro-architecture](#simple-risc-v-micro-architecture)
- [Fetch and Code](#fetch-and-code)
- [RISC-V Control Logic](#risc-v-control-logic)

**Day 5 - Complete Pipelined RISC-V CPU micro-architecture**
- [Pipeline Hazards](#pipeline-hazards)
- [Lab](#lab)
- [Final Implementation](#final-implementation)


## Day 1 - Introduction to RISC-V ISA And GNU compiler toolchain

## Installation
<details><summary>Steps For Installation</summary>
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


## Labs
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


## Day 3 - Digital Logic with TL-Verilog and Makerchip 
## Combinational logic in TL-Verilog using Makerchip
<details><summary><strong>Logic Gates</strong></summary>
<br>
Basic Gates:

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/810ed624-0fee-40e4-b729-28ae5cb8f680)

</details>

<details><summary><strong>Combinational Circuit</strong></summary>


![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/0a839b8a-40af-460a-bc64-517441f87bd3)

Boolean Operators:

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/66444f0e-2538-4ce1-8ada-07903da189cb)



 
</details>






<details><summary><strong>Labwork</strong></summary>
<details><summary><strong>Lab 1 : Maker Platform</strong></summary>

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/9e2310e3-c67b-494b-bb60-429f1d817cec)

	
</details>
<details><summary><strong>Lab 2 : Inverter</strong></summary>

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/341bc2b1-351b-4d01-a283-f29128155a97)


 
</details>
<details><summary><strong>Lab 3 : Vectors</strong></summary>

 ![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/1871521a-91f0-470d-8496-b9f4f5a9d871)

</details>

<details><summary><strong>Lab 4 : Mux</strong></summary>

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/08b46bd3-88ed-4a1f-a5d9-37c2e073aeb8)

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/5cdbd401-3beb-4341-ba9e-ad9b15be7ed5)



</details>

<details><summary><strong>Lab 5 : Combinational Calculator</strong></summary>

 ![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/cf99da17-7cc7-4013-9066-98d0870ee588)


</details>
</details>

## Sequential Logic
<details><summary><strong>Sequential Circuit</strong></summary>
A sequential circuit is a type of digital circuit that has memory and the ability to store and process information based on previous states. It contrasts with a combinational circuit, which doesn't have memory and processes information solely based on its current inputs.<br>
Sequential logic introduces a clock in the circuit as well as reset signal which is used to get all the flipflops into a known state.<br>
Example: D-Flip Flop

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/f88e3db6-c1e3-4238-9841-19dd06e4b70a)

	
</details>
<details><summary><strong>Labwork</strong></summary>

<details><summary><strong>Lab 1: Fibonacci Series</strong></summary>

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/9f996d41-8b2a-416d-af21-a64874a3ec42)


</details>


<details><summary><strong>Lab 2: Counter</strong></summary>

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/6018eacb-0cb8-452c-a19a-8b9548d47bb2)

</details>

<details><summary><strong>Lab 3: Sequential calculator</strong></summary>

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/d7885fbf-4168-4317-aa4a-6de6b9ac702d)


 
</details>


</details>



## Pipelined Logic

<details><summary><strong>Pipeling</strong></summary>
Pipelining refers to a technique used to improve the overall performance of a processor by allowing multiple instructions to overlap in execution. This enables the processor to achieve a higher instruction throughput and better utilization of its functional units.<br>

Let us understand through an example:

We will take the example of a pythagoras theorem. The simple pipelined structure for it is shown below:

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/bae1e5ba-e67c-42ea-ac3f-6e74ef56dab4)

We have divided it in three stages :
First is squaring of both the numbers, second includes the adding of numbers and third does the squareroot of the number.

The implementation of pipelining is shown below:

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/9dd45d85-b056-48f1-b85d-ed9db8669db5)

	
</details>


<details><summary><strong>Labwork</strong></summary>

<details><summary><strong>Lab 1 - Fibonacci Series</strong></summary>

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/0a9ceeba-4b2f-4178-86ab-8017c1c782a9)


 
</details>

<details><summary><strong>Lab 2 : Lab on Error Conditions with Computational Pipelining</strong></summary>

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/0fce58df-58a8-40fe-bdb9-34dc6f2d8674)


 
</details>

<details><summary><strong>Lab 3 : Counter And Calculator In Pipeline</strong></summary>


![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/25fe2fdb-edfe-4e6f-a270-f0f9a7b4b84e)

</details>

<details><summary><strong>Lab 4 : Cycle Calculator</strong></summary>

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/c64160f5-53f9-42e4-bb2a-d8b5729c5fd2)

	
</details>

 
</details>


## Validity
<details><summary><strong>Validity</strong></summary>
	<br>
"Validity" is a fundamental concept that helps describe communication between modules or components in a more intuitive way. The validity feature is used to represent whether the data being transmitted or processed is valid and should be considered meaningful by the receiving module.<br>
Valdity provides:
	
- Easier debug
- Cleaner design
- Better error checking
- Automated clock gating


**Clock Gating** 
<br>
Clock gating is a power-saving technique used in digital circuit design, including microprocessors and other integrated circuits, to reduce power consumption by selectively enabling or disabling clock signals to specific parts of a circuit. This technique is particularly effective in scenarios where parts of a circuit are idle or not actively performing computations.

- Clock gating avoids toggling clock signals.


**Example Of Validity On Pythagoras Theorem**

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/8f9894cb-117a-4c6a-9267-88f02c2d2a7e)

 
</details>

<details><summary><strong>Labwork</strong></summary>

<details><summary><strong>Lab 1: Distance Accumulator</strong></summary>

 
![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/2051abb0-5dea-4c6e-88e8-0476c3f84f59)


</details>

<details><summary><strong>Lab 2 : Cycle Calculator With Validity</strong></summary>

 ![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/d3eb0956-0b3b-4f84-b331-a2bb5141ca4d)

</details>


<details><summary><strong>Lab 3 : Calculator With Single Value Memory</strong></summary>

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/2a119482-d365-44b3-8795-00ad1b646eee)


</details>
</details>


## Wrap-up
<details><summary><strong>Labwork</strong></summary>
<details><summary><strong>Lab 1 : Conways's Game Of Life</strong></summary>
	
![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/8d2431ad-6a76-46c3-88fa-82cb1d1959e9)



</details>

 
</details>



## Day 4 - Basic RISC-V CPU micro-architecture
## Simple RISC-V Micro-architecture
<details><summary><strong>Micro-architecture Of Single Cycle RISC-V CPU</strong></summary>

The User-Level Simple RISC-V Microarchitecture is a basic design representing a simplified version of a RISC-V processor's core, catering to user-level instructions and operations. This microarchitecture provides a concise overview of the core components without delving into advanced features.

Components:

- Instruction Fetch (IF):
  - Fetches instructions from memory using the program counter (PC).
  - Increments the PC for the next instruction.
  - Passes the fetched instruction to the Decode stage.

- Instruction Decode (ID):
  - Decodes the fetched instruction to identify the operation and operands.
  - Determines the instruction type and control signals.
  - Sends control signals to relevant units.

- Register File (RF):
  - Contains general-purpose registers for temporary data storage.
  - Reads data from registers based on instruction operands.
  - Sends data to the Execute stage.

- Execution (EXE):
  - Performs basic arithmetic and logic operations.
  - Executes operations using the ALU.
  - Handles simple data manipulation tasks.

- Memory Access (MEM):
  - Manages load and store operations.
  - Calculates memory addresses and interacts with data memory.
  -  Handles simple memory transfers.

- Write Back (WB):
  - Writes results of operations back to registers.
  - Receives data from the Execute or Memory stage.
  - Updates destination registers.

**Example:**

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/dacf464f-89cb-4726-9c74-38936c1afe75)

 
</details>

## Fetch and Code
<details><summary><strong>Labwork</strong></summary>
<details><summary><strong>Lab 1 : PC</strong></summary>

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/878e6511-300e-4cc1-a4d6-c18878c5279d)


</details>

<details><summary><strong>Lab 2 : Fetch</strong></summary>

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/83220908-d87d-4de4-8110-df3bfd26f9ea)



![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/0a352288-09fa-4d1b-a38a-004626c34331)


 
</details>

<details><summary><strong>Lab 3 : Instruction Type Decoder</strong></summary>

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/071986ac-9e1a-4d67-957d-f976f8cc7dc6)


 
</details>

<details><summary><strong>Lab 4 : Instruction Immediate Decode</strong></summary>

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/f622d1e8-0038-4a52-8718-728cacd0449c)

	
</details>

<details><summary><strong>Lab 5 : Instruction Decode</strong></summary>

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/d6478989-0f7d-41db-bdd4-430a9503316e)

 
</details>

<details><summary><strong>Lab 6 : Instruction Field Decode</strong></summary>

**Decoder 1**

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/1d668bd6-49f8-443e-84d3-a6dadb1cbb19)

**Decoder 2**

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/127ce918-9998-48e2-ad1e-a2f7cb98e69d)


 
</details>

	
</details>


## RISC-V Control Logic



<details><summary><strong>Lab</strong></summary>

<details><summary><strong>Lab 1 : Register File Read</strong></summary>

 ![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/3eaa7e9c-99f0-4aff-9eec-cc32eced31de)


</details>

<details><summary><strong>Lab 2 : ALU</strong></summary>

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/7bdf2b13-ab74-4009-b222-a607f180be54)


 
</details>

<details><summary><strong>Lab 3 : Register File Write</strong></summary>

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/a20a6fda-9f68-46c5-969e-e08daeef6cbd)


</details>

<details><summary><strong>Lab 4 : Branch Instruction</strong></summary>

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/ecccb743-4d69-4457-9518-2f8d3e69f12e)

 
</details>


<details><summary><strong>Lab 5 : Testbench</strong></summary>

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/7393417b-d1bc-4daa-8637-bb61fbb85f10)


 
</details>

 
</details>



## Day 5 - Complete Pipelined RISC-V CPU micro-architecture

<details><summary><strong>Pipeline Hazards</strong></summary>
	
**Control Flow Hazards**  Control flow hazards occur when the sequence of instructions being executed is altered due to the outcome of a branch instruction (conditional jump or branch). In a pipelined processor, instructions are fetched and executed in stages, and the pipeline can be affected by branch instructions that change the program counter (PC), causing a misprediction in the instruction fetch stage.<br>
<br>
**Read-After-Write Hazards**     Read-after-write hazards occur when an instruction tries to read a data value from a register that is being written to by a previous instruction that has not yet completed. In a pipelined processor, instructions are executed in stages, and multiple instructions can be in different stages of execution simultaneously. If one instruction writes to a register and another instruction tries to read from the same register before the first instruction has completed writing, a hazard occurs.<br>
</details>



<details><summary><strong>Lab</strong></summary>
<details><summary><strong>Lab 1 : CYCLE VALID SIGNAL</strong></summary>

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/506e38c6-45b1-497c-991f-29b541821217)

</details>

<details><summary><strong>Lab 2 : Cycle RISC-V</strong></summary>

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/22fa652d-ab01-4b91-96e7-40d68e4f70cc)

 
</details>

<details><summary><strong>Lab 3 : Register File Bypass</strong></summary>

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/8d01e65d-068f-4505-9e2c-55659773707f)

 
</details>

<details><summary><strong>Lab 4 : Complete ALU Instruction</strong></summary>

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/ce9b5c3b-844a-471d-a2b2-d3b157d3555f)

 
</details>

<details><summary><strong>Lab 5 : Load Instruction</strong></summary>

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/f58787ad-72cd-495e-826b-1e1b9d22262b)


 
</details>

<details><summary><strong>Lab 6 : Load_store</strong></summary>

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/792910ec-1492-4112-97fa-ace6b73e16ba)

 
</details>
 
</details>




<details><summary><strong>Final Implementation</strong></summary>

![image](https://github.com/Nancy0192/RISC-V-ISA/assets/140998633/b96e3a13-8f78-418f-a8a0-aed18c53eedc)


**Code For Final RISC-V Core Processor**

```
\m4_TLV_version 1d: tl-x.org
\SV
   // This code can be found in: https://github.com/stevehoover/RISC-V_MYTH_Workshop
   
   m4_include_lib(['https://raw.githubusercontent.com/stevehoover/RISC-V_MYTH_Workshop/c1719d5b338896577b79ee76c2f443ca2a76e14f/tlv_lib/risc-v_shell_lib.tlv'])

\SV
   m4_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV

   // /====================\
   // | Sum 1 to 9 Program |
   // \====================/
   //
   // Program for MYTH Workshop to test RV32I
   // Add 1,2,3,...,9 (in that order).
   //
   // Regs:
   //  r10 (a0): In: 0, Out: final sum
   //  r12 (a2): 10
   //  r13 (a3): 1..10
   //  r14 (a4): Sum
   //
   // External to function:
   m4_asm(ADD, r10, r0, r0)             // Initialize r10 (a0) to 0.
   // Function:
   m4_asm(ADD, r14, r10, r0)            // Initialize sum register a4 with 0x0
   m4_asm(ADDI, r12, r10, 1010)         // Store count of 10 in register a2.
   m4_asm(ADD, r13, r10, r0)            // Initialize intermediate sum register a3 with 0
   // Loop:
   m4_asm(ADD, r14, r13, r14)           // Incremental addition
   m4_asm(ADDI, r13, r13, 1)            // Increment intermediate register by 1
   m4_asm(BLT, r13, r12, 1111111111000) // If a3 is less than a2, branch to label named <loop>
   m4_asm(ADD, r10, r14, r0)            // Store final result to register a0 so that it can be read by main program
   m4_asm(SW, r0, r10, 10000)           // Store the final result value to byte address 16
   m4_asm(LW, r15, r0, 10000)           // Load the final result value from adress 16 to x17
   
   // Optional:
   // m4_asm(JAL, r7, 00000000000000000000) // Done. Jump to itself (infinite loop). (Up to 20-bit signed immediate plus implicit 0 bit (unlike JALR) provides byte address; last immediate bit should also be 0)
   m4_define_hier(['M4_IMEM'], M4_NUM_INSTRS)


   |cpu
      @0
         $reset = *reset;
         
         //MODIFIED NEXT PC LOGIC FOR INCLUDING BRANCH INSTRCUTIONS
         $pc[31:0] = >>1$reset ? 32'b0 :
                     >>3$valid_taken_branch ? >>3$br_target_pc :
                     >>3$valid_load ? >>3$inc_pc :
                     >>3$valid_jump && >>3$is_jal ? >>3$br_target_pc :
                     >>3$valid_jump && >>3$is_jalr ? >>3$jalr_target_pc :
                     >>1$inc_pc ;
         //START LOGIC TO PROVIDE FIRST VALID LOGIC
         //$start = (>>1$reset && $reset == 0) ? 1'b1 : 1'b0;
         //$valid = $reset ? 1'b0 :
                  //$start ? 1'b1 : >>3$valid;
     
      @1  
         //INSTRUCTION FETCH
         $inc_pc[31:0] = $pc + 32'd4;
         
         $imem_rd_en = !$reset;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         
         $instr[31:0] = $imem_rd_data[31:0];
         
         //INSTRUCTION TYPES DECODE        
         
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         
         $is_r_instr = $instr[6:2] ==? 5'b011x0 ||
                       $instr[6:2] ==? 5'b01011 ||
                       $instr[6:2] ==? 5'b10100;
         
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                       $instr[6:2] ==? 5'b001x0 ||
                       $instr[6:2] ==? 5'b11001;
         
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         
         //INSTRUCTION IMMEDIATE DECODE
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                      $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                      $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                      $is_u_instr ? {$instr[31:12], 12'b0} :
                      $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                                            32'b0;
         //INSTRUCTION DECODE
         $opcode[6:0] = $instr[6:0];
         
         
         //INSTRUCTION FIELD DECODE
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
           
         $rs1_valid = $is_r_instr  || $is_s_instr || $is_b_instr || $is_i_instr;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         
         $funct3_valid = $is_r_instr  || $is_s_instr || $is_b_instr || $is_i_instr;
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
           
         $funct7_valid = $is_r_instr ;
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
           
         $rd_valid = $is_r_instr  || $is_u_instr || $is_j_instr || $is_i_instr;
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         
         
      @2
         //INSTRUCTION DECODE
         $dec_bits[10:0] = {$funct7[5],$funct3,$opcode};
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
         $is_lui = $dec_bits ==? 11'bx_xxx_0110111;
         $is_auipc = $dec_bits ==? 11'bx_xxx_0010111;
         $is_jal = $dec_bits ==? 11'bx_xxx_1101111;
         $is_jalr = $dec_bits ==? 11'bx_000_1100111;
         $is_load = $opcode == 7'b0000011;
         $is_sb = $dec_bits ==? 11'bx_000_0100011;
         $is_sh = $dec_bits ==? 11'bx_001_0100011;
         $is_sw = $dec_bits ==? 11'bx_010_0100011;
         $is_slti = $dec_bits ==? 11'bx_010_0010011;
         $is_sltiu = $dec_bits ==? 11'bx_011_0100011;
         $is_xori = $dec_bits ==? 11'bx_100_0100011;
         $is_ori = $dec_bits ==? 11'bx_110_0100011;
         $is_andi = $dec_bits ==? 11'bx_111_0100011;
         $is_slli = $dec_bits ==? 11'b0_001_0100011;
         $is_srli = $dec_bits ==? 11'b0_101_0100011;
         $is_srai = $dec_bits ==? 11'b1_101_0100011;
         $is_sub = $dec_bits ==? 11'b1_000_0110011;
         $is_sll = $dec_bits ==? 11'b0_001_0110011;
         $is_slt = $dec_bits ==? 11'b0_010_0110011;
         $is_sltu = $dec_bits ==? 11'b0_011_0110011;
         $is_xor = $dec_bits ==? 11'b0_100_0110011;
         $is_srl = $dec_bits ==? 11'b0_101_0110011;
         $is_sra = $dec_bits ==? 11'b1_101_0110011;
         $is_or = $dec_bits ==? 11'b0_110_0110011;
         $is_and = $dec_bits ==? 11'b0_111_0110011;
         
         $jalr_target_pc[31:0] = $src1_value +$imm ;
      @3
         $is_jump = $is_jal || $is_jalr ;   
         `BOGUS_USE($is_beq $is_bne $is_blt $is_bge $is_bltu $is_bgeu $is_addi $is_add
                    $is_lui $is_auipc $is_jal $is_jalr $is_load $is_sb $is_sh $is_sw $is_slti
                    $is_sltiu $is_xori $is_ori $is_andi $is_slli $is_srli $is_srai $is_sub $is_sll
                    $is_slt $is_sltu $is_xor $is_srl $is_sra $is_or $is_and)
         
      @2  
         //REGISTER FILE READ
         //$rf_wr_en = 1'b0;
         //$rf_wr_index[4:0] = 5'b0;
         //$rf_wr_data[31:0] = 32'b0;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         
         $src1_value[31:0] = >>1$rf_wr_en && (>>1$rf_wr_index == $rf_rd_index1) ? >>1$result : $rf_rd_data1;
         $src2_value[31:0] = >>1$rf_wr_en && (>>1$rf_wr_index == $rf_rd_index2) ? >>1$result : $rf_rd_data2;
         $br_target_pc[31:0] = $pc +$imm;
         
      @3  
         //ARITHMETIC AND LOGIC UNIT (ALU)
         
         $sltu_rslt[31:0] = $src1_value < $src2_value;
         $sltiu_rslt[31:0] = $src1_value < $imm;
         $result[31:0] = $is_addi ? $src1_value + $imm :
                         $is_add ? $src1_value + $src2_value :
                         $is_andi ? $src1_value & $imm :
                         $is_ori ? $src1_value | $imm :
                         $is_xori ? $src1_value ^ $imm :
                         $is_slli ? $src1_value << $imm[5:0] :
                         ($is_addi || $is_load || $is_s_instr) ? $src1_value + $imm :
                         $is_srli ? $src1_value >> $imm[5:0] :
                         $is_and ? $src1_value & $src2_value :
                         $is_or ? $src1_value | $src2_value :
                         $is_xor ? $src1_value ^ $src2_value :
                         $is_sub ? $src1_value - $src2_value :
                         $is_sll ? $src1_value << $src2_value[4:0] :
                         $is_srl ? $src1_value >> $src2_value[4:0] :
                         $is_sltu ? $sltu_rslt :
                         $is_sltiu ? $sltiu_rslt :
                         $is_lui ? {$imm[31:12],12'b0} :
                         $is_auipc ? $pc + $imm :
                         $is_jal ? $pc + 4 :
                         $is_jalr ? $pc + 4 :
                         $is_srai ? { {32{$src1_value[31]}},$src1_value} >> $imm[4:0] :
                         $is_slt ? ($src1_value[31] == $src2_value[31]) ? $sltu_rslt : {31'b0,$src1_value[31]} :
                         $is_slti ? ($src1_value[31] == $imm[31]) ? $sltiu_rslt : {31'b0,$src1_value[31]} :
                         $is_sra ? { {32{$src1_value[31]}},$src1_value} >> $src2_value[4:0] :
                         32'bx;
         
         
         //REGISTER FILE WRITE
         $rf_wr_en = ($rd_valid && $rd != 5'b0 && $valid) || >>2$valid_load;
         $rf_wr_index[4:0] = >>2$valid_load ? >>2$rd : $rd;
         $rf_wr_data[31:0] = >>2$valid_load ? >>2$ld_data : $result;
         
         
         //BRANCH INSTRUCTIONS 1
         $taken_branch = $is_beq ? ($src1_value == $src2_value):
                         $is_bne ? ($src1_value != $src2_value):
                         $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])):
                         $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])):
                         $is_bltu ? ($src1_value < $src2_value):
                         $is_bgeu ? ($src1_value >= $src2_value):
                         1'b0;
          //CYCLE VALID INSTRUCTIONS
         $valid = !(>>1$valid_taken_branch || >>2$valid_taken_branch ||
                    >>1$valid_load || >>2$valid_load) ;
         
         $valid_load = $valid && $is_load ;
         //$valid = !(>>1$valid_taken_branch || >>2$valid_taken_branch);
         $valid_taken_branch = $valid && $taken_branch;
         $valid_jump = $is_jump && $valid ;
         `BOGUS_USE($taken_branch)
      @4
         //MINI 1-R/W MEMORY
         $dmem_wr_en = $is_s_instr && $valid ;
         $dmem_addr[3:0] = $result[5:2] ;
         $dmem_wr_data[31:0] = $src2_value ;
         $dmem_rd_en = $is_load ;
         
      @5
         //LOAD DATA
         $ld_data[31:0] = $dmem_rd_data ;   
         
         
         

      // Note: Because of the magic we are using for visualisation, if visualisation is enabled below,
      //       be sure to avoid having unassigned signals (which you might be using for random inputs)
      //       other than those specifically expected in the labs. You'll get strange errors for these.

   
   // Assert these to end simulation (before Makerchip cycle limit).
   //*passed = *cyc_cnt > 40;
   *passed = |cpu/xreg[15]>>5$value == (1+2+3+4+5+6+7+8+9) ;
   *failed = 1'b0;
   
   // Macro instantiations for:
   //  o instruction memory
   //  o register file
   //  o data memory
   //  o CPU visualization
   |cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@2, @3)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+dmem(@4)    // Args: (read/write stage)
   
   m4+viz(@4)    // For visualisation, argument should be at least equal to the last stage of CPU logic
   //@4 would work for all lab
\SV
   endmodule
```
</details>





