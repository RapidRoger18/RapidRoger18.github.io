---
layout: post
title:  "BeagleV-Fire"
author: Atharva
categories: [ GSOC ]
tags: [Updates]
image: ../assets/images/BeagleV-Fire.png
description: "A little introduction about BeagleV-Fire board which will be used during my GSOC project"
featured: true
hidden: false
---

Fast forwarding to 1.5 weeks later I completed writing a wrapper module for integrating the PicoRV32 with the CAPE module on BeagleV-Fire. This module will be responsible for connecting the PicoRV32 CPU module to the memory modules for data transfers.

A CPU typically has 3 types of main memories, instruction/program memory, data memory(scratchpad RAM), and Stack memory. In a CPU these memories are bound by address spaces within which they can be accessed by the CPU. These assignments are very important as they define the sizes of the memory as well.

This `Wrapper` module instantiates memory modules and the CPU and assigns the pins and buses according to the assigned addresses of the memory modules. In our case we have decided to have 128KB of Program Memory, 4KB of RAM and and 4KB of Stack memory.

The address spaced de