# RTL Synthesis Workshop — Day 2

This document captures key concepts and commands discussed on **Day 2** of the RTL Synthesis Workshop. Topics include PVT corners, hierarchical synthesis, flip-flop coding styles, and relevant synthesis commands in Yosys.

---

## PVT Corners

**PVT** stands for **Process, Voltage, Temperature** — key factors influencing timing and power in physical design.

Example library file: sky_hd_sc_hd_tt_025C_1v80.lib


Breakdown:
- `tt` → **Typical process corner** (options: Fast, Typical, Slow)
- `025C` → **Temperature = 25°C** (varies based on geography, e.g., India, Europe)
- `1v80` → **Voltage = 1.8V**

---

## Hierarchical Synthesis

### Example Design:
A module instantiates an OR gate and AND gate to implement: Y = (A & B) | C


### Post-Synthesis Observation:
- Synthesized design contains **NAND gates**, **not AND/OR gates**
- No **NOR gates** due to **PMOS stacking** (NAND preferred due to NMOS stack)
- **Hierarchy is preserved** in the netlist — submodules remain intact

### Key Commands:
- `flatten` → Flattens the hierarchy (optimizes logic but removes module boundaries)

### Submodule-Level Synthesis:
Used when:
- A submodule is **instantiated multiple times** in a larger design
- A design is **too large** to synthesize all at once

```bash
synth -top <SUB_MODULE>
```
This allows reuse of synthesized logic for efficiency.

## Flip-Flop (Flop) Coding Style

### Notes:
- Too many combinational blocks cause **glitches**
- **Flops reduce glitches** and ensure timing stability
- **Set/Reset** signals initialize flip-flops

### Flop Types to Implement:
- Flop with **Asynchronous Reset**
- Flop with **Synchronous Reset**
- Flop with **both Async + Sync Reset**

> Note: **Asynchronous reset** appears directly in the `always` sensitivity list.

## Yosys Synthesis Commands for Flops

After reading the RTL and performing `synth -top`, use the following commands to map flip-flops to actual cells in the target library:

```bash
dfflibmap -lib <lib_file>
abc -liberty <lib_file>
```



## Summary

Day 2 focused on:

- Understanding **PVT (Process, Voltage, Temperature)** corners and how they impact synthesis.
- How synthesis replaces high-level logic gates (AND, OR) with technology-optimized gates (like NAND).
- The difference between **hierarchical** and **flattened** synthesis.
- Advantages of **submodule-level synthesis** for large or repetitive designs.
- Best practices for **flip-flop coding styles** and how to map them to standard cell libraries using Yosys.
