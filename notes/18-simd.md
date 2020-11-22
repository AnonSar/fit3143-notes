[← Return to Index](https://github.com/cjmlgrto/fit3143-notes/)

# SIMD Architectures
* SIMD systems offers:
     * simplicity of programming
     * regularity of structure
     * scalability (both in size and performance)
     * wide applicability
* 2D array of processing elements (2D processing array)
* All processors execute the same instruction in parallel where each processor has its own local memory
* Processors are programmable
* Data can propagate through the processor array
* Advantages:
   * **Multiple data** can be loaded at once
   * **Operations** can be applied to all of the data in one operation
* Disadvantages:
   * **Not all operations** can be done with SIMD
   * Implementation requires **human labour** in terms of coding
   * Programming with particular **SIMD instruction sets** can involve numerous low-level challenges.

## Granularity
* Fine-grained systems (Such systems try to map each individual data element to one processing element as closely as possible)
* Course-grain systems (Such systems relax the above restrictions where an individual PE can handle multiple data elementsI)
* Dependent on data density passed to the processors

## SIMD Connectivity
* Near-neighbour
* Tree
* Pyramid
* Hypercube

## Processor Complexity/Precision
* Single bit (fine-grain used for image processing)
* Integer (A compromise solution used for vision or general computing)
* Floating-point (Coarse-grain usually used for scientific computing)

## Local Autonomy
* Different sections at the hardware level can have different design as above 
* (i.e. a hypercube with single bit and another with a fine-grain granularity at near-neighbour with floating point, etc.)

## Intel SIMD Extensions (SSE)
* Streaming SIMD Extensions (SSE): Single Instruction, Multiple Data (SIMD) instruction set extension for **x86 architecture**.
* SSE new data type:
   * SSE introduced one new data type called **128-bit packed single-preccision floating-point data type** to the IA-32 architecture.
   * This data type consists of four IEEE 32-bit single-precision floating-point values packed into a double quad word.
   * This data type is operated on XMM registers or in the memory.
* SSE instructions are divided into four sub-groups:
   * Packed and scalar single-precision floating-point instructions:
        * Data Movement Instruction
        * Arithmetic Instruction
        * Logical Instrcution
        * Comparison  Instruction
        * Shuffle Instructions 
        * Conversionn Instructions
   * 64-bit SIMD integer instruction
   * State Management Instructions
   * Cacheability control, prefetch and memory ordering instructions
* In **SSE packed single-precision floating-point instruction**, each source operand contains four single-precision flaoting-point values and the destination operand contains the results of the operation performed in parallel.
* The **SSE scalar single-precision floating-point instruction**, operate on the least single doubelwords of the two source operands. The three most significant double-word of the first operand are passed as it is through the destination.
* **SSE2 (Streaming SIMD extensions 2)**
  * SSE2 adds new math instructions for double-precision floating point and also extends MMX instruction to operate on 128-bit XMM registers.
  * Enables programmers to perform SIMD math on virtuallly any datatype entirely with the XMM registers, without the need to use the (legacy) MMX/FPU registers.
  * SSE2 extensions add the following features to teh IA-32 architecture:
    * Five data types:
        * 128-bit packed double-precisoin floating-point
        * 128-bit packed byte integers
        * 128-bit packed word integers
        * 128-bit packed doubleword integers
        * 128-bit packed quadword integers
    *  Instructions to support additional data types and extend existing SIMD integer operations:
        * Packed and scalar double-precision floating-point instructions
        * Additional 64-bit and 128-bit SIMD integer instructions
        * 128-bit versions of SIMD integer instructions introduced with the MMX technology and the SSE extensions
        * Additional cacheability-control and instruction-ordering instructions.
* The above features extends the IA-32 architecture's SIMD programming model in three important ways:
    * Permits higher precision computations to be carried out in XMM registers.
    * Additional flexibility is provided with instructions that operate on single double-precision floating-point values located in the low quad-word of an XMM register.
    * Provide an ability to operate on 128-bit packed integers.
* SSE2 Data Types:
    * Packed double-precision floating point
    * 128 bit packed integers
* SSE2 Packed & Scalar Double-Precision Floating-Point Instructions:
    * The **packed double-precision floating-point instructions** perform SIMD operations similarly to the packed single-precision floating-point instructions. Each source operand consists of the two double-precision flaoting-point values and the destination operand consists the results of the operation.
    * The **scalar double-precision floating-point instructions** operate on the least significant bit of the two operand and the most significant bit of the first operand is copied as it is to the destination operand.
* **SSE3 (Streaming SIMD extensions 3)**
    * 13 new instructions were introduced in SSE3.
    * SSE3 did not introduce any new data type or programming model.
    * The most significant change in SSE3 was its capability to work horizontally in a register as opposed to the more or less strictly vertical operation of all the previous SSE instructions.
    * SSE3 also added instructions to perform different operation on SIMD data
    
* **SSE4 (Streaming SIMD extensions 4)**
    * SSE4 comprises of two sets of extensions: SSE4.1 and SSE4.2
    * SSE4 didn't introduce any new datatype
    * SSE4 does not support operations on 64-bit MMX registers;
* **AVX (Advanced Vector Extensions)** is an advanced versions of SSE announced by Intel featuring a **widened data path from 128 bits to 256 bits** and **3-operand instructions**. 
## Intel MultiMedia Extension (MMX)
* Intel MMX technology introduced single-instruction multiple-data (SIMD) capability into the **IA-32 architecture**:
  * 8 of 64-bit MMX registers (MM0 through MM7) 
  * 64-bit packed integer data types
  * New instructions to perform SIMD operations on packed integers
 * Intel addressed the shortcomings of the MMX technology with the help of SSE, a greatly expanded set of SIMD instructions with 32-bit floating point support.
 * SSE added eight new 128-bit registers known as XMM0 through XMM7, which made it easy to perform SIMD and FPU operations at the same time.
 * The x86-64 extensions add a further eight registers XMM8 through XMM15.
 * SSE added the following features to IA-32 architecture:
   * Eight XMM registers in non-64-bit modes and sixteen XMM registers in 64-bit mode.
   * MXCSR registers which provides control and status bits for operations performed on XMM registers.
   * 128-bit packed single-precision floating-point data type.
* These features extend the IA-32 architecture's SIMD programming model in the following ways:
   * The ability to perform SIMD operations on **four packed single-precision floating-point values** enhances the performance of IA-32 processors for advanced media and communications applications that use computation-intensive algorithms to perform repetitive operations on large arrays of simple, native data elements.
   * The ability to perform  **SIMD single-precision flaoting-point operations** in XMM registers and SIMD integer operations in MMX registers provides greater flexibility and throughput for executing applications that operate on large arrays of floating-point and integer data.
   * Cache control instructions provide the ability to stream data in and out of XMM registers without polluting the caches and the ability to prefetch data to selected cache levels before it is actually used;
## Advantages of SSE over MMX:
  * The CPU is unable to work on both floating point and MMX data at the same time.
  * MMX only works on integers while the SSE works on both i.e. integers and floating point data.
  * Hence, SSE provides more flexible and has much more use than MMX.
   





