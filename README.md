# Pipelined MIPS32 Processor --- Verilog HDL

## Overview
This project implements a **32-bit Pipelined MIPS Processor** designed using **Verilog HDL** and verified through simulation. The processor follows a classic **5-stage instruction pipeline** and demonstrates hardware-level parallelism used in modern CPUs.

> Designed for learning Computer Architecture, Digital Design, and VLSI system implementation.

---

## Architecture
The processor implements a **5-stage pipeline**:

### Instruction Flow
```
--------------------------------------------------
IF  →  ID  →  EX  →  MEM  →  WB
--------------------------------------------------
Fetch   Decode  Execute  Memory  Writeback
```

### Pipeline Stages
| Stage | Description |
|---|---|
| **IF** | Fetch instruction from memory |
| **ID** | Decode instruction & read registers |
| **EX** | ALU computation / branch evaluation |
| **MEM** | Data memory access |
| **WB** | Write result back to register |

---

## ⏱ Two-Phase Clocking Scheme
| Clock | Active Stages |
|---|---|
| `clk1` | IF, EX, WB |
| `clk2` | ID, MEM |

This avoids structural hazards between stages.

---

## ⚙️ Supported Instruction Set

### R-Type (Register ALU)
- ADD
- SUB
- AND
- OR
- SLT
- MUL

### I-Type (Immediate)
- ADDI
- SUBI
- SLTI

### Memory Operations
- LW (Load Word)
- SW (Store Word)

### Branch Instructions
- BEQZ (Branch if Equal to Zero)
- BNEQZ (Branch if Not Equal to Zero)

### Control Instruction
- HLT (Halts processor execution)

---

## 🧩 Instruction Format

### R-Type
```
| opcode | rs | rt | rd | unused |
```

### I-Type
```
| opcode | rs | rt | immediate |
```

---

## 📂 Project Structure
```
Pipelined-MIPS32/
│
├── pipe_MIPS32.v      # Processor implementation
├── test_mips32.v      # Simulation testbench
├── mips.vcd           # Generated waveform
└── README.md
```

---

## ▶️ Running the Simulation

### Using Icarus Verilog

#### Compile
```bash
iverilog -o mips_out pipe_MIPS32.v test_mips32.v
```

#### Run
```bash
vvp mips_out
```

#### View Waveform
```bash
gtkwave mips.vcd
```

---

## Expected Simulation Result
```text
R1 = 10
R2 = 20
R3 = 25
R4 = 30
R5 = 55
```

---

## Pipeline Behavior
- Instruction overlap across stages improves throughput.
- Branch instructions flush incorrect instructions.
- Dummy instructions help avoid data hazards.

---

## Waveform Analysis
Recommended signals to observe:
- `PC`
- `IF_ID_IR`
- `ID_EX_IR`
- `EX_MEM_IR`
- `MEM_WB_IR`
- `Reg[]`
- `TAKEN_BRANCH`
- `HALTED`

---

## Tools & Technologies
- Verilog HDL
- Icarus Verilog
- GTKWave
- ModelSim (optional)

---

## Learning Outcomes
- CPU pipeline implementation
- Hardware concurrency
- Instruction decoding logic
- Pipeline register design
- Branch control mechanisms
- Digital system simulation

---

## Resume Description
Designed and simulated a 32-bit pipelined MIPS processor using Verilog HDL implementing a 5-stage pipeline with branch handling and memory operations. Verified instruction execution through waveform analysis using GTKWave.

---

## 👩 Author
**Aditee Ping**  
B.Tech --- Computer Science and Engineering  
National Institute of Technology Rourkela  

---

## ⭐ Future Improvements
- Data forwarding unit
- Hazard detection unit
- Cache memory integration
- FPGA implementation

---

## License
Academic and educational use.
