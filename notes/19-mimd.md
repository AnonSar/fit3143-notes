[← Return to Index](https://github.com/cjmlgrto/fit3143-notes/)

# MIMD (Multiple Instructions Multiple Data)

# MIMD Architectures
* Distributed Memory MIMD
	* Processor/memory pairs are replicated and they are connected via an interconnection network
* Shared Memory MIMD
	* Processors and memories are replicated independently and they happen to be connected via an interconnection network

## Distributed Memory Machine
* In distributed memory machine, each processor has its own local memory which is not shared with other processors
* Access to local memory module is faster than remote memory
* Hardware access the remote memory via
	* Load/Store primitive
	* Message passing layer
* **Cache memory** for local memory traffic
* Message can be sent from:
	* Memory to memory
	* Cache to cache

### Advantages
* **Less contention** in local memory traffic than in shared memory traffic
* Highly scalable
* Don’t need sophisticated **synchronisation features** like monitors, semaphores
* Message passing serves dual purpose
	* To send data
	* Provide synchronisation

### Disadvantages
* Load balancing is difficult
* Message passing can lead to **synchronization failures**, including deadlock
	* Blocking Send → Blocking Receive
	* Blocking Receive → Blocking Send
* Entire data structure needs to be copied which can be an intensive process
* The overhead for small messages is high relative to the size of the message.

## Shared Memory Architecture
* All processors have **equal access** to shared memory
* **Local Caches** reduce
	* Memory traffic
	* Network traffic
	* Memory access time

### Advantages
* No need to partition code or data
* Occurs on the fly
* No need to move data explicitly
* Existing programming languages or compilers can be used.

### Disadvantages
* **Synchronisation of resources** is difficult
* **Lack of scalability**
	* IPC (Inter Process Communication) becomes bottleneck
* Scalability can be addressed by
	* High throughput, low latency network
	* Cache Memories (but this can lead to coherence problem)
	* Distributed Shared Memory architecture

## Distributed Shared Memory
* Non-Uniform Memory Access **(NUMA)**
* Cache Coherent Non-Uniform Memory Access **(CC-NUMA)**
* Cache-Only Memory Access **(COMA)**

## Problems of Scalable Computers
* Tolerate and hide the latency of **remote loads**
	* Worse if output of one computation relies on another to complete
* Tolerate and hide idling due to synchronisation among processors

### Tolerating Latency
* **Cache Memory**: Involves maintaining the local copy of remote memory which ultimately reduces the cost of remote access. This technique might introduce cache coherence problem
* **Prefetching**: This technique involves prefetching the data before it is needed. This is already implemented to some extent thus reduces the cost of implementation but it can increase the network load.
* **Threads + Fast Context Switching**: This technique involves using **local multithreading** in order to minimise the time spent idling.
**NOTE:** These solutions don’t solve sync issues and in order to solve the sync issues, we must make use of latency-tolerant algorithm.

## Design Issues of Scalable MIMD
Scalable MIMD is subject to several design issues:
* **Processor Design** should consider pipelining and the issues that arise from running instructions in parallel.
* **Interconnection Network Design** should be designed to be scalable, high bandwidth, low latency.
* **Memory Design** maybe complex if shared memory design is used.
	* Cache coherence
* I/O Subsystem
	* Parallel IO
