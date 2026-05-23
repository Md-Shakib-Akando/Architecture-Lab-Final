# Architecture Lab Final Project
An implementation and simulation of core CPU components using Logisim. This project covers the foundational building blocks of computer architecture, including Clock Control Logic, a 4x1-bit Register File, and a 256-Byte Random Access Memory (RAM) module.

## 📌 Table of Contents
* [Modules](#-modules)
  * [1. Clock Gating & Selection Circuit](#1-clock-gating--selection-circuit)
  * [2. 4x1-bit Register File](#2-4x1-bit-register-file)
  * [3. 256-Byte Memory (RAM) Module](#3-256-byte-memory-ram-module)
* [How to Run the Simulations](#-how-to-run-the-simulations)
* [Author](#-author)

---

## 🧩 Modules

### 1. Clock Gating & Selection Circuit
This module controls the processor's heartbeat. It features a multiplexing unit to switch between an automated system clock and manual stepping (for debugging), alongside a software-triggered halt mechanism.

* **Key Features:**
    * **Mode Switching (`CLK_ENB`):** Toggles between Automated Clock (`CLK_IN`) and Manual Pulse (`Manual_clock`).
    * **Halt Logic (`HALT`):** Uses an Active-High Halt signal connected via an inverter to immediately freeze the clock output (`Clock_Out = 0`).
* **Truth Table:**

| CLK_ENB | HALT | Manual_clock | Clock_Out Behavior | Mode |
| :---: | :---: | :---: | :---: | :--- |
| `1` | `0` | `X` | Follows `CLK_IN` | **Automated Execution** |
| `0` | `0` | `Toggle` | Follows `Manual_clock` | **Manual Debugging** |
| `X` | `1` | `X` | Always `0` | **Processor Halted** |

---

### 2. 4x1-bit Register File
A high-speed temporary storage unit consisting of four 1-bit D-Flip-Flops. It supports simultaneous dual-register reading and synchronized single-register writing.

* **Key Features:**
    * **Write Control:** A $2 \times 4$ Decoder paired with `regWrite` (via AND gates) routes the Enable signal safely to the targeted flip-flop.
    * **Dual Read Ports:** Two $4 \times 1$ Multiplexers allow the CPU to read from two different registers concurrently (`read data 1` and `read data 2`).
* **Bus Specifications:**
    * `write Register` / `Read Register 1 & 2`: 2-bit Address Lines.
    * `write data` / `read data 1 & 2`: 1-bit Data Lines.

---

### 3. 256-Byte Memory (RAM) Module
A standardized byte-addressable Random Access Memory (RAM) configuration designed for data caching and instruction storage.

* **Key Features:**
    * **Address Space:** 8-bit Address Bus providing $2^8 = 256$ unique memory addresses.
    * **Word Size:** 8-bit Data Bus (1 Byte per storage cell).
    * **Control Safe Guards:** Chip Select (`sel`) is pinned High to keep the module active, while Clear (`clr`) is pinned Low to protect against accidental data wipes.
* **Operational Specs:** * `str` (Store) acts as Write Enable.
    * `ld` (Load) acts as Read Enable. 
    * *Note: In Logisim, if both `str` and `ld` are High, the Store (Write) operation takes priority.*

---

## 🚀 How to Run the Simulations

1.  Download and install **Logisim** (or Logisim-Evolution).
2.  Clone this repository:
    ```bash
    git clone [https://github.com/your-username/Architecture-Lab-Final.git](https://github.com/your-username/Architecture-Lab-Final.git)
    ```
3.  Open Logisim and load the respective `.circ` files.
4.  To test the **Clock Module**, turn on Simulation (`Ctrl + K`) and toggle the inputs using the **Poke Tool** (Hand Icon).
5.  To write data into the **Register File** or **RAM**, ensure the write-enable lines are active and cycle the clock manually.

---

## 👤 Author
* **Shakib Akando**
    * Computer Programming Club (CPC) Development Community
