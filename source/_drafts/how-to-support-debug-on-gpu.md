---
title: how-to-support-debug-on-gpu
tags: 
- Micro-Arch
- Debugging
- Heterogeneous Computing
---

# How to support debug on GPU

## Before the Sharing

First time to write a blog in English, worthy to memorize.

Recently I'm interested by the debugging tech on heterogeneous computing system, CPU with GPU for example, especially the micro-arch design. I'm lucky that I was part of a developper toolchain team, I know a bunch of guys who are really familiar with debugging tech. 

In the beginning of 2018, our team were involved in the first NPU chip project of HUAWEI and we developed logging system(focusing on the software implementation), trace tool, IDE and the prototype of the debugger. Why was just a prototype, which is complicated and no comments here. Anyway, some guys were experts in that team, like my memtor Zheng. We communicated these days and concluded a brief design about the debugging system on GPU/NPU system.

## Background of Debugging

Basic debug actions include: setting breakpoints, running by step, veiwing variables information(type, address, temporary value). In this blog, I will focus on the hardware support requirements to the "breakpoint setting" and "running by step".

In CPU system, OS provides various of system interruptions to support debugging user's applications. For example INT3 instruction of X86 help trigger a interrupt for the debugger, debugger will catch the signal and process following debugging action, like viewing the value of temporary variable. This is a software level breakpoint. And also there is a hardware way to set a breakpoint. Hardware may design several register for storing breakpoint address, which is the PC address. When polling the breakpoint registers and meeting the PC is equal to the value stored in the breakpoint register, the PC issue module will stop issuing, which implements break action of user's program.

## GPU Design for supporting Debugging

Both software and hardware ways to set a breakpoint, the hardware should support instruction level interrupt in the micro arch design.