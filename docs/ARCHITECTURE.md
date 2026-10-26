# EVO-ISA: Architecture & Design Specification

## 1. Base Processor Architecture
EVO-ISA is implemented as a **32-bit, multi-cycle RISC-style processor**. We deliberately chose a multi-cycle design for the baseline to ensure absolute correctness in instruction execution before introducing the adaptive subsystem.

### Core Hardware Modules
- **Datapath:** Program Counter (PC), Instruction Register (IR), 8-register File (R0-R7), ALU, and Multiplexers.
- **Memory:** Separate Instruction Memory (ROM) and Data Memory (RAM) for simplified Harvard-style access during the multi-cycle execution.
- **Control Unit:** A main Finite State Machine (FSM) that sequences instructions through Fetch, Decode, Execute, Memory, and Write-Back states.

## 2. Instruction Set Architecture (ISA)
We utilize a custom, simplified 32-bit ISA to keep decoder complexity manageable while fully demonstrating the COA concepts.

### Instruction Formats
- **R-Type:** Register-to-register operations (e.g., `ADD`, `SUB`)
- **I-Type:** Memory and immediate operations (e.g., `LOAD`, `STORE`, `ADDI`)
- **J-Type:** Control flow (e.g., `BEQ`, `JUMP`)
- **C-Type:** *Custom EVO-ISA format reserved for Compound Operations.*

## 3. The EVO-ISA Adaptive Subsystem (Core Innovation)
The adaptive subsystem operates in parallel with the main datapath. It consists of four tightly coupled hardware modules:

1. **Observation Unit (`obs_unit.v`):** Taps into the datapath at the end of every instruction retirement. It logs the `opcode` of the executed instruction.
2. **Pattern Detector (`pattern_detector.v`):** A depth-4 shift register that continuously compares the last 4 executed instructions against a hardcoded target pattern: `[LOAD, LOAD, ADD, STORE]`.
3. **Frequency Counter (`freq_counter.v`):** Increments when `pattern_match == 1`. Resets to 0 on any branch/jump to prevent false pattern matching across different code blocks.
4. **Adaptive Controller (`adaptive_ctrl.v`):** When the frequency counter hits the threshold (default: **5 occurrences**), this unit intercepts the main Control FSM. It forces the processor to bypass standard fetch/decode cycles and jump directly into compressed `S_COP` (Compound Operation) micro-states.

## 4. Evaluation Methodology
Performance is evaluated by running identical assembly workloads on both the Baseline CPU and the EVO-ISA CPU. 
- **Metrics:** Total Execution Cycles, Retired Instructions, CPI, IPC, and Speedup.
- **Verification:** Both execution paths must result in identical final Register and Memory states.

## 5. AI-Assisted Workflow
- **ARCHITECT:** Responsible for RTL drafting, module interface definitions, and FSM state-table generation.
- **VERIFIER:** Responsible for independent testbench generation, correctness checking, and parsing simulation logs to calculate CPI/Speedup.
