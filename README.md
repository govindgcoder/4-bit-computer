# 4-bit-computer
A '4 bit computer' circuit I designed during my Digital Electronics Course.

---

## 🎯 Problem Analysis
The project's primary requirement was applying digital logic, specifically **sequencing** and **multiplexer (mux) trees**, to manage instruction processing and data flow between registers.

* Input is entered via DIP switches and stored in the **Instruction Register** and **Data Register**.
* The instruction is decoded (using a 4-to-16 bit decoder) to enable the required branch of the main mux tree.
* The **Arithmetic and Logic Unit (ALU)** is the core processing subsystem. It uses a mux tree to connect the Data Register, Accumulator, and a temporary register to various operator ICs (quad-AND, quad-OR, quad-NOT, quad-XOR, and quad-ADD).

---

## 🛠️ Circuit Design

### Simulation
The logic system was first simulated and tested using **Digital Logic Sim** by Sebastian League.
(Link: `https://sebastian.itch.io/digital-logic-sim`)

Afterward, it was converted to an actual circuit using **Proteus**.

### Hardware Implementation
Components used were primarily from the 74HC series family:

* **74HC86 (Quad XOR):** Used for subtraction in the ALU.
* **74HC139 (Dual 2-to-4 Decoder/Demux):** Used as CLOCK MUX for the Main sequencer.
* **74HC157 (Quad 2-to-1 MUX):** Used to implement the MUX tree for the ALU.
* **74HC160 (Decade Counter):** Used as the sequencer for the entire system.
* **74HC173 (4-bit Register):** Used for the instruction register, data register, accumulator, and temporary register.
* **74HC04 (Hex-Inverter):** Used for NOT gates and in the ALU.
* **74HC08 (Quad AND):** Used for Gate Logic and the ALU.
* **74HC32 (Quad OR):** Used for Gate logic and the ALU.
* **74HC154 (4-to-16 Decoder):** Used as the primary instruction decoder.
* **74LS83 (4-bit Adder):** Used for implementing adder and subtractor circuits.

### Testing
The system was divided into multiple subsystems to isolate and handle logic errors:
* Clock circuit
* Primary Sequencer
* Input system
* Decoder System
* ALU and MUX tree
* ALU sequencer

---

## 🔌 Implementation

* Input system
* Decoder
* Clock and Sequencer
* ALU
* ALU sequencer

### Design Process Notes
* **Scrapped Idea:** An input system with memory capacity was considered but scrapped due to component cost.
* MUX tree for ALU
* Hardware implementation:
    * Clock circuit
    * ALU and sequencer
    * Input and memory subsystem.

---

## 📊 Results & Operation

### General Operation
1.  Input the required commands using DIP switches.
2.  The sequencer triggers the load pin: the instruction is sent to the instruction register, and data is stored in the data register.
3.  The sequencer enables the register outputs to the instruction decoder, which triggers the required logic circuits of the mux tree.

### ALU Sequencer Operation
The ALU operations follow this format:
1.  `IR -> ALU-control`
2.  `ACC -> ALU first operand`
3.  `DR -> ALU second operand`
4.  ALU processes result
5.  `ALU-result -> TEMP`
6.  `TEMP -> ACC`

### Sample Program
* `0000 0010` -> **Addition:** Add 2 (0010) to the initial ACC (0). -> **ACC = 2 (0010)**
* `0001 0001` -> **Subtraction:** Subtract 1 (0001) from ACC (2). -> **ACC = 1 (0001)**
* `0001 0000` -> **AND:** Perform ACC AND 0 (0000). -> **ACC = 0 (0000)**
* `0011 0110` -> **OR:** Perform ACC OR 6 (0110). -> **ACC = 6 (0110)**
* `0100 0000` -> **NOT:** Perform NOT on ACC (0110). -> **ACC = 9 (1001)**
* `1000 0000` -> **INPUT:** Load 0 (0000) into ACC (wipes current data). -> **ACC = 0 (0000)**
* `1111 0000` -> **OUTPUT:** Output the ACC data using LEDs.

---

## 💡 Innovation and Application
* Use of a **double sequencer** (master/slave) with logic circuit control.
* This differs from traditional mini-computer implementations. It's less efficient but was a great learning experience.
* **Potential Application:** Advanced low-power control systems for industrial machines or home appliances.

---

## ⚠️ Challenges and Troubleshooting
* **Sequencer Logic:** The biggest challenge was managing the data flow from the ALU, through computation, and back to the accumulator. This was resolved by implementing a **double sequencer** (master/slave configuration).
* **Wiring:** The physical wiring of the circuit was complex. Building the systems on separate breadboards enhanced troubleshooting.
* **Chip Incompatibility:** The `74LS83` (TTL) had trouble driving the `74HC` (CMOS) chips, causing noise. This was fixed by using **pull-up resistors** on the `74LS83`'s output.

---

## 🏁 Conclusion
The project was an invaluable platform for learning and implementing all major logical systems in Digital Electronics.

A key takeaway for future projects is the importance of a **"divide and conquer"** approach. Attempting to design the entire complex system at once resulted in wasted time. Breaking the problem into smaller, manageable subsystems would be a more efficient methodology.

---

## 📚 References
* Google Images was used to understand the pinouts and functionality of individual ICs.
* No major academic references were used, as the goal was hands-on learning.

---

## 📎 Appendix: Datasheets
* [74LS83 (4-bit Adder)](https://www.alldatasheet.com/datasheet-pdf/view/5744/MOTOROLA/74LS83.html)
* [74HC154 (4-to-16 Decoder)](https://www.alldatasheet.com/datasheet-pdf/view/104086/PHILIPS/74HC154N.html)
* [74HC32 (Quad OR)](https://www.mouser.com/ds/2/308/74HC32.REV1-102593.pdf)
* [74HC04 (Hex-Inverter)](https://www.mouser.com/datasheet/2/308/74HC04.REV1-104629.pdf)
* [74HC173 (4-bit Register)](https://www.ti.com/lit/ds/symlink/cd74hc173.pdf?ts=1760848431915)
* [74HC160 (Decade Counter)](https://assets.nexperia.com/documents/data-sheet/74HC160.pdf)
* [74HC157 (Quad 2-to-1 MUX)](https://assets.nexperia.com/documents/data-sheet/74HC_HCT157.pdf)
* [74HC139 (Decoder/Demux)](https://www.mouser.com/datasheet/2/302/74HC_HCT139-351015.pdf)
* [74HC86 (Quad XOR)](https://toshiba.semicon-storage.com/info/74HC86D_datasheet_en_20160804.pdf)
