# Day 1:  Introduction to Verilog RTL design and Synthesis

This repository documents key commands and flow used during **Day 1** of the RTL Synthesis Workshop. It focuses on simulation using Icarus Verilog and GTKWave, as well as synthesis using Yosys with the Sky130 standard cell library.

---

## Tools Used

- **Icarus Verilog** – RTL simulation
- **GTKWave** – Waveform visualization
- **Yosys** – Open-source synthesis tool
- **Sky130** – Open-source PDK (Process Design Kit)

---

## RTL Simulation

### Files:
- `good_mux.v` – RTL design
- `tb_good_mux.v` – Testbench

### Steps:
```bash
# Compile RTL and testbench
iverilog good_mux.v tb_good_mux.v

# Run simulation
./a.out

# View waveforms in GTKWave
gtkwave good_mux.vcd

