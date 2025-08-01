# RTL Synthesis Workshop — Day 4

This document covers the key takeaways from **Day 4** of the RTL Synthesis Workshop. The focus is on **Gate-Level Simulation (GLS)**, common causes of mismatches between RTL and synthesized designs, and how to perform GLS using Icarus Verilog.

---

## ⛓️ Gate-Level Simulation (GLS)

**GLS** is used to verify:

- Correctness of the **synthesized gate-level netlist**
- **Timing behavior** (since RTL is not timing-aware)
- Real-world behavior by simulating with **delay-aware primitives**

> ⚠️ GLS is essential after synthesis, especially for sign-off or final verification.

---

## ⚠️ Synthesis vs Simulation Mismatches

Common causes of mismatch between RTL simulation and gate-level simulation:

### 🔸 Missing Sensitivity List

Incorrect behavior occurs if not all necessary signals are included in the sensitivity list.

**Example:**
```verilog
always @(sel)  // Incorrect: input data not included
  y = sel ? a : b;
```

Should be:

```verilog
always @(*)
  y = sel ? a : b;
```

### 🔸 Blocking vs Non-Blocking Assignments

Order matters when using blocking (`=`) vs non-blocking (`<=`) assignments.

**Example:**
```verilog
q0 = a | b;
y = q0 & c;
```

Changing the order of these assignments will result in different synthesized hardware.

✅ **Best Practice**: Use non-blocking (`<=`) assignments for sequential logic, especially in `always @(posedge clk)` blocks, to avoid unintended behavior such as race conditions or glitches.

---

### 🔸 Non-Standard Verilog Coding

Avoid ambiguous, tool-specific, or non-synthesizable constructs in Verilog.

🔧 Non-standard coding may simulate correctly but cause mismatches after synthesis due to differing interpretations by tools.

✅ **Best Practice**: Stick to synthesizable constructs and follow established RTL coding guidelines to ensure consistency between simulation and synthesis.

---

## 🧪 Running GLS with Icarus Verilog

To perform Gate-Level Simulation (GLS) using Icarus Verilog, compile the synthesized netlist along with required primitive and library files, and your testbench:

```bash
iverilog primitives.v sky130_fd_sc_hd.v mydesign_netlist.v my_tb.v
./a.out
```

---

## 📁 File Descriptions

| File Name              | Description                                        |
|------------------------|----------------------------------------------------|
| `primitives.v`         | Contains basic logic gate models for simulation    |
| `sky130_fd_sc_hd.v`    | Sky130 standard cell library (synthesis + GLS)     |
| `mydesign_netlist.v`   | Synthesized Verilog netlist (output from Yosys)    |
| `my_tb.v`              | Testbench to drive inputs and observe outputs      |

---

## 📌 Summary

- **Gate-Level Simulation (GLS)** validates functionality and timing after synthesis using actual gate-level netlists.
- Common mismatches between RTL and synthesized simulation include:
  - Missing or incomplete sensitivity lists
  - Misuse of blocking (`=`) vs non-blocking (`<=`) assignments
  - Non-synthesizable or non-standard Verilog code
- Use `iverilog` to simulate the gate-level netlist together with cell libraries and primitives.
- GLS ensures your design behaves correctly after synthesis and before physical implementation.

---

