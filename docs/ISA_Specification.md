# EVO-ISA: Custom 32-bit RISC Instruction Set Architecture

## 1. Design Philosophy
To ensure rapid development and clear debugging, EVO-ISA utilizes a simplified, MIPS-like 32-bit fixed-length instruction format. This reduces decoder complexity while providing all necessary operations to demonstrate the adaptive pattern-matching capabilities.

## 2. Instruction Formats
All instructions are 32 bits wide. We utilize two primary formats:

### R-Type (Register Operations)
| 31-26 (6 bits) | 25-21 (5 bits) | 20-16 (5 bits) | 15-11 (5 bits) | 10-0 (11 bits) |
| :---: | :---: | :---: | :---: | :---: |
| Opcode | Rs (Source 1) | Rt (Source 2) | Rd (Destination) | Unused / Func |

### I-Type (Immediate / Memory Operations)
| 31-26 (6 bits) | 25-21 (5 bits) | 20-16 (5 bits) | 15-0 (16 bits) |
| :---: | :---: | :---: | :---: |
| Opcode | Rs (Base/Source) | Rt (Dest/Source) | Immediate / Offset |

## 3. Core Instruction Set (Initial Baseline)
| Mnemonic | Format | Opcode (6-bit) | Description |
| :--- | :---: | :---: | :--- |
| `ADD` | R-Type | `000000` | Rd = Rs + Rt |
| `SUB` | R-Type | `000001` | Rd = Rs - Rt |
| `LOAD`| I-Type | `001000` | Rt = Memory[Rs + Imm] |
| `STORE`| I-Type | `001001` | Memory[Rs + Imm] = Rt |
| `BEQ` | I-Type | `001100` | Branch if Rs == Rt (PC + Imm) |
| `JUMP`| I-Type | `001101` | Unconditional jump to (PC + Imm) |

## 4. EVO-ISA Adaptive Extension
When the Pattern Detection Unit identifies a recurring sequence (e.g., `LOAD` -> `LOAD` -> `ADD`), the Adaptive Controller will map this to a reserved custom opcode:
- **Macro-Opcode:** `111111` (Reserved for EVO-ISA Custom Operations)
- **Execution:** Bypasses standard fetch/decode overhead, executing the pre-defined micro-operation sequence from the Custom Operation Cache in a reduced cycle count.
