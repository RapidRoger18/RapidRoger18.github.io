---
layout: post
title:  "Starting My GSoC Journey"
author: Atharva
categories: [ GSOC ]
tags: [Updates]
image: ../assets/images/BeagleV-Fire.png
description: "Week 1 Foundation: Challenges and Innovations in programming and testing real-time systems with RISC-V architecture."
featured: false
hidden: false
---

*As the GSoC timeline began, I was still immersed in my end-term examinations, which delayed my start on the coding aspect of my project. However, I remained committed to advancing my work by focusing on foundational research.*

I began by addressing some fundamental questions:

- **How will I program this PRU?** <br>
    A quick solution would be to load the program while flashing the soft core onto the FPGA, but this undermines the essence of a "real-time" system. To achieve true real-time functionality, I needed to program the memory at runtime, which could only be accomplished through the Linux system running on the main CPU. This approach promised to be challenging to implement and even harder to debug.

- **How will the CPU access the I/O?** <br>
    Unlike x86 processors, RISC-V lacks a MEM/IO pin for implementing "I/O mapped I/O." Thus, I would need to utilize memory-mapped I/O, the standard protocol for RISC-V architecture. We also considered an alternative approach of mounting I/O to the CPU's built-in registers for faster operations. While both methods are efficient and reliable, they come with their own sets of pros and cons, which we would only fully understand after thorough testing.

- **How can anyone program this PRU?** <br>
    To program the PRU in C, I needed a compiler configured with specific arguments to set the exact parameters for memory and peripherals, ensuring the program compiled correctly.

With these questions in mind, I gathered numerous resources, diving into a select few to seek answers.

Once my exams concluded, I set up a basic environment for testing I/O mapping. Given my prior experience with a RISC-V CPU during my first-year project, I chose to use the same processor for testing. This decision not only expedited the setup process but also leveraged my existing knowledge of the architecture. I also revisited RISC-V compiler instructions and arguments that defined system parameters for memory and peripherals, drawing from resources I had encountered in previous competitions.

Overall, I was excited to build on this groundwork and eager to see where this project would lead me in the world of RISC-V and real-time systems.
