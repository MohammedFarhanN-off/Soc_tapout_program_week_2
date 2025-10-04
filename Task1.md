# VSDBabySoC: An Open-Source RISC-V SoC for Learning and Experimentation

This project details the design of **VSDBabySoC**, a compact, open-source System on Chip (SoC) built on the Sky130 technology platform. Centered around the **RVMYTH** RISC-V processor core, this SoC integrates a **Phase-Locked Loop (PLL)** for precise clock generation and a **10-bit Digital-to-Analog Converter (DAC)** for interfacing with external analog systems.

The primary goal of this project is to provide a highly documented, educational platform for learning and experimentation in digital-analog interfacing and open-source IP integration. By converting digital signals into analog outputs, the VSDBabySoC can communicate with devices like televisions and mobile phones, enabling it to produce audio or video.

---

## 1. Project Goals

* **Integrate and Test Open-Source IPs:** Serve as a platform to simultaneously test three open-source IP cores: the RVMYTH CPU, a PLL, and a DAC.
* **Provide an Educational Tool:** Offer a clear and comprehensive example of a complete SoC design flow, from high-level architecture to analog interfacing.
* **Bridge Digital and Analog Worlds:** Demonstrate a practical application of a DAC within an SoC to control real-world analog devices.
* **Promote Open-Source Hardware:** Utilize the open-source RISC-V architecture and Sky130 PDK to encourage community collaboration and learning.

---

## 2. System Architecture and Workflow

The VSDBabySoC operates through a coordinated sequence of actions between its core components:

1.  **Initialization and Clock Generation:** Upon receiving an initial input signal, the **PLL** activates. It generates a stable, high-frequency clock signal that synchronizes the entire system, ensuring all components operate in harmony.
2.  **Data Processing:** The **RVMYTH** RISC-V core, acting as the system's brain, processes data and prepares it for analog conversion. It sequentially loads digital values into its registers, creating a continuous data stream.
3.  **Analog Signal Generation:** The **10-bit DAC** receives the digital values from RVMYTH and converts them into a corresponding analog voltage. This analog output can then be used to drive external devices, such as speakers or video displays.



---

## 3. Core Components in Detail

### RVMYTH (RISC-V CPU Core)

RVMYTH is the central processing unit of the VSDBabySoC. Based on the open-source RISC-V instruction set architecture (ISA), it is a simple and customizable CPU ideal for educational purposes. Its main role is to execute instructions, process data, and manage the data flow to the DAC.

### Phase-Locked Loop (PLL)

The PLL is a critical component for generating a stable and precise clock signal, which is essential for the reliable operation of any digital system.

* **Function:** A PLL is a control system that generates an output signal whose phase is locked to the phase of an input reference signal. In this SoC, it ensures all operations are perfectly synchronized.
* **Key Blocks:**
    * **Phase Detector:** Compares the reference clock with the feedback clock and produces an error signal.
    * **Loop Filter:** A low-pass filter that smooths the error signal into a stable control voltage.
    * **Voltage-Controlled Oscillator (VCO):** Generates the final clock output, whose frequency is adjusted by the control voltage.
* **Why is a PLL Necessary?** Off-chip clocks can introduce problems like **jitter** (timing variations) and **distribution delays**. A PLL provides a clean, stable on-chip clock and can synthesize different required frequencies from a single reference.



### 10-bit Digital-to-Analog Converter (DAC)

The DAC is the bridge between the digital processing world of the SoC and the analog world of external devices.

* **Function:** It converts a digital input (a 10-bit binary number in this case) into a corresponding analog output voltage or current.
* **Resolution:** A 10-bit DAC can represent $2^{10} = 1024$ distinct analog levels, providing a high-resolution output.
* **Common Architectures:**
    * **Weighted Resistor DAC:** Uses resistors with binary-weighted values. Simple in concept but can be difficult to fabricate accurately for high-bit counts.
    * **R-2R Ladder DAC:** Uses a repeating network of only two resistor values (R and 2R). This design is much easier to manufacture accurately and is scalable.



---

## 4. Background: Understanding the Technology

### What is a System on a Chip (SoC)?

A System on a Chip is a microchip that integrates all the necessary components of a computer or electronic system into a single integrated circuit.

* **Key Parts:** An SoC typically includes a **CPU**, **Memory** (RAM/ROM), **I/O Ports**, a **GPU** (Graphics Processing Unit), and specialized blocks like a **DSP** (Digital Signal Processor).
* **Advantages:**
    * **Space Saving:** Combining components onto one chip enables smaller, more portable devices.
    * **Energy Efficient:** Shorter distances between components reduce power consumption, improving battery life.
    * **High Performance:** Faster communication between integrated parts leads to better performance.
    * **Cost-Effective:** A single-chip solution is often cheaper to manufacture than a system built from multiple discrete components.

### SoC Design Flow

The creation of an SoC follows a structured design process, broadly divided into two main stages:

1.  **Front-End Design:** Focuses on the logical and functional aspects of the design.
    * **Architecture Design:** Defining the system's specifications.
    * **RTL Design:** Writing the hardware description in a language like Verilog or VHDL.
    * **Functional Simulation & Verification:** Ensuring the design works as intended.
2.  **Physical Design (Back-End):** Focuses on turning the logical design into a physical layout.
    * **RTL Synthesis:** Translating the RTL code into a gate-level netlist.
    * **Place and Route:** Arranging the logic gates and wiring them together on the chip.
    * **Physical Verification:** Running final checks to ensure the layout is correct and meets timing and power requirements before manufacturing.
