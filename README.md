# 🖥️ Computer Implementation from Scratch

> Building a fully functional general-purpose computer — starting from a single logic gate.

---

## Overview

This project walks the complete path from the most primitive building block in digital logic — the **NAND gate** — all the way up to a working computer with its own **CPU**, **memory hierarchy**, and a custom **assembler**.

Every component is implemented by hand: gates and chips in **HDL**, the assembler in **Python**. No black boxes, no shortcuts — every layer of abstraction is built explicitly on top of the one before it.

---

## Repository Structure

```
.
├── 1) Logic Gates/        # All fundamental gates, derived from NAND
├── 2) Building an ALU/    # Adders, incrementer, and the ALU itself
├── 3) Memory/             # Bit cell up to RAM16K and Program Counter
├── 4) Computer/           # CPU, Memory chip, and full Computer
└── 5) Assembler/          # A multi-file Python assembler
```

---

## Chapters

### 1 · Logic Gates
**`1) Logic Gates/`**

The entire project rests on one axiom: **NAND is universal**. Every gate here is derived from it, with no external primitives allowed.

| File | Gate |
|---|---|
| `Not.hdl`, `Not16.hdl` | Inverter (1-bit and 16-bit) |
| `And.hdl`, `And16.hdl` | Conjunction |
| `Or.hdl`, `Or16.hdl`, `Or8Way.hdl` | Disjunction |
| `Xor.hdl` | Exclusive OR |
| `Mux.hdl`, `Mux16.hdl`, `Mux4Way16.hdl`, `Mux8Way16.hdl` | Multiplexers |
| `DMux.hdl`, `DMux4Way.hdl`, `DMux8Way.hdl` | Demultiplexers |

---

### 2 · Building an ALU
**`2) Building an ALU/`**

With gates in place, arithmetic becomes possible. The chapter builds upward from single-bit addition to a complete 16-bit ALU.

| File | Component |
|---|---|
| `HalfAdder.hdl` | Adds two bits, produces sum and carry |
| `FullAdder.hdl` | Adds three bits (includes carry-in) |
| `Add16.hdl` | 16-bit ripple-carry adder |
| `Inc16.hdl` | 16-bit incrementer |
| `ALU.hdl` | Full Arithmetic Logic Unit — addition, bitwise ops, negation, zero/negative flags |

---

### 3 · Memory
**`3) Memory/`**

Computation without state is useless. This chapter builds the memory hierarchy from the ground up, starting from a single stored bit.

| File | Component |
|---|---|
| `Bit.hdl` | 1-bit memory cell (D flip-flop) |
| `Register.hdl` | 16-bit register |
| `RAM8.hdl` → `RAM16K.hdl` | RAM units: 8, 64, 512, 4K, 16K words |
| `PC.hdl` | Program Counter with load, increment, and reset |

---

### 4 · Computer
**`4) Computer/`**

All components converge into a working machine.

| File | Component |
|---|---|
| `CPU.hdl` | Fetches, decodes, and executes instructions; manages the A/D registers and the PC |
| `Memory.hdl` | Unified address space — RAM, screen, and keyboard mapped into a single chip |
| `Computer.hdl` | Top-level chip wiring the CPU, Memory, and ROM together |

---

### 5 · Assembler
**`5) Assembler/`**

A computer is only as useful as the programs it can run. The assembler translates symbolic assembly code into binary machine instructions the CPU can execute.

The implementation is cleanly split across multiple modules:

| File | Role |
|---|---|
| `Assembler.py` | Entry point — orchestrates the two-pass assembly process |
| `Lex.py` | Tokenizes the raw source input |
| `Parser.py` | Parses tokens into A-instructions, C-instructions, and labels |
| `Code.py` | Translates parsed instructions into binary fields |
| `SymbolTable.py` | Manages predefined symbols, labels, and variable allocation |

**Usage:**
```bash
python Assembler.py <source.asm>
# Output: <source.hack>  —  binary ready to load into the CPU emulator
```

---

## Implementation Stack

| Layer | Technology |
|---|---|
| Logic gates, ALU, Memory, CPU | HDL (`.hdl`) |
| Assembler | Python |
| Simulation & testing | Hardware Simulator / CPU Emulator |

---

## Running the Hardware

Load any `.hdl` file into the **Hardware Simulator** and run its corresponding test script:

```
File → Load Chip    →  select .hdl file
File → Load Script  →  select .tst file
Run
```

---

## Philosophy

Most people use computers their entire lives without ever asking what one *actually is*. This project is an answer to that question — not in theory, but in working, gate-level code.

The architecture is intentionally minimal. That minimalism is the point: it forces every design decision to be explicit and fully understood before moving to the next layer.

---
