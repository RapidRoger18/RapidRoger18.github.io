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

Inline assembly in C or C++ is specified using the asm or __asm__ keyword, and it follows this general form:
```C:
asm [volatile] (
    "assembly instruction" 
    : output operands 
    : input operands 
    : clobbered registers
);
```
- *Assembly Instructions*: The assembly code you want to execute.
- *Output Operands*: Values that are produced by the assembly code.
- *Input Operands*: Values that are used as inputs to the assembly code.
- *Clobbered Registers*: Registers that are modified by the assembly code.

**Clobber List:**<br>
The clobber list indicates which registers (or memory) the assembly code modifies. This information is crucial for the compiler to avoid using these registers for other purposes within the same code section, preventing potential conflicts and incorrect results.

***For Example in our case:***
```C:
asm volatile (
    "addi x17, x0, %0"
    :
    : "r" (GPIO_ENABLE_OUTPUT)
    : "x17"
);
```
- `"addi x17, x0, %0"`: The assembly instruction to execute.
- `:` (empty): No output operands.
- `: "r" (GPIO_ENABLE_OUTPUT)`: Specifies the input operand. Here ***%0*** will be replaced by ***GPIO_ENABLE_OUTPUT***.
- `: "x17"`: Indicates that the ***x17*** register is modified (or clobbered) by this instruction.

By listing x17 in the clobber list, the compiler understands that the value in x17 before this instruction cannot be relied upon afterward. This helps avoid issues with register allocation and ensures that the compiler does not make assumptions about the values in x17.