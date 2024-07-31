---
layout: post
title:  "About my GSOC Project"
author: Atharva
categories: [ GSOC ]
tags: [Resources]
image: ../assets/images/BeagleV-Fire.png
description: "About: Exploring the deployment of a custom RISC-V core on BeagleV-Fire to achieve ultra-low-latency I/O operations."
featured: true
hidden: false
---
## Introduction

*As embedded systems evolve, the need for efficient real-time processing is crucial. The BeagleV-Fire's FPGA fabric provides an ideal platform to deploy a custom RISC-V core aimed at high-performance I/O control tasks. This project aims to replicate the Programmable Real-time Unit (PRU) subsystem by Texas Instruments deployed on BeagleBone Black, enhancing the flexibility and responsiveness of embedded applications.*

---

### Project Goals

The main objectives of this project include:

- *High Bandwidth Communication*: Facilitate efficient data transfer between the main CPU and various I/O devices.
- *Single-Cycle Execution*: Modify the RISC-V core to ensure all instructions execute in a single cycle, significantly reducing latency.
- *I/O Compatibility*: Adapt the existing PicoRV core to support a wide range of I/O operations necessary for real-time tasks.

### Development Stages

The project is divided into two key stages:

- **Stage 1: Core Development** <br>
    This phase focuses on enhancing the PicoRV core for I/O compatibility and ensuring single-cycle execution. By examining existing soft processor IPs like AMD's Microblaze, we aim to implement efficient I/O operations.

- **Stage 2: Communication Setup** <br>
    Once the RISC-V core is deployed, we will establish a robust communication channel between the PRU and the main CPU. This setup will enable on-the-fly programming of the PRU using a bare-metal C compiler (riscv64-unknown-elf-gcc), allowing seamless instruction transfers without requiring frequent FPGA reconfiguration.

### Challenges Ahead

While the project holds great promise, it also presents challenges. Achieving I/O compatibility and single-cycle execution for I/O operations will require careful design and extensive testing. Additionally, establishing a reliable communication interface will be crucial for effective interaction between the PRU and main CPU.

### Conclusion

This project stands at the intersection of open-source hardware and software development, with the potential to significantly enhance real-time control systems. By deploying a custom RISC-V core on the BeagleV-Fire, we aim to create a powerful and flexible platform for various industrial applications. Stay tuned for updates as we progress through our development journey!
