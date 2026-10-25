# EVO-ISA: Workload-Adaptive Processor Architecture

## 📌 Project Summary
EVO-ISA is a dynamic, workload-adaptive processor architecture designed to optimize execution by identifying frequently recurring instruction patterns (e.g., `LOAD → LOAD → ADD → STORE`) and mapping them to optimized compound operations at runtime. This project aims to reduce Cycles Per Instruction (CPI) and execution overhead compared to conventional fixed-ISA processors.

##  Team Members
- Chetan Saatvic Reddy Beeram - Adaptive Subsystem & Integration Lead
- Srivignesh Thokala - Datapath & ALU Engineer
- Mahammad Mathin Shaik - Control & Memory Subsystem Engineer

## 🛠️ Technical Stack
- **HDL:** Verilog / SystemVerilog
- **Simulation & Synthesis:** Xilinx Vivado
- **Target Hardware:** Xilinx Nexys A7 (Artix-7) FPGA
- **Version Control:** Git / GitHub

## 📂 Repository Structure
- `docs/` : Architectural specifications, ISA encoding, and project reports.
- `src/` : Verilog source code, testbenches, and Python assembler scripts.
- `benchmarks/` : Assembly/C test programs for performance evaluation.

## 🚀 Current Status: Week 1
- [x] Project initialization and repository setup.
- [x] Custom 32-bit RISC ISA definition and encoding finalized.
- [ ] Base processor datapath and control unit design (In Progress).
- [ ] Vivado project setup and initial testbench creation.
