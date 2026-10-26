# EVO-ISA: Workload-Adaptive Processor Architecture

## 📌 Project Overview
EVO-ISA is a custom 32-bit, multi-cycle RISC-style processor designed for our Computer Organization and Architecture (COA) course. Unlike conventional fixed-ISA processors, EVO-ISA features a hardware-based adaptive subsystem that monitors the instruction stream, detects recurring patterns (e.g., `LOAD → LOAD → ADD → STORE`), and dynamically maps them to optimized "Compound Operations" to reduce execution cycles and CPI.

## 👥 Development Team
This project is being developed by a hybrid team of human engineers and specialized AI agents to ensure rigorous design and verification.

**Human Engineers:**
- Chetan Saatvic Reddy Beeram - Integration, Adaptive Subsystem & Project Coordination
- Srivignesh Thokala - Datapath, ALU, and Memory Modules
- Mohammad Mathin Shaik - ISA, Control Unit, and Instruction Execution

**AI Teammates:**
- **ARCHITECT:** Assists with RTL design, architecture documentation, and Verilog drafting.
- **VERIFIER:** Independently generates testbenches, checks correctness, and analyzes performance metrics.

## 🛠️ Technology Stack
- **Hardware Description:** Verilog HDL
- **Simulation & Synthesis:** AMD Xilinx Vivado (RTL Simulation)
- **Target Hardware:** Optional Xilinx Nexys A7 FPGA
- **Version Control:** Git / GitHub

## 📂 Project Structure
- `/docs/` - Architecture specifications, ISA definitions, and design documents.
- `/rtl/` - Verilog source code for the datapath, control unit, and adaptive subsystem.
- `/tb/` - Testbenches and verification scripts.
- `/benchmarks/` - Assembly programs used for performance evaluation.

## 📊 Current Status (Week 1)
- [x] Project scope and methodology finalized.
- [x] Base processor architecture and multi-cycle FSM designed.
- [x] Custom 32-bit ISA specification defined.
- [x] AI Agent roles (ARCHITECT & VERIFIER) configured.
- [ ] *Next:* Implementation of baseline CPU modules (ALU, Register File).
