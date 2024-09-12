---
title: how-to-support-debug-on-gpu
tags: 
- Micro-Arch
- Debugging
- Heterogeneous Computing
---

# How to support debug on GPU

First time to write a blog in English, worth to memorize.

Recently I'm interested by the debugging tech on heterogeneous computing system, CPU with GPU for example, especially the micro-arch design. I'm lucky that I was part of a developper toolchain team, I know a bunch of guys who are really familiar with debugging tech. 

In the beginning of 2018, our team were involved in the first NPU chip project of HUAWEI and we developed logging system(focusing on the software implementation), trace tool, IDE and the prototype of the debugger. Why just a prototype? 