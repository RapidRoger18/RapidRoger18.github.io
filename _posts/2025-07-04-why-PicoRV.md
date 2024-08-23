---
layout: post
title:  "Choosing PicoRV32: A Balanced Softcore CPU"
author: Atharva
categories: [ GSOC ]
tags: [Updates]
image: ../assets/images/BeagleV-Fire.png
description: "We landed on PicoRV32 as the softcore CPU for our project, balancing resource efficiency and community support with the trade-offs of performance and code complexity."
featured: true
hidden: false
---

With a month into the project timeline, it became imperative to finalize the processor choice—a decision I had initially deferred since the project proposal phase due to insufficient data. This topic was touched upon briefly during our first meeting, where we agreed to seek a reliable, well-supported processor, but the conversation had paused there.

Now, having gathered enough insights, I began integrating the PicoRV core into the BVF Gateware. My initial approach was to incorporate it as an option within the CAPE component of the Gateware. This task started with delving into the 3,000 lines of Verilog code that constitute the PicoRV32. 

Fortunately, the README provided in the PicoRV repository was comprehensive enough to give me a clear understanding of its external parameters and input/output signals. The key challenge was mapping these signals correctly to the peripherals and memory to ensure proper processor access.

At this stage, my mentor suggested that I provide a rationale for choosing PicoRV32. Here are some reasons:

- **Size Optimization:** PicoRV32 is highly size-optimized, meaning it won't consume excessive resources on the BeagleV-Fire's FPGA. This allows users to experiment with various logic implementations.

- **Documentation and Community Support:** PicoRV32 is well-documented and enjoys robust community support, which is crucial for troubleshooting and enhancements.

- **Compiler Support:** The CPU comes with compiler support and custom linker scripts within its parent repository, simplifying the development process.

- **Flexible Options:** PicoRV32 offers various features, including ISA extensions, interrupt support, a debug console, and speed optimizations for faster instruction execution.

However, there are also some drawbacks to consider:

- **Performance:** The architecture of PicoRV32 is customized for minimal size rather than high performance, leading to longer instruction execution times.

- **Code Complexity:** All PicoRV modules are implemented within a single Verilog file, making it challenging to navigate the codebase.

After weighing these pros and cons, we decided to proceed with PicoRV32 as the Softcore CPU for this project. Its balance between resource efficiency and flexibility made it the ideal choice, despite some small trade-offs in performance and code structure complexity.