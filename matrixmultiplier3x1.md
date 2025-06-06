
# 🔢 3×3 Matrix × 3×1 Vector Multiplier (VHDL)

This project implements a hardware-accelerated 3×3 matrix and 3×1 vector multiplier using **VHDL**. It is designed for FPGA deployment and was tested and simulated using **Xilinx Vivado**.

---

## 📌 Project Overview

Matrix multiplication is fundamental to many applications in computer graphics, robotics, and 3D transformations. This module forms the mathematical basis for **3D point cloud rotation** using rotation matrices.

This implementation serves as **Phase 2** of a larger project:  
🎯 *Accelerated Matrix Multiplication and 3D Point Cloud Rotation on FPGA*

---

## 📐 Functionality

Given a 3×3 matrix `A` and a 3×1 vector `X`, the hardware computes:

```

Y = A × X

```

Where:
```

A = | a11 a12 a13 |
\| a21 a22 a23 |
\| a31 a32 a33 |

X = | x1 |
\| x2 |
\| x3 |

Y = | y1 |
\| y2 |
\| y3 |

```

Each output `yi` is the dot product of the `i-th` row of the matrix and the input vector.

---

## 🧰 Tools & Technologies

- 🔧 **Language**: VHDL  
- 💻 **Simulation**: Xilinx Vivado  
- 🧪 **Testbench**: Custom VHDL testbench  
- ⚡ **Hardware**: Targeted for FPGA implementation

---

## 📂 Repository Structure

```

.
├── MatrixMultiplier3x1.vhd       # Main VHDL module
├── tb\_MatrixMultiplier3x1.vhd    # Testbench for simulation
├── simulation\_waveform.png       # Screenshot of simulation output
├── README.md                     # Project description and guide

```

---

## ▶️ Simulation

The design is simulated with static input values using **Vivado simulator**.  
The testbench checks the correctness of the output for fixed known inputs and matrix coefficients.

🖥️ To run the simulation:

1. Open Vivado → Create a new project
2. Add both `.vhd` files to the project
3. Set `tb_MatrixMultiplier3x1` as the top module
4. Run behavioral simulation and analyze the waveform

---
## 🔧 RTL Design

The Register Transfer Level (RTL) design for the multiplier module was generated and verified in Vivado. It shows:

- Three rows of combinational multipliers and adders
- Parallel structure of arithmetic units for low latency
- Synchronous output logic to store final vector values

🖼️ View the RTL schematic in Vivado:
- Open synthesized design
- Use `Tools → Schematic` to view hierarchy and logic gates
- Look for modules like `mult_gen`, `add`, and internal signal flow

![Screenshot 2025-06-05 152748](https://github.com/user-attachments/assets/cff19f14-bf84-421e-8686-dd54e70ae45b)
  

![Screenshot 2025-06-05 153131](https://github.com/user-attachments/assets/d1673999-54cc-4167-afee-cd7828de2b45)



## 📊 Waveform Output

![Screenshot 2025-06-05 154903](https://github.com/user-attachments/assets/1d2a420f-9952-49f9-8a32-886da8c1be8e)

---

## 📌 Future Enhancements

- ⬜ Add pipelining or parallelism for better performance
- ⬜ Connect module with VGA display and 3D p
oint cloud visualization
- ⬜ Switch-controlled axis selection for dynamic rotation

---

## 📚 License

This project is open-source under the MIT License.  
Feel free to use, modify, and distribute with attribution.

---

## 👤 Author

**Sandeep Kumar**  
B.Tech ECE | FPGA Enthusiast | VLSI Design  
Connect with me on [www.linkedin.com/in/sandeepkumar2612](www.linkedin.com/in/sandeepkumar2612)
