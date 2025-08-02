# 📘 Day 5 – Optimization in Synthesis

## ✅ IF / CASE Constructs

- `if` statements create **priority logic** and synthesize into **priority multiplexers**.
- `case` statements are used for **parallel decision logic** (non-priority MUX).
- **Incomplete** `if` or `case` blocks can infer **latches** — always assign all outputs.
- Use **`default`** in `case` to avoid latches, but it must fully define outputs.
- `if` / `case` must be inside an `always` block, and the assigned variables should be declared as `reg`.
- Avoid multiple matching `case` expressions, especially with `casex`/`casez`, as they may lead to ambiguity.

---

## 🔁 For Loops vs. Generate Loops

### `for` Loop (Procedural)
- Used inside `always` blocks to **evaluate expressions multiple times**.
- Commonly used to create logic for wide MUXes or repeated operations on data buses.
- Does **not instantiate** hardware modules.

### `generate-for` Loop (Structural)
- Used outside `always` blocks to **instantiate hardware blocks repeatedly**.
- Useful in building N-bit adders, arrays of registers, etc.

---

## 🔹 if-generate
- Used to **conditionally instantiate** hardware based on parameters or conditions.
- Enables flexible, modular RTL code design.

---

## 📝 Summary Table

| Construct       | Purpose                        | Hardware Instantiated |
|----------------|----------------------------------|------------------------|
| `if` / `case`  | Conditional logic / MUX         | ✅ Yes                 |
| `for`          | Repeated logic (within always)  | ❌ No (unrolled logic) |
| `generate-for` | Module replication              | ✅ Yes                 |
| `if-generate`  | Conditional module inclusion    | ✅ Yes                 |


