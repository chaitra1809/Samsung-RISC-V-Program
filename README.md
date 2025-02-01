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

# SECOND TASK:

-O1 and -Ofast 
-
The `-O1` and `-Ofast` options in the context of compiling C code with RISC-V (or any GCC-compatible compiler) control the level and type of optimizations applied during the compilation process

In the case of `-O1` it  focus  A moderate level of optimization that aims to improve code performance while keeping compilation times and memory usage reasonable.

In the case of `-Ofast` it focus  Aggressively optimizes for maximum performance, often at the expense of strict adherence to the language standard and longer compilation times.

The implementation of the neural network-based branch predictor in C:
-

```c
#include <stdio.h>
#include <stdlib.h>

#define INPUT_SIZE 5
#define HIDDEN_SIZE 3
#define OUTPUT_SIZE 1
#define EPOCHS 10000
#define LEARNING_RATE 0.1

// Custom approximation of the exponential function
double custom_exp(double x) {
    double result = 1.0;
    double term = 1.0;
    for (int i = 1; i < 20; i++) {  // Use 20 terms for better approximation
        term *= x / i;
        result += term;
    }
    return result;
}

// Activation function (Sigmoid)
double sigmoid(double x) {
    return 1.0 / (1.0 + custom_exp(-x));
}

// Derivative of Sigmoid
double sigmoid_derivative(double x) {
    return x * (1.0 - x);
}

// Initialize weights and biases randomly
void initialize(double weights_in[HIDDEN_SIZE][INPUT_SIZE], double weights_out[OUTPUT_SIZE][HIDDEN_SIZE], 
                double bias_hidden[HIDDEN_SIZE], double bias_output[OUTPUT_SIZE]) {
    for (int i = 0; i < HIDDEN_SIZE; i++) {
        for (int j = 0; j < INPUT_SIZE; j++) {
            weights_in[i][j] = (double)rand() / RAND_MAX;
        }
        bias_hidden[i] = (double)rand() / RAND_MAX;
    }

    for (int i = 0; i < OUTPUT_SIZE; i++) {
        for (int j = 0; j < HIDDEN_SIZE; j++) {
            weights_out[i][j] = (double)rand() / RAND_MAX;
        }
        bias_output[i] = (double)rand() / RAND_MAX;
    }
}

// Forward pass
void forward(double input[INPUT_SIZE], double weights_in[HIDDEN_SIZE][INPUT_SIZE], double bias_hidden[HIDDEN_SIZE],
             double hidden[HIDDEN_SIZE], double weights_out[OUTPUT_SIZE][HIDDEN_SIZE], 
             double bias_output[OUTPUT_SIZE], double output[OUTPUT_SIZE]) {
    // Hidden layer computation
    for (int i = 0; i < HIDDEN_SIZE; i++) {
        hidden[i] = bias_hidden[i];
        for (int j = 0; j < INPUT_SIZE; j++) {
            hidden[i] += input[j] * weights_in[i][j];
        }
        hidden[i] = sigmoid(hidden[i]);
    }

    // Output layer computation
    for (int i = 0; i < OUTPUT_SIZE; i++) {
        output[i] = bias_output[i];
        for (int j = 0; j < HIDDEN_SIZE; j++) {
            output[i] += hidden[j] * weights_out[i][j];
        }
        output[i] = sigmoid(output[i]);
    }
}

// Backward pass (Training)
void backward(double input[INPUT_SIZE], double weights_in[HIDDEN_SIZE][INPUT_SIZE], double bias_hidden[HIDDEN_SIZE],
              double hidden[HIDDEN_SIZE], double weights_out[OUTPUT_SIZE][HIDDEN_SIZE], double bias_output[OUTPUT_SIZE], 
              double output[OUTPUT_SIZE], double target[OUTPUT_SIZE]) {
    double output_error[OUTPUT_SIZE], hidden_error[HIDDEN_SIZE];

    // Calculate output error
    for (int i = 0; i < OUTPUT_SIZE; i++) {
        output_error[i] = (target[i] - output[i]) * sigmoid_derivative(output[i]);
    }

    // Calculate hidden layer error
    for (int i = 0; i < HIDDEN_SIZE; i++) {
        hidden_error[i] = 0.0;
        for (int j = 0; j < OUTPUT_SIZE; j++) {
            hidden_error[i] += output_error[j] * weights_out[j][i];
        }
        hidden_error[i] *= sigmoid_derivative(hidden[i]);
    }

    // Update weights and biases (Output layer)
    for (int i = 0; i < OUTPUT_SIZE; i++) {
        for (int j = 0; j < HIDDEN_SIZE; j++) {
            weights_out[i][j] += LEARNING_RATE * output_error[i] * hidden[j];
        }
        bias_output[i] += LEARNING_RATE * output_error[i];
    }

    // Update weights and biases (Input to Hidden layer)
    for (int i = 0; i < HIDDEN_SIZE; i++) {
        for (int j = 0; j < INPUT_SIZE; j++) {
            weights_in[i][j] += LEARNING_RATE * hidden_error[i] * input[j];
        }
        bias_hidden[i] += LEARNING_RATE * hidden_error[i];
    }
}

// Main function
int main() {
    // Define network parameters
    double weights_in[HIDDEN_SIZE][INPUT_SIZE], weights_out[OUTPUT_SIZE][HIDDEN_SIZE];
    double bias_hidden[HIDDEN_SIZE], bias_output[OUTPUT_SIZE];
    double hidden[HIDDEN_SIZE], output[OUTPUT_SIZE];

    // Initialize network
    initialize(weights_in, weights_out, bias_hidden, bias_output);

    // Define training data
    double inputs[4][INPUT_SIZE] = {
        {1, 0, 1, 1, 0},  // Example historical branch patterns
        {0, 1, 1, 0, 1},
        {1, 1, 0, 1, 0},
        {0, 0, 0, 1, 1}
    };
    double targets[4][OUTPUT_SIZE] = {
        {1},  // Branch taken
        {0},  // Branch not taken
        {1},  // Branch taken
        {0}   // Branch not taken
    };

    // Train the network
    for (int epoch = 0; epoch < EPOCHS; epoch++) {
        for (int i = 0; i < 4; i++) {
            forward(inputs[i], weights_in, bias_hidden, hidden, weights_out, bias_output, output);
            backward(inputs[i], weights_in, bias_hidden, hidden, weights_out, bias_output, output, targets[i]);
        }
    }

    // Test the network
    double test_input[INPUT_SIZE] = {0, 1, 0, 1, 1};
    //double test_input[INPUT_SIZE] ={1, 0, 1, 1, 0};
    forward(test_input, weights_in, bias_hidden, hidden, weights_out, bias_output, output);
    printf("Prediction for input {0, 1, 0, 1, 1}: %.2f\n", output[0]);
    //printf("Prediction for input {1, 0, 1, 1, 0}: %.2f\n", output[0]);
    //printf("Prediction for input : %.2f\n", output[0]);
    printf("%s\n", output[0] >= 0.5 ? "Branch Taken" : "Branch Not Taken");
    
    return 0;
}
```

---

####  Compile the C code using GCC compiler
  ```
  $ gcc bpnn.c
  $ ./a.out
  ```
![task1pic1](https://github.com/user-attachments/assets/e29b6be4-fcc6-43b6-873a-242241e0b11a)

---

####  Compile the C code using the RISC-V compiler ( -O1)
  ```
  $ riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o bpnn.o bpnn.c
  $ ls -ltr bpnn.o
  ```
![task2pic2](https://github.com/user-attachments/assets/dd4e62ac-7fee-4034-aeb3-0a3d69c166f9)

---

####  Inspect the Assembly Code for the Main Function (-O1)
   ```
   $ riscv64-unknown-elf-objdump -d bpnn.o | less
   ```
![task2pic3](https://github.com/user-attachments/assets/3b9cdfc3-c2bb-4891-9cd7-66ae7b0a06c2)

---

####  Compile the C code using the RISC-V compiler (-Ofast) 
  ```
  $ riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o bpnn.o bpnn.c
  ```
![task2pic4](https://github.com/user-attachments/assets/44512c5a-b8b8-4c19-8bf3-d862352252be)

---

####  Inspect the Assembly Code for the Main Function (-Ofast)
  ```
  $ riscv64-unknown-elf-objdump -d bpnn.o | less
  ```
![task2pic5](https://github.com/user-attachments/assets/fc8e6b90-40fe-4d98-bd46-318af0838088)

---

####  Observe the ouput given by RISC V Compiler
  ```
  $ spike pk bpnn.o
  ```
![task2pic6](https://github.com/user-attachments/assets/0786e303-e551-4deb-af24-81f7e83c8e4c)

---

####  Inspect the Stack pointer in the  Assembly Code of the Main Function (-Ofast)
  ```
  $ riscv64-unknown-elf-objdump -d bpnn.o | less
  ```
![task2pic7](https://github.com/user-attachments/assets/9d91196d-f9fa-4fbb-bb1f-9347ad47a02e)

---

####  Debug the C code compiled by RISC V Compiler using spike command by inspecting the stack pointer
  ```
  $ spike -d pk bpnn.o
  ```
![task2pic8](https://github.com/user-attachments/assets/20470995-d3b2-415b-88a7-8e810bb4af90)

---

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
    ![WhatsApp Image ](https://github.com/user-attachments/assets/62d18328-66d8-461d-91f5-af4d9991ec49)

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

![image](https://github.com/user-attachments/assets/3e567cf2-00eb-4711-b30e-c760c5402fc4)



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
![WhatsApp Image ](https://github.com/user-attachments/assets/c330e2d7-7bb2-4de2-adf2-5df40744aa8a)

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

![WhatsApp Image](https://github.com/user-attachments/assets/27904b7f-6048-4e82-855d-d7ed5ec24260)

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

![WhatsApp Image ](https://github.com/user-attachments/assets/4c8c579e-7866-460b-bf88-f5c4b0ed3e33)

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

![WhatsApp Image](https://github.com/user-attachments/assets/7a90011d-b24e-452c-9063-2a1d51181c5d)

---


## Encoding Branch Prediction Using a Neural Network Application Instructions

### **1. addi sp, sp, -496**

For the instruction `addi sp, sp, -496`:

| **Bit**       | **31-20**       | **19-15** | **14-12** | **11-7**  | **6-0**   |
|---------------|-----------------|-----------|-----------|-----------|-----------|
| **Field**     | imm[11:0]       | rs1 (sp)  | funct3    | rd (sp)   | opcode    |
| **Value**     | 111111111000    | 00010     | 000       | 00010     | 0010011   |

#### **Explanation of Fields:**
- **imm[11:0]**: `-496` is represented as `111111111000` (12-bit sign-extended immediate).  
- **rs1**: `sp` is register `x2`, encoded as `00010`.  
- **funct3**: `000` indicates an `addi` operation.  
- **rd**: `sp` is register `x2`, encoded as `00010`.  
- **opcode**: `0010011` is the opcode for immediate arithmetic instructions.

#### **32-bit Representation:**
`111111111000 00010 000 00010 0010011`  
**Hexadecimal Representation:** `0xFFF10213`

---

### **2. sd ra, 488(sp)**

For the instruction `sd ra, 488(sp)`:

| **Bit**       | **31-25**       | **24-20** | **19-15** | **14-12** | **11-7**  | **6-0**   |
|---------------|-----------------|-----------|-----------|-----------|-----------|-----------|
| **Field**     | imm[11:5]       | rs2 (ra)  | rs1 (sp)  | funct3    | imm[4:0]  | opcode    |
| **Value**     | 0111100         | 00001     | 00010     | 011       | 01000     | 0100011   |

#### **Explanation of Fields:**
- **imm[11:5]**: Upper 7 bits of `488` (`1111000` in binary), encoded as `0111100`.  
- **rs2**: `ra` is register `x1`, encoded as `00001`.  
- **rs1**: `sp` is register `x2`, encoded as `00010`.  
- **funct3**: `011` indicates a `sd` operation.  
- **imm[4:0]**: Lower 5 bits of `488` (`1111000` in binary), encoded as `01000`.  
- **opcode**: `0100011` is the opcode for store instructions.

#### **32-bit Representation:**
`0111100 00001 00010 011 01000 0100011`  
**Hexadecimal Representation:** `0x3E825023`

---

### **3. sd s0, 480(sp)**

For the instruction `sd s0, 480(sp)`:

| **Bit**       | **31-25**       | **24-20** | **19-15** | **14-12** | **11-7**  | **6-0**   |
|---------------|-----------------|-----------|-----------|-----------|-----------|-----------|
| **Field**     | imm[11:5]       | rs2 (s0)  | rs1 (sp)  | funct3    | imm[4:0]  | opcode    |
| **Value**     | 0111000         | 00000     | 00010     | 011       | 00000     | 0100011   |

#### **Explanation of Fields:**
- **imm[11:5]**: Upper 7 bits of `480` (`1111000` in binary), encoded as `0111000`.  
- **rs2**: `s0` is register `x8`, encoded as `01000`.  
- **rs1**: `sp` is register `x2`, encoded as `00010`.  
- **funct3**: `011` indicates a `sd` operation.  
- **imm[4:0]**: Lower 5 bits of `480` (`1110000` in binary), encoded as `00000`.  
- **opcode**: `0100011` is the opcode for store instructions.

#### **32-bit Representation:**
`0111000 01000 00010 011 00000 0100011`  
**Hexadecimal Representation:** `0x3A802023`

---

### **4. sd s1, 472(sp)**

For the instruction `sd s1, 472(sp)`:

| **Bit**       | **31-25**       | **24-20** | **19-15** | **14-12** | **11-7**  | **6-0**   |
|---------------|-----------------|-----------|-----------|-----------|-----------|-----------|
| **Field**     | imm[11:5]       | rs2 (s1)  | rs1 (sp)  | funct3    | imm[4:0]  | opcode    |
| **Value**     | 0111000         | 00001     | 00010     | 011       | 00000     | 0100011   |

#### **Explanation of Fields:**
- **imm[11:5]**: Upper 7 bits of `472` (`1110100` in binary), encoded as `0111000`.  
- **rs2**: `s1` is register `x9`, encoded as `01001`.  
- **rs1**: `sp` is register `x2`, encoded as `00010`.  
- **funct3**: `011` indicates a `sd` operation.  
- **imm[4:0]**: Lower 5 bits of `472` (`1110000` in binary), encoded as `00000`.  
- **opcode**: `0100011` is the opcode for store instructions.

#### **32-bit Representation:**
`0111000 01001 00010 011 00000 0100011`  
**Hexadecimal Representation:** `0x3A902023`

---

### **5. sd s2, 464(sp)**

For the instruction `sd s2, 464(sp)`:

| **Bit**       | **31-25**       | **24-20** | **19-15** | **14-12** | **11-7**  | **6-0**   |
|---------------|-----------------|-----------|-----------|-----------|-----------|-----------|
| **Field**     | imm[11:5]       | rs2 (s2)  | rs1 (sp)  | funct3    | imm[4:0]  | opcode    |
| **Value**     | 0111000         | 00010     | 00010     | 011       | 00000     | 0100011   |

#### **Explanation of Fields:**
- **imm[11:5]**: Upper 7 bits of `464` (`1110100` in binary), encoded as `0111000`.  
- **rs2**: `s2` is register `x18`, encoded as `10010`.  
- **rs1**: `sp` is register `x2`, encoded as `00010`.  
- **funct3**: `011` indicates a `sd` operation.  
- **imm[4:0]**: Lower 5 bits of `464` (`1110000` in binary), encoded as `00000`.  
- **opcode**: `0100011` is the opcode for store instructions.

#### **32-bit Representation:**
`0111000 10010 00010 011 00000 0100011`  
**Hexadecimal Representation:** `0x3A928023`

---


## Task 4

### Functional simulation of the given design code of pipelined RISC V 32I Processor

#### Initial steps

- Both design and testbench codes are saved in a separate folder
- To simulate the verilog code
```
$ iverilog -o iiitb_rv32i iiitb_rv32i.v iiitb_rv32i_tb.v
$ ./iiitb_rv32i
```

- To open the dumped vcd file
```
$ gtkwave iiitb_rv32i.vcd
```

![task4pic1](https://github.com/user-attachments/assets/c1dba9ef-1fdd-4c76-8024-1f3dc78382f5)

---

### Analayzing the hex code given by the designer in the instruction memory

| **Program**                  | **Hex Code**     | **Assembly Code**       |
|------------------------------|------------------|--------------------------|
| MEM[0] <= 32'h02208300;      | 02208300         | add r6, r1, r2          |
| MEM[1] <= 32'h02209380;      | 02209380         | sub r7, r1, r2          |
| MEM[2] <= 32'h0230a400;      | 0230a400         | and r8, r1, r3          |
| MEM[3] <= 32'h02513480;      | 02513480         | or r9, r2, r5           |
| MEM[4] <= 32'h0240c500;      | 0240c500         | xor r10, r1, r4         |
| MEM[5] <= 32'h02415580;      | 02415580         | slt r11, r2, r4         |
| MEM[6] <= 32'h00520600;      | 00520600         | addi r12, r4, 5         |
| MEM[7] <= 32'h00209181;      | 00209181         | sw r3, 2(r1)            |
| MEM[8] <= 32'h00208681;      | 00208681         | lw r13, 2(r1)           |
| MEM[9] <= 32'h00f00002;      | 00f00002         | beq r0, r0, 15          |
| MEM[25] <= 32'h00210700;     | 00210700         | add r14, r2, r2         |

### Verifying each instructions using the waveform

Value of general purpose registers before running the program (As per the design code)

| **Register** | **Value (Hex)** | **Value (Decimal)** |
|--------------|------------------|----------------------|
| REG[0]       | 0x00000000       | 0                   |
| REG[1]       | 0x00000001       | 1                   |
| REG[2]       | 0x00000002       | 2                   |
| REG[3]       | 0x00000003       | 3                   |
| REG[4]       | 0x00000004       | 4                   |
| REG[5]       | 0x00000005       | 5                   |
| REG[6]       | 0x00000006       | 6                   | 

## Instruction 1: add r6, r1, r2  

![in1](https://github.com/user-attachments/assets/0362eedf-8249-4b89-b252-fa5d375548f7)

- REG[6] = REG[1] + REG[2] = 1 + 2 = 3
- 
| **Register** | **Value (Hex)** | **Value (Decimal)** |
|--------------|------------------|----------------------|
| REG[0]       | 0x00000000       | 0                   |
| REG[1]       | 0x00000001       | 1                   |
| REG[2]       | 0x00000002       | 2                   |
| REG[3]       | 0x00000003       | 3                   |
| REG[4]       | 0x00000004       | 4                   |
| REG[5]       | 0x00000005       | 5                   |
| REG[6]       | 0x00000003       | 3                   |


## Instruction 2: sub r7, r1, r2

![in2](https://github.com/user-attachments/assets/8cbfe1b1-4933-411c-948d-1f1b7e20c60e)

- REG[7] = REG[1] - REG[2] = 1 - 2 = -1
- 
| **Register** | **Value (Hex)** | **Value (Decimal)** |
|--------------|------------------|----------------------|
| REG[0]       | 0x00000000       | 0                   |
| REG[1]       | 0x00000001       | 1                   |
| REG[2]       | 0x00000002       | 2                   |
| REG[3]       | 0x00000003       | 3                   |
| REG[4]       | 0x00000004       | 4                   |
| REG[5]       | 0x00000005       | 5                   |
| REG[6]       | 0x00000003       | 3                   |
| REG[7]       | 0xFFFFFFFF       | -1                  |


## Instruction 3: and r8, r1, r3

![in3](https://github.com/user-attachments/assets/aa25ca12-7163-44de-ad97-6939daee59d3)

- REG[8] = REG[1] AND REG[3] = 1 AND 3 = 01 AND 11 = 01 = 1 (decimal)  

| **Register** | **Value (Hex)** | **Value (Decimal)** |
|--------------|------------------|----------------------|
| REG[0]       | 0x00000000       | 0                   |
| REG[1]       | 0x00000001       | 1                   |
| REG[2]       | 0x00000002       | 2                   |
| REG[3]       | 0x00000003       | 3                   |
| REG[4]       | 0x00000004       | 4                   |
| REG[5]       | 0x00000005       | 5                   |
| REG[6]       | 0x00000003       | 3                   |
| REG[7]       | 0xFFFFFFFF       | -1                  |
| REG[8]       | 0x00000001       | 1                   |


## Instruction 4: or r9, r2, r5

![in4](https://github.com/user-attachments/assets/718af532-02c0-45b6-8d9e-a4901b59260d)

- REG[9] = REG[2] OR REG[5] = 2 OR 5 = 010 OR 101 = 111 = 7 (decimal)
  
| **Register** | **Value (Hex)** | **Value (Decimal)** |
|--------------|------------------|----------------------|
| REG[0]       | 0x00000000       | 0                   |
| REG[1]       | 0x00000001       | 1                   |
| REG[2]       | 0x00000002       | 2                   |
| REG[3]       | 0x00000003       | 3                   |
| REG[4]       | 0x00000004       | 4                   |
| REG[5]       | 0x00000005       | 5                   |
| REG[6]       | 0x00000003       | 3                   |
| REG[7]       | 0xFFFFFFFF       | -1                  |
| REG[8]       | 0x00000001       | 1                   |
| REG[9]       | 0x00000007       | 7                   |


## Instruction 5: xor r10, r1, r4 

![in5](https://github.com/user-attachments/assets/284d60d7-5552-4977-b6dc-551714604ad8)

- REG[10] = REG[1] XOR REG[4] = 1 XOR 4 = 001 OR 100 = 101 = 5 (decimal) 

| **Register** | **Value (Hex)** | **Value (Decimal)** |
|--------------|------------------|----------------------|
| REG[0]       | 0x00000000       | 0                   |
| REG[1]       | 0x00000001       | 1                   |
| REG[2]       | 0x00000002       | 2                   |
| REG[3]       | 0x00000003       | 3                   |
| REG[4]       | 0x00000004       | 4                   |
| REG[5]       | 0x00000005       | 5                   |
| REG[6]       | 0x00000003       | 3                   |
| REG[7]       | 0xFFFFFFFF       | -1                  |
| REG[8]       | 0x00000001       | 1                   |
| REG[9]       | 0x00000007       | 7                   |
| REG[10]      | 0x00000005       | 5                   |


## Task 5

**Interfacing VSDSquadron Mini (CH32V003F4U6) and Raspberry Pi Pico (RP2040)**  

---

### Components Required 
1. VSDSquadron Mini (CH32V003F4U6)    
2. Raspberry Pi Pico (RP2040)  
3. Connecting Wires
4. Bread Board
5. Power Supply   

---

### Software Required  
1. Arduino IDE
2. Thonny
   
---

### Raspberry Pi Pico Pin diagram

![image](https://github.com/user-attachments/assets/c1be58d4-2512-489e-8f2a-b35ba4e41d51)

---

### CH32V003F4U6 RISC-V SoC IO Bank Assignment for Communication Interfaces 

![image](https://github.com/user-attachments/assets/beeaf265-9806-405d-95bb-bf4f95c18ca5)

---

### Pin Connections

| **VSDSquadron Mini** | **Raspberry Pi Pico** |
|-----------------------------|-----------------------------|
|          PD6 (RX)           |           GP4 (TX)          |
|          PD5 (TX)           |           GP5 (RX)          |
|          GND                |           GND               |

---

### Circuit diagram

![image](https://github.com/user-attachments/assets/42a39651-b385-4c73-aa5d-02b249423733)

---

### Circuit Connection 

The transmitter is the VSDSquadron Mini development board featuring the CH32V003F4U6 RISC-V microcontroller, while the receiver is a Raspberry Pi Pico based on the ARM Cortex-M0+ based microcontroller. The VSDSquadron Mini’s TX pin (PD5) is connected to the RP2040’s RX pin (GPIO 5), with a common ground connection between both boards. The VSDSquadron Mini is programmed using the onboard single-wire programmer via USB-C, with development done in C using an Arduino IDE. The Raspberry Pi Pico is programmed in MicroPython using the Thonny IDE, leveraging the machine library for UART communication and GPIO control. The VSDSquadron Mini transmits a constant HIGH signal on its TX pin, and the Raspberry Pi Pico monitors the RX pin, toggling an LED on GPIO 25 ON or OFF based on the signal state. 

---

### TRANSMITTER CODE - VSDSquadron Mini (Arduino IDE)

```c
#define TX PD5
#define TX PD6
void setup() {
  // Configure PD5 (Digital Pin 5) as an output pin
  pinMode(TX, OUTPUT);

  pinMode(RX INPUT);

  Serial.begin(9600);

 // Set PD5 to HIGH
  digitalWrite(TX, HIGH);
}

void loop() {
  // To keep PD5 HIGH forever
  while (1) {
    // Infinite loop 
  }
}
```

---

### RECEIVER CODE - Raspberry Pi Pico (Thonny)

```python
from machine import Pin, UART
import time

# Initialize the UART interface 
uart = UART(1, baudrate=9600, tx=Pin(4), rx=Pin(5))

# Initialize the LED on GPIO 25 
led = Pin(25, Pin.OUT)


tx_pin = Pin(4, Pin.IN)
rx_pin = Pin(5, Pin.IN)


while True:
    if rx_pin.value() == 1:  # Check if TX pin is high
       #print("tx_pin.value")
       led.value(1)  # Turn on LED
    else:
        #print("rx_pin.value")
        led.value(0)  # Turn off LED
       
    time.sleep(0.1)  
```
---
