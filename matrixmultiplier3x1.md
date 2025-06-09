
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
## 🔧 VHDL design code 
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.NUMERIC_STD.ALL;

entity MatrixMultiplier3x1 is
    Port (
        a11, a12, a13 : in  STD_LOGIC_VECTOR(7 downto 0);
        a21, a22, a23 : in  STD_LOGIC_VECTOR(7 downto 0);
        a31, a32, a33 : in  STD_LOGIC_VECTOR(7 downto 0);
        x, y, z       : in  STD_LOGIC_VECTOR(7 downto 0);
        result1       : out STD_LOGIC_VECTOR(15 downto 0);
        result2       : out STD_LOGIC_VECTOR(15 downto 0);
        result3       : out STD_LOGIC_VECTOR(15 downto 0)
    );
end MatrixMultiplier3x1;

architecture Behavioral of MatrixMultiplier3x1 is
begin
    process(a11, a12, a13, a21, a22, a23, a31, a32, a33, x, y, z)
        variable temp1, temp2, temp3 : unsigned(15 downto 0);
    begin
        temp1 := unsigned(a11) * unsigned(x) + unsigned(a12) * unsigned(y) + unsigned(a13) * unsigned(z);
        temp2 := unsigned(a21) * unsigned(x) + unsigned(a22) * unsigned(y) + unsigned(a23) * unsigned(z);
        temp3 := unsigned(a31) * unsigned(x) + unsigned(a32) * unsigned(y) + unsigned(a33) * unsigned(z);

        result1 <= std_logic_vector(temp1);
        result2 <= std_logic_vector(temp2);
        result3 <= std_logic_vector(temp3);
    end process;
end Behavioral;

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


## 🔧 RTL Design
-- File: tb_MatrixMultiplier3x1.vhd
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.NUMERIC_STD.ALL;

entity tb_MatrixMultiplier3x1 is
end tb_MatrixMultiplier3x1;

architecture behavior of tb_MatrixMultiplier3x1 is

    component MatrixMultiplier3x1
        Port (
            a11, a12, a13 : in  STD_LOGIC_VECTOR(7 downto 0);
            a21, a22, a23 : in  STD_LOGIC_VECTOR(7 downto 0);
            a31, a32, a33 : in  STD_LOGIC_VECTOR(7 downto 0);
            x, y, z       : in  STD_LOGIC_VECTOR(7 downto 0);
            result1       : out STD_LOGIC_VECTOR(15 downto 0);
            result2       : out STD_LOGIC_VECTOR(15 downto 0);
            result3       : out STD_LOGIC_VECTOR(15 downto 0)
        );
    end component;

    -- Test signals
    signal a11, a12, a13 : STD_LOGIC_VECTOR(7 downto 0);
    signal a21, a22, a23 : STD_LOGIC_VECTOR(7 downto 0);
    signal a31, a32, a33 : STD_LOGIC_VECTOR(7 downto 0);
    signal x, y, z       : STD_LOGIC_VECTOR(7 downto 0);
    signal result1, result2, result3 : STD_LOGIC_VECTOR(15 downto 0);

begin

    -- UUT Instantiation
    uut: MatrixMultiplier3x1
        Port Map (
            a11 => a11, a12 => a12, a13 => a13,
            a21 => a21, a22 => a22, a23 => a23,
            a31 => a31, a32 => a32, a33 => a33,
            x => x, y => y, z => z,
            result1 => result1,
            result2 => result2,
            result3 => result3
        );

    -- Test Stimulus
    stim_proc: process
    begin
        -- Matrix:
        -- 1 2 3
        -- 4 5 6
        -- 7 8 9
        -- Vector: 1 2 3

        a11 <= "00000001"; a12 <= "00000010"; a13 <= "00000011";  -- Row 1
        a21 <= "00000100"; a22 <= "00000101"; a23 <= "00000110";  -- Row 2
        a31 <= "00000111"; a32 <= "00001000"; a33 <= "00001001";  -- Row 3

        x <= "00000001"; y <= "00000010"; z <= "00000011";        -- Vector

        wait for 10 ns;

        -- Optional console output
        report "Result1 = " & integer'image(to_integer(unsigned(result1)));
        report "Result2 = " & integer'image(to_integer(unsigned(result2)));
        report "Result3 = " & integer'image(to_integer(unsigned(result3)));

        wait;
    end process;

end behavior;

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
