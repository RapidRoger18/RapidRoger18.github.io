---
layout: post
title:  "Integrating PicoRV32 with BeagleV-Fire"
author: Atharva
categories: [ GSOC ]
tags: [Updates]
image: ../assets/images/PolarFire-SoC-FPGA-Regular.png
description: "A detailed walkthrough of creating a flexible wrapper module to connect PicoRV32 with memory and GPIOs."
featured: false
hidden: false
---

After 1.5 weeks of dedicated work, I successfully developed a wrapper module to integrate the PicoRV32 CPU with the CAPE module on the BeagleV-Fire. This module is critical for connecting the PicoRV32 CPU to the memory modules, facilitating efficient data transfers.

### Understanding the Memory Architecture

A CPU typically operates with three main types of memory:

- **Instruction/Program Memory**: Stores the executable code.
- **Data Memory (Scratchpad RAM)**: Holds temporary data during execution.
- **Stack Memory**: Manages function calls, local variables, and control flow.

These memories are organized into distinct address spaces within the CPU, defining their sizes and accessibility. Proper address space assignment is crucial as it directly impacts the CPU's performance and functionality.

### Implementing the Wrapper Module

The Wrapper module I developed plays a central role in instantiating the memory modules and the CPU, and it assigns pins and buses according to the designated memory addresses. For this project, I allocated:

- **1MB of Program Memory**
- **4KB of Data Memory**
- **4KB of Stack Memory**

The remaining address space is reserved for I/O and other peripheral devices, following a register-memory-mapped approach. This method allows easy access to GPIOs by simply reading from or writing to specific CPU-mapped addresses. The CAPE module's pre-defined BiBuf connections to the I/O pins simplified this process, making GPIO manipulation straightforward.

### Memory Address Mapping for PicoRV32

The memory and I/O address space for the PicoRV32 Softcore is mapped as follows:

| Address Range         | Description                   |
|:-----------------------:|:-------------------------------:|
| `0000_0000 -> 000F_FFFF` | **Program Memory** (1MB)      |
| `0010_0000 -> 0010_0FFF` | **Data Memory** (4KB)         |
| `0010_1000 -> 0010_1FFF` | **Stack Memory** (4KB)        |
| `0010_2000`           | **GPIO Read Register**        |
| `0010_2004`           | **GPIO Output Enable Register** |
| `0010_2008`           | **GPIO Output Register**      |

<br>
By implementing this mapping in the `BVF_WRAPPER.v` file, I established a reliable and efficient memory architecture that meets the project’s requirements.

### Introducing a Dedicated Softcore Component Option

Initially, integrating the softcore as a part of the CAPE option seemed logical. However, this approach limited users' ability to incorporate their custom Verilog designs alongside the softcore processor within the FPGA fabric.

To overcome this limitation, I restructured the design by introducing a dedicated ***SOFTCORE*** component option separate from the ***CAPE*** options. This architectural change offers several advantages:

- **Flexibility**: Users can now select and integrate different CPU cores as needed, without being constrained by the CAPE configurations.
- **Customization**: It becomes easier to add or modify peripheral interfaces and custom logic designs alongside the softcore processor.
- **Scalability**: The system can be extended with additional components and functionalities without extensive reconfiguration.

### Implementing Configuration Changes

To facilitate this modular approach, several configuration updates were made:

- **TCL Scripts**: New scripts were developed to automate the setup and integration process of the softcore component within the FPGA design flow.
- **Directory Structure**: A structured directory layout was established to organize the softcore and associated resources effectively.
- **XML Configuration**: Necessary modifications were made to the XML files governing the project configurations, enabling seamless selection and combination of different **CAPE** and **SOFTCORE** options.

These enhancements collectively contribute to a more user-friendly and adaptable development environment, empowering developers to tailor the FPGA system to their specific application requirements.

### Conclusion

The integration of the PicoRV32 softcore processor with the BeagleV-Fire platform through a dedicated wrapper module and modular component design significantly enhances the system's flexibility and usability. Users can now effortlessly combine custom designs with the softcore processor, facilitating diverse applications ranging from embedded systems to complex computational tasks.

This modular approach not only streamlines the development process but also opens avenues for future expansions and optimizations, ensuring that the system can evolve alongside emerging technological demands and innovations.

---
### References
- [BVF Wrapper module](https://openbeagle.org/gsoc/2024/riscv-io-core/-/blob/03705ea32662c539c17e95e0700310f81e81e066/sources/FPGA-design/script_support/components/SOFTCORE/PICO_RISCV/HDL/BVF_WRAPPER.v)
- [Softcore component to gateware](https://openbeagle.org/gsoc/2024/riscv-io-core/-/tree/03705ea32662c539c17e95e0700310f81e81e066/sources/FPGA-design/script_support/components/SOFTCORE)
