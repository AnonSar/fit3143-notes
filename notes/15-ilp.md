[← Return to Index](https://github.com/cjmlgrto/fit3143-notes/)

# Instruction-Level Parallelism
- ILP stands for Instruction-Level Parallelism
- ILP of a program is a measure of the number of instructions a program can execute simultaneously
- ILP involves executing multiple independent instructions in parallel
- Increases the performance of processors by making the most efficient use of processors

## Pipelining
- Pipelining involves sequentially passing processes through a series of stages
- In ILP, the pipeline involves fetching instructions from memory, decoding the instruction, executing the instruction and then writing its result to a register file
- In this way there is a continuous flow of each stage at all times and each process begins in a sequential order

## Superscalar vs VLIW (Very Long Instruction Word)
- In both, we have multiple **execution units** that are dedicated to executing multiple instructions simultaneously.
- Superscalar involves hardware scheduling and scheduling is dynamic
- VLIW involves software scheduling and operates on multiple instructions/word

## Data Dependencies
Dependencies are responsible for determining which instructions can be scheduled where, and whether they can be executed in parallel or must be serialised. Following are some of the dependencies:
- **Read-after-write dependency,** which says that the data must be read, but is currently being written to. That is, if r1 is written to in instruction 1 and used in instruction 2, instruction 2 cannot be rearragned prior to instruction 1: it depends on teh value written by instruction 1.
    - **Load-use dependency**, which involves reading data stored directly after it has been loaded from an address
    - **Define-use dependency**, which involves reading data stored directly after it has been defined
- **Write after Read dependency**, which involves writing data into a register directly after it has been utilised, and it is only correct so long as the register has been utilised before being written into
- **Write after Write dependency** — when an instruction uses a value that is overwritten in subsequent instructions, the initial must be done before the latter for the current result to be achieved
**NOTE:** **Write After Read** & **Write After Write** dependencies, both of them happen to be false dependencies since they can be eliminated with the help of register renaming.

## Instruction Scheduling
There are thre primary methods of instruction scheduling:
- **Static scheduling**, which involves finding independent instructions at compile time (it is done by the compiler in software)
- **Dynamic scheduling**, which involves finding independent instructions at runtime (which is done by the processor — the hardware)
- **Hybrid Scheduling**, which involves a combination of both static scheduling and dynamic scheduling where both the compiler and the hardware work together to find optimal scheduling for instructions.

## Preserving Sequential Consistency
* When instructions are executed in parallel, processor must be careful to preserve the sequential consistency of the operations.

## Types of Consistency
* **Strong Consistency** — preserves the actual execution order
* **Weak Consistency** which may execute out of order as long as the result is still correct.

## How fast can we go in ILP?
* Performance of ILP is limited by
	* Underlying algorithm (may have dependencies that cannot be removed)
	* Compiled code (compiled code may introduce false dependencies and code that is difficult to pipeline)
	* Actual hardware (resource restrictions)
56321``
