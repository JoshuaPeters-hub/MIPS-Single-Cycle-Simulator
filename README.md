# MIPS Single-Cycle Processor Simulator

A cycle-by-cycle simulator of a single-cycle MIPS processor, written in C++. It loads a MIPS program and its data memory from text files, runs each instruction through fetch, decode, execute, memory access and write-back in one cycle, and writes out the final register file and data memory.

Built for Computing Systems Architecture (NYU Tandon, Fall 2026) with my lab partner [@limb0007](https://github.com/limb0007). The course provided the program skeleton and test files; we implemented the processor logic together.

## What it does

- Reads a program (`imem.txt`) and initial data (`dmem.txt`) as binary strings, one byte per line, big-endian.
- Fetches each 32-bit instruction, decodes its opcode and function fields, and executes it.
- Supports these instructions:

| Type | Instructions |
|---|---|
| R-type | `addu`, `subu` |
| I-type | `addiu`, `beq`, `lw`, `sw` |
| J-type | `j` |
| Special | `halt` (stops the simulation) |

- Writes the register file after every cycle to `RFresult.txt`, and the final data memory to `dmemresult.txt`.

## How it works

- **Register file:** 32 registers of 32 bits, with register 0 fixed at zero.
- **Instruction and data memory:** byte-addressable arrays loaded from the text files.
- **ALU:** adds or subtracts based on the decoded ALU operation.
- **Control:** the decoder sets the signals for each instruction type (register write, memory read and write, branch, jump), including sign-extending immediates and computing branch and jump targets.

## Running it

```bash
make            # builds ./MIPS with g++
rm -f RFresult.txt dmemresult.txt   # the program appends to these, so start clean
./MIPS          # reads imem.txt and dmem.txt from the current folder
```

Compare the output with the expected results (a fresh run matches them exactly):

```bash
diff RFresult.txt expected_results/RFresult_ans.txt
diff dmemresult.txt expected_results/dmemresult_ans.txt
```

## Built with

C++ (g++), Make

## Authors

Uzoma Peters ([@JoshuaPeters-hub](https://github.com/JoshuaPeters-hub)) and [@limb0007](https://github.com/limb0007)
