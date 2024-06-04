## Overview

This project is an implementation of an assembler for a simple hypothetical computer architecture. The architecture includes 32 registers, memory, and a set of instructions divided into three types: R-type, I-type, and J-type. This assembler converts assembly language code into machine code, handling all necessary encoding and error checking.

## CPU and Memory Specifications

- **Registers:** 
  - 32 registers, named $0 to $31.
  - Each register is 32 bits in size.
  - The least significant bit is 0, and the most significant bit is 31.

- **Memory:**
  - The memory size is (2^25) bytes.

## Instruction Set

The instruction set is divided into three types:

1. **R-type Instructions:**
   - Used for arithmetic and logical operations.
   - Operands are registers.
   - Arithmetic instructions have three operands (rs, rt, rd) where the result of the operation between rs and rt is stored in rd.
   - Copy instructions have two operands and clone information from one register to another.
   - Opcode for arithmetic instructions: 0.
   - Opcode for copy instructions: 1.

2. **I-type Instructions:**
   - One operand is a constant (immediate number).
   - Arithmetic and logical operations use the rs register and the immediate value, storing the result in the rt register.
   - Equality instructions compare values in rs and rt registers, potentially jumping to a label if they are equal. The jump target is encoded in the immediate field, allowing jumps within a range of ±16 bits.
   - Load and save instructions handle data transfer between registers and memory, using the sum of rs and the immediate value as the memory address.

3. **J-type Instructions:**
   - Used for jump operations to labels.

## Assembly Program Structure

The assembly program is composed of the following types of statements:
- **Null Statements:** Whitespace.
- **Comment Statements:** Comments.
- **Directive Statements:** Memory allocation, initialization, etc.
- **Instruction Statements:** Encodings of the instructions.

## Assembler Functionality

The assembler operates in two passes:

1. **First Pass:**
   - Recognizes symbols and builds a symbol table.

2. **Second Pass:**
   - Converts symbols into binary numbers and encodes instructions into machine code.

### Assembler Workflow

1. **Initialization:**
   - Instruction Counter (IC) starts at 100.
   - Data Counter (DC) starts at 0.

2. **Processing Input Files:**
   - Takes a list of input file names via command line arguments.
   - Each assembly file must have a `.as` extension.
   - If a file fails to open, an error message is printed, and the assembler moves to the next file.

3. **Line-by-Line Processing:**
   - Ignores empty or comment lines.
   - Processes instruction lines and updates the symbol table if a label is encountered.
   - Handles directive lines as specified.

4. **Output Files:**
   - **Object File:** Contains the machine code.
   - **Externals File:** Contains external labels.
   - **Entries File:** Contains entry labels.
   - Output files are only generated if relevant data exists.

## Error Handling

The assembler identifies and alerts any errors, printing messages to `stdout`. It continues checking for additional errors after encountering the first one.

## Project Structure

The assembler maintains two arrays:
- **instructionTable:** Used for encoding instructions during the first pass.
- **dataTable:** Used for storing encoded data.
- The assembler also maintains a symbol table for all encountered labels.

## Usage

To use the assembler, provide a list of input assembly files via command line arguments. The assembler will process each file separately, generating corresponding output files if the process is successful.
