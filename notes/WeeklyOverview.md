# Weekly Overview

### Week 6

* **Election**
    * Assumptions and how the election amongst the process works
    * Bully Algorithm
    * Ring Algorithm
    
* **Atomic Transaction**
    * About Atomic Transaction
    * Primitives used to implement atomic transaction
    * Properties of Atomic Transaction
    * Nested Transaction
    * How to implement Atomic Transaction:
        * Private Workspace
        * Write Ahead log
    * How to commit transaction atomically
        * Two Phase Commit Protocol
        * Three Phase Commit Protocol
        
*  **Concurrency Control**
    * Concurreny Control Algorithms:
        * Uinsg locks
        * Using Timestamps
        * Being optimistic
    * Locks
        * About locking algorithm 
        * Optimization in the Locking algorithm   
        * Two-Phase Locking in order to guarantee serializability
        * Strick Two-Phase Locking in order to avoid cascading abort
             * Advantages of Strict Two-Phase Locking
             * Disadvantages of Two-Phase Locking
        * Lock Granularity
    * Timestamps
        * About Timestamps (Read and write timestamps)
        * Timestamp algorithm working
    * Optimistic
        * About
        * Transaction progress phases
        * Validation conditions
