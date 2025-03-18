---
title: LLVM Note - Instruction Selection In LLVM
date: 2022-03-17 00:18:11
tags:
- Compiler
- LLVM
---

# Instruction Selection In LLVM

## Instruction Selection Method

- FastISel
- SelectionDAGISel
- GlobalISel

related hooks, like how to specify which isel method to use
- in `TargetConfig::addCoreISelPasses` will choose a valid isel method

### FastISel

- llvm ir based
- fast
- used in O0

#### workflow

llvm ir -> machine instruction with virtual register

#### how to impl

1. define a class inherit from `FastISel`
2. override a virtual function `fastSelectInstruction`, then emit each opcode in llvm ir which is target dependent

### SelectionDAG based ISel

- should lowering to DAG first from llvm ir
- will do several times legalize and combine in instruction selecting, includes:
  - type legalize then combine
  - vector legalize then combine
  - dag legalize then combine
- will do heuristic schdeule on DAG after selected to MachineDAG

#### workflow

llvm ir -> lowering to DAG -> initialize DAG -> combine -> type legalize and combine -> vector legalize and type legalize and combine -> dag legalize and combine -> insturction selection -> instruction scheduling(will introduce later)

#### how to impl

1. define a class inherit from `SelectionDAGISel`
2. override the entry of selection isel `Select()`
3. override most of all `selectXXX` virtual function to select instruction, usually named as `<TargetName>DAGToDAGISel()`

#### what is lowering

lowering define some legalization info and other rules for DAG builder when SelectionDAG is initialized

### GlobalISel

TODO