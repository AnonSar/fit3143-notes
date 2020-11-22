[← Return to Index](https://github.com/cjmlgrto/fit3143-notes/)

# Data Parallel Architectures
* Data Parallel Architecture consists of:
	* Memory, which passes on to
		* Consists of 8 bit wide memory sells
	* Two registers, which passes on to
		* Consists of 8 bit wide registers each
	* 8 Bit ALU, which passes back to memory
		* Consists of 8 single but ALUs

## Connectivity
How do we access data in different processors?

### Nearest Neighbours 
* Mapping **_spatially coherent data_** into SIMD systems
	* Spatially correlated, like images
* Common to connect NSEW (cardinal directions), but diagonal has also been implemented
* This technique is usually applied to massively parallel systems and it happens to be:
	* Scalable
	* Simple to implement

### Trees and Graphs
* Problems expressed as graphs
	* e.g. database searching, model machines
* No mathematically regular structure due to which architecture requires reconfigurability
* Binary and quad trees common
* Communication bottlenecks can occur going through roots of subtrees

### Pyramid
* This structure is a combination of mesh and tree:
	* Supports nearest neighbour plus tree communication
	* Local communication  mesh
	* Global communication of tree
* Useful for data stored at multiple resolutions like images

### Hypercube
* 2^N processors where each processor has N links
* Fault tolerant
* Shorter pathways than mesh management

## Different Data Parallel Architectures
* SIMD — program pipelined into multiple processors then back
* Systolic/Pipelined — grab data, then processes through stages of processors
* Vectorising — vector unit can operate on vector memory
* Associative and Neural — objects, databases, etc

### Principle Characteristics of Data-Parallel Systems

| Property | SIMD | Systolic | Pipeline | Neural | Associative |
| --- | --- | --- | --- | --- | --- |
| Programmability | Good | Fixed | Fixed | Good | Poor | Good |
| Availability | Good | Poor | Poor | Good | Poor | Poor |
| Scalability | Good | Fixed | Fixed | Fixed | Fixed | Good |
| Applicability | Wide | Narrow | Narrow | Wide | Narrow | Wide |
