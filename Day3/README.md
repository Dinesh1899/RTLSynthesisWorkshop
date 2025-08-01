# RTL Synthesis Workshop — Day 3

This document summarizes the key learnings from **Day 3** of the RTL Synthesis Workshop, with a focus on combinational and sequential logic optimizations, flop optimizations, and handling unused logic in RTL designs.

---

## Combinational Logic Optimizations

### Techniques:
- **Constant Propagation**  
  Identifies and propagates known constant values through the logic to simplify expressions.

- **Boolean Logic Optimization**  
  Minimizes and simplifies logic expressions using Boolean algebra.

---

## Sequential Constant Propagation

- A **D flip-flop (DFF)** with `D = 0` will always produce `Q = 0`.  
  → In such cases, the flop can be eliminated from the design.

- This only holds true when a **reset input** is used. It does **not** apply with a **set input**:
  - After a set input is removed, the flop remains set until the next clock edge.
  - Therefore, `Q` does not immediately equal the set condition, and the flop cannot be removed safely.

---

## Flop Optimizations

### 1. **Cloning**
- Duplicate logic is created intentionally to **reduce routing delay** between distant logic elements.

### 2. **Retiming**
- Moves combinational logic across flop boundaries to **balance delays** and **increase maximum clock frequency**.

---

## Yosys Optimization Commands

Run the following after synthesizing the top module:

```bash
opt_clean -purge
```
- Cleans up unused or redundant logic.
- Useful after synth -top and before exporting the netlist.
- Multiple modules should be flattened before running this optimization.

- Modules like multiple_module_opt.v should be flattened before running this optimization.

- Also, review dff_const3.v to understand flop-level optimization through constant propagation.
