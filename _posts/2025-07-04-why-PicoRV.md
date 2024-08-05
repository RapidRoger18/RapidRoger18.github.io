---
layout: post
title:  "BeagleV-Fire"
author: Atharva
categories: [ GSOC ]
tags: [Updates]
image: ../assets/images/BeagleV-Fire.png
description: "Week 4 Implementation: A little introduction about BeagleV-Fire board which will be used during my GSOC project"
featured: true
hidden: false
---

With a month into the project timeline it was now time to finally decide which processor to use. I had left this dicision since I made a propsal for the project as i didn't have sufficient data in this respects but no more. This topic was also discussed breifly during the first meeting and it was decided to find a good operating processor that can be relied on, but the discussion ended then and there.

With a month into the project I started to interface the PicoRV core within the BVF Gateware. Initially I decided to add it as a option to CAPE component of the Gateware. This started with reading and understanding the 3000 lines of Verilog code for PicoRV32. Luckily the  README provided on the PicoRV repository was enough to give me an idea of its external parameters and input and output signal. All I had to do was to use these signals to correctly map to peripherals and memory to access the Processor corectly.

This is when I was suggested by my mentor to give a few reason on why I was using the picoRV32 CPU. Some of the reasons are :
- PicoRV32 is a size optimized, hence it will not occupy a lot of resources on BeagleV-Fire's FPGA, allowing users to try on diffrent logic.
- PicoRV32 is very well documented as well as community supported CPU.
- PicoRV32 is provided compiler support with custom linker scripts within its parent repository.
- PicoRV32 offers lots of different options like ISA extentions, interupt support, debug console, and also a few speed optimizations for  