# VivadoVerse
# 🚀 Accelerated Matrix Multiplication and 3D Point Cloud Rotation on FPGA

This project demonstrates the use of FPGA hardware to accelerate matrix multiplication and apply it to 3D point cloud transformations. It is structured in **multiple phases**, with each phase building on the last to reach full 3D visualization and control via hardware interfaces.

---

## 📌 Objective

To implement a high-speed hardware engine for 3×3 matrix × 3×1 vector multiplication on FPGA and visualize the result through **real-time 3D point cloud rotation**. The goal is to leverage FPGA parallelism for efficient computation and enable dynamic axis-based rotation using external controls.

---

## 📁 Project Phases

| Phase | Description | Status |
|-------|-------------|--------|
| **Phase 1** | Project Planning & Specification | ✅ *(Complete)* |
| **Phase 2** | Matrix Multiplication Engine (3×3 × 3×1) in VHDL | ✅ *(Completed in Xilinx Vivado)* |
[matrixmultiplier3x1](matrixmultiplier3x1)
| **Phase 3** | SRAM Memory Interface and HPS-FPGA Communication | 🔜 |
| **Phase 4** | VGA Display of Rotating 3D Point Cloud | 🔜 |
| **Phase 5** | Switch-Controlled Dynamic Axis Rotation (X, Y, Z) | 🔜 |

---

## 🔧 Current Phase: Phase 2 – Matrix Multiplier (3×3 × 3×1)

### ✔️ Goals:
- Create a VHDL module to multiply a 3×3 matrix with a 3×1 vector.
- Simulate using static inputs in **Xilinx Vivado**.
- Analyze waveform and generate RTL design.
- Prepare testbench for validation.

### 🔨 Deliverables:
- `MatrixMultiplier3x1.vhd` – Core logic
- `tb_MatrixMultiplier3x1.vhd` – Testbench
- Simulation waveforms
- RTL schematic (Vivado)

📷 Simulation Preview:

![Waveform Output](./simulation_waveform.png)

📷 RTL Preview:

_Add RTL schematic screenshot here later._

---

## 💻 Tools & Technologies

- 💡 **Language**: VHDL  
- 🛠️ **Toolchain**: Xilinx Vivado (Design & Simulation)  
- 🖥️ **Target Platform**: Artix-7 FPGA  
- 📈 **Testbench**: Manual simulation with ModelSim/Vivado Simulator

---

## 📂 Repository Structure

```

.
├── src/
│   ├── MatrixMultiplier3x1.vhd
│   ├── tb\_MatrixMultiplier3x1.vhd
│
├── images/
│   ├── simulation\_waveform.png
│   └── rtl\_schematic.png (to be added)
│
├── README.md
└── LICENSE

```

---

## 📌 Future Roadmap

Once Phase 2 is complete and verified, future work includes:

- 🔁 Interfacing multiple SRAMs for dynamic pixel data
- 🧠 Using HPS (ARM) to initialize pixel coordinates
- 🎮 Integrating VGA to display real-time point cloud rotation
- 🎚️ Implementing user-controlled axis rotation with switches

---

## 📜 License

MIT License. Use, modify, and distribute freely with credit.

---

## 🙋‍♂️ Author

**Sandeep kumar**  
B.Tech Electronics & Communication | FPGA Design | VHDL Enthusiast  
📬 Connect on [www.linkedin.com/in/sandeepkumar2612](www.linkedin.com/in/sandeepkumar2612) | 💻 Open for collaborations

```

