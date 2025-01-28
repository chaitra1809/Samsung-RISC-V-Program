# Samsung-RISC-V-Program
Karnataka's RISC-V Skilled Workforce Powered by Samsung Semiconductor India Research ,Kunal Ghosh(VSD) &amp; Co.

##  Basic Details

**Name:** Chaitra Krishna Gouda  
**College:** DAYANANDA SAGAR COLLEGE OF ENGINEERING 

**Email ID:** chaitragouda0918@gmail.com
**GitHub Profile:** [chaitra1809](https://github.com/chaitra1809)  
**LinkedIN Profile:** [chaitra krishna gouda](https://www.linkedin.com/in/chaitra-krishna-gouda-286b682b3/)

----------------------------------------------------------------------------------------------------------------
##  INAUGURATION MEET
Inauguration meet on 6th Jan,2025.

Event Summary:
RISC-V Mission 2025 Powered by Samsung Semiconductor India Research in Collaboration with VLSI System Design

I am pleased and delighted to announce that we students of KARNATAKA are part of this remarkable initiative by Samsung Semiconductor India Research (SSIR) and VLSI System Design (VSD) under the RISC-V Mission 2025. This nation-building effort aims to create a skilled workforce of 1,000 RISC-V engineers across Karnataka, contributing to the vision of Digital India.
Here’s what makes this program a game-changer:
1. 6-Week Training Program: A focused, hands-on cohort designed to equip participants with practical knowledge in RISC-V and semiconductor technologies.
2. Perfect for Campus Aspirants: Specifically tailored for engineering students preparing for interviews, with a passion for entering the semiconductor industry.
3. FREE RISC-V Development Boards: VSD provides all participants with the right tools to empower innovation.

I sincerely thank Samsung Semiconductor India Research and VLSI System Design for giving us this incredible opportunity to explore and excel. This initiative inspires innovation and builds a strong foundation for students to become leaders in the semiconductor industry.
It’s an honour to contribute to this transformative mission and take a step toward becoming future RISC-V innovators.


------------------------------------------------------------------------------------------------------------------------------

# FIRST TASK 
Install this riscv tool chain on your machine. The labs related to first the above task will be shared over email. Complete this before the inauguration call on 6th Jan, 2025.

![image](https://github.com/user-attachments/assets/14a488f3-d020-40d0-9284-a7e524d1ad50)

 and further steps are attached as pdf.


**1. Install Ubuntu 20.04 LTS on Oracle Virtual Machine Box**

![image](https://github.com/user-attachments/assets/817643ac-f806-4a34-8786-b82df2f8c123)


![VirtualBox_vsdworkshop_07_01_2025_15_29_01](https://github.com/user-attachments/assets/0e938e95-5689-4607-873d-27b54b8d4a4d)



![risc](https://github.com/user-attachments/assets/68059e43-e90e-4055-ae0a-a41eca6b8b4d)

![image](https://github.com/user-attachments/assets/94142f25-b461-4f32-9cb6-ea314285bc2f)


![image](https://github.com/user-attachments/assets/312f05f9-1147-473a-a2b9-d05292c0b76d)



------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# THIRD TASK

RISCV Instruction types
--

There are 6 types of instruction types in RISC-V types
 1.  R-Type (Register Type)
 2.  I-Type (Immediate Type)
 3.  S-Type (Store Type)
 4.  U-Type (Branch Type)
 5.  B-Type (Upper Immediate Type)
 6.  J-Type (Jump Type)

In the base RV32I ISA, there are four core instruction formats (R/I/S/U), as shown in Base instruction formats. All are a fixed 32 bits in length.

![image](https://github.com/user-attachments/assets/47b33518-df07-42ce-9922-4530c16492e9)

1.R-Type:
--
![image](https://github.com/user-attachments/assets/6bcad23c-667d-4fa1-ba98-e5c6d82f3b12)

  This diagram represents the R-Type instruction format in the RISC-V Instruction Set       
    Architecture (ISA). R-Type instructions are typically used for register-to-register operations

1. Opcode (bits 6-0):

   The 7-bit opcode identifies the type of operation and the instruction format. For R-Type instructions, the opcode specifies that the instruction is register-based.

2. rd( bits 11:7):
   This bit is used for designation register where the output of the operation is written.
3. funct3( bits 14:12) :
   This 3 bit is used for differentiate between categories of operations within the same opcode.
   R type operations:

      
| **funct3** | **Operation**                      |
|------------|------------------------------------|
| `000`      | Add / Sub (depends on `funct7`)   |
| `001`      | Shift Left Logical (SLL)          |
| `010`      | Set Less Than (SLT)               |
| `011`      | Set Less Than Unsigned (SLTU)     |
| `100`      | XOR                               |
| `101`      | Shift Right (Logical/Arithmetic; depends on `funct7`) |
| `110`      | OR                                |
| `111`      | AND                               |

4. rs1(bits 19:15) :
 It specifies the first source register for the operation.
5. rs2(bits 24:20) :
 It specifies the second source register for the operation.
6. funct7(bits 31:25) :
 It provides additional differentiation between instructions that use the same opcode and fuct3.

Examples for R Type operation.  

| **funct7**  | **funct3** | **Operation**                        |
|-------------|------------|--------------------------------------|
| `0000000`   | `000`      | Add                                 |
| `0100000`   | `000`      | Sub                                 |
| `0000000`   | `001`      | Shift Left Logical (SLL)            |
| `0000000`   | `010`      | Set Less Than (SLT)                 |
| `0000000`   | `011`      | Set Less Than Unsigned (SLTU)       |
| `0000000`   | `100`      | XOR                                 |
| `0000000`   | `101`      | Shift Right Logical (SRL)           |
| `0100000`   | `101`      | Shift Right Arithmetic (SRA)        |
| `0000000`   | `110`      | OR                                  |
| `0000000`   | `111`      | AND                                 |

2.I-Type :
--
![image](https://github.com/user-attachments/assets/291e132c-afb6-46c2-a34c-9e46c2a845de)

I-Type instructions are used for operations involving immediate values, such as arithmetic with constants, memory access (e.g., loads), and control flow (e.g., jumps).

Breakdown of the Fields:
-
1. opcode( bits 6:0) :
 This 7 bits are used to identify the general operation type 
 
2. rd (bits 11:7) :
 It specifies the Destination register which is used to store the result of operation

3. funct3(bits 14:12) :
 It specifies the operation to perform such as load , immediate arthematic etc.,


4. rs1 (bits 19 :15 ) :
specifies the source register for the operation. For example, it provides the base address for memory instructions or a source operand for arithmetic operations.

5. imm[11:0] ( bits 31:20) :
 This 12-bit immediate value is sign-extended and used directly as part of the operation.
It serves as a constant operand for immediate operations or an offset for memory access.

Common I -Type instructions :
-
| **Instruction** | **opcode** | **funct3** | **Description**                       |
|-----------------|------------|------------|---------------------------------------|
| `addi`          | `0010011`  | `000`      | Add immediate to register (`rd = rs1 + imm`). |
| `slti`          | `0010011`  | `010`      | Set if less than immediate (signed). |
| `andi`          | `0010011`  | `111`      | Bitwise AND with immediate.          |
| `lw`            | `0000011`  | `010`      | Load word from memory.               |
| `lh`            | `0000011`  | `001`      | Load halfword from memory.           |
| `jalr`          | `1100111`  | `000`      | Jump and link register (indirect jump). |

3.S-Type:
-
![image](https://github.com/user-attachments/assets/e69f40bc-c431-4334-b77a-a5f1286a4431)

 S-Type instructions are primarily used for store operations, where data from a register is stored into memory at a specified address.

1. opcode (bits 6:0) :
 It identifies the general operation

2. imm[4:0] (bits 11:7) :
 Lower 5 bits of the 12-bit immediate (offset)

3. funct3 (bits 14:12) :
 specifies the type of store like word, byte,halfword etc.,

4. rs1 (bits 19 :15 ) :
 specifies the first source register for the operation.

5. rs2 (bits 24:20) :
 specifies the source register containing the value to be stored in memory.

6. imm[11:5] (bits 31:25) :
  Upper 7 bits of the 12-bit immediate (offset).

Common S-Type Instructions
-
| **Instruction** | **opcode**  | **funct3** | **Description**                      |
|-----------------|-------------|------------|--------------------------------------|
| `sw`           | `0100011`   | `010`      | Store Word (32-bit).                |
| `sh`           | `0100011`   | `001`      | Store Halfword (16-bit).            |
| `sb`           | `0100011`   | `000`      | Store Byte (8-bit).                 |

4.U-Type :
-
![image](https://github.com/user-attachments/assets/fca113b5-0577-4955-a24f-d5454a9aa0a6)

U-Type format is used for instructions like LUI (Load Upper Immediate) and AUIPC (Add Upper Immediate to PC)

1.opcode(bits 6:0) :
 It identifies the general operation

 1.opcode(bits 6:0) :
 It identifies the general operation

2.rd(bits 11:7) :
 It specifies the Destination register which is used to store the reult of the operation

3.imm[31:12] (bits 31:12) :
 20-bit immediate value (constant) used in the instruction. It is stored in the upper 20 bits of the target register.

5.B-Type:
-
![image](https://github.com/user-attachments/assets/f332980d-bbbd-47aa-9635-fdc77de1d97f)

B-Type instructions enable branching (jumping) to another location in the code, determined by the offset in the instruction.These instructions check specific conditions and branch (jump) to a target address if the condition is satisfied. If the condition is not met, the program continues with the next sequential instruction.

1.opcode(bits 6:0) :
 It identifies the general operation
 
2.imm[11] (bit 7) :
 Represents one of the middle bits of the immediate value.
 
3.imm[4:1] (bits 11:8) :
 Contributes the lower bits of the branch offset.

4.funct3 (bits 14:12) :
 specifies the branch condition that determines how the values in the source registers (rs1 and rs2) are compared.
 
5.rs1 (bits 19:15) :
 specifies the first source register for comparision
 
6.rs2 (bits 24:20) :
 specifies the second source register for comparision
 
7.imm[10:5] (bits 30:25) :
 Provides part of the branch offset.
These bits are directly concatenated to the rest of the immediate fields to form the full 12-bit offset.
 
8.imm[12] (bit 31) :
 Determines the sign of the branch offset.
If imm[12] is 1, the offset is negative (indicating a backward branch in memory).
If imm[12] is 0, the offset is positive (indicating a forward branch in memory).

funct3 examples in B-Type:

| **Instruction** | **`funct3` Value** | **Condition**                   |
|------------------|---------------------|----------------------------------|
| `BEQ`           | `000`              | Branch if `rs1 == rs2`.         |
| `BNE`           | `001`              | Branch if `rs1 != rs2`.         |
| `BLT`           | `100`              | Branch if `rs1 < rs2` (signed). |
| `BGE`           | `101`              | Branch if `rs1 >= rs2` (signed).|
| `BLTU`          | `110`              | Branch if `rs1 < rs2` (unsigned).|
| `BGEU`          | `111`              | Branch if `rs1 >= rs2` (unsigned).|

6.J-Type:
-
![image](https://github.com/user-attachments/assets/5fa4d127-0de3-45e7-8305-d116a979ebae)

J-Type instructions are used for unconditional jumps ,these are also  used for control flow, such as implementing function calls or jumping to a specific instruction

1.opcode(bits 6:0) :
 identifies the general operation

2.rd (bits 11:7) :
 Holds the return address (PC + 4), allowing the program to return to this location after completing the jump.

3.imm[19:12] (bits 19:12) :
 Bits 19 through 12 of the immediate value.
 4.imm[11] (bit 20) :
 Bit 11 of the intermediate Value

5.imm[10:1] (bits 30:21) :
 Bits 10 through 1 of the immediate value.

6.imm[20] (bit 31) :
 The 21st (MSB) bit of the 21-bit immediate (used for sign extension).

Common J-Type instructions:
-

| **Instruction** | **Opcode (Bits 6–0)** | **Registers** | **Description**                           |
|------------------|-----------------------|---------------|-------------------------------------------|
| `JAL`           | `1101111`            | `rd`          | Jump and Link: Save return address and jump to target address |


## 32-bit instructions from application (counterdown clock):

![15 instr](https://github.com/user-attachments/assets/025ed997-7162-426f-aa1a-eaac5449bad6)

1 . addi sp,sp -32
-
I-Type Instruction

imm[11:0] | rs1 | funct3 | rd | opcode

- *opcode* = 0010011
  
- *funct3* = 000 (addi)

- *rd* = x2 (sp)

- *rs1* = x2 (sp)

- *imm* = -32 (signed 12-bit: 111111111110)

32 - bit representation:

``11111111111000010 |  000  |   00010 |  0010011``

