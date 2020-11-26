[← Return to Index](https://github.com/cjmlgrto/fit3143-notes/)

# Distributed Transactions
## Atomic Transactions
An **atomic transaction** gives a view that either a set of operations is all completed or none of them is completed

* First, a process declares to all other processes (involved in a transaction) that it is starting the transaction
* The processes exchange information and perform their specific operations
* The initiator announces that it wants all the other processes to “commit” to all the operations done up to that point
* If all processes agree to commit, the results are made permanent
* If at least one of the processes refuse, all the states — usually, opened files/databases (on all machines) — are reversed to the point before starting the transaction

## Transaction Processing
### System Model for a Transaction
* A system consists of independent processes where each process may fail at random
* No communication error may be encountered
* A “stable storage” is available

### Stable Storage
* **Stable Storage** guarantees no data is lost (unless physically damaged)
* Note: Data in RAM disappear when power is turned off — data in a disk becomes inaccessible if the head crashes. Thus, they are not stable storages
* Stable Storage can be implemented with a pair of disks:
	* Each block on drive 2 is a copy of the corresponding block on drive 1
	* When a block (of data) is updated, the block on drive 1 is updated then verified
	* Then, the same block on drive 2 is updated and verified (aka as a backup)
	* If the system crashes after the update of drive 1 but before the update of drive 2, the block of the two drives are compared and the blocks on drive 1 are copied to drive 2 after system reboot
	* If checksum error is encountered because of a bad block, the block is fixed by copying from the disk without an error

## Transaction Primitives
* Programming a transaction requires _special primitives_ that must be supplied by the OS or by the programming language — either as system calls, library functions etc.
* Examples of primitives are
	* **Begin transaction**
	* **End transaction**
	* **Abort transaction**
	* **Read**
	* **Write**
* **Begin Transaction** and  **End Transaction** are the two primitives that specify the scope of the transaction and all the primitives between these primitivies form the transaction.
	
## Properties of Transactions
### Atomic
* A transaction happens indivisibly to the outside world
* i.e. either all of the operations of the transaction are completed or not
* The other processes cannot observe intermediate states of the transaction

### Consistency
* A transaction does not violate system invariants (true rules of the system)

### Isolation
* Even if more than one transactions are running simultaneously, the order that they occur doesn’t matter as the end result is the same
* Also called “Serialisable”

### Durability
* Once a transaction commits, changes are permanent
* No failure _after the commit_ can undo the results or cause these to be lost

## Nested Transactions
* **Nested transactions** are just sub-transactions of a transaction (a transaction containing other transactions)
* A problem of nested transactions is that if the parent is aborted, the entire system needs to undo changes — but if the changes in the sub-transactions have already been committed, they need to be undone — but _undoing a commit is a violation_
* To alleviate the above problem, we define the characterstics of a nested transaction:
	* **Permanence of a sub-transaction** is only valid in the world of its direct parent and is invalid in the world of further ancestors
	* **Permanence of the results** is only valid for the outermost transaction (that is, the top level transaction that is itself not nested in another transaction)

### Addressing Transaction Violation
* Create a private copy of all objects in the system for each sub-transaction
* If a sub-transaction commits, its private copy replaces its parent’s copy

## Implementation of Atomic Transactions
* Implementing means:
	* Hiding operations within a transaction from outer processes
	* Making results visible only after commit
	* Restoring old state of the transaction is aborted
* Two ways to restore old state:
	* Private workspace
	* Write-ahead log

### Private Workspace
* When a process starts a transaction, it is given a **private workspace** containing all the objects (including data and files) of the system.
* The data within the workspace is written back when the transaction commits
* Problem: cost of copying every object in the private workspace is high
* Solution: 
	* if a process only reads the objects, then there's no need for the private copy of those objects.
	* if a process needs to update an object, then only copy that particular object in the private workspace of the process.
	* Use **indices to objects** in order to reduce the **number of copy operations**
	* When an object needs to be updated, a copy of it's index and the objects are made in the private workspace
	* The private index is updated
	* On commit, the private index is copied to the parent’s index (i.e. replacing pointers)
	* If the transaction is aborted, then the object in the private workspace and it's private index in the workspace, both of them are discarded.

### Write-ahead Log
* Before any changes are made, a record (log) is written to a **write-ahead log** on stable storage
* The log contains the following information
	* Which transaction is making the change
	* Which object is being changes
	* What the old and new values are
* Only after the log has been written successfully, the change is made to the object
* If the transaction committed, a commit record is written to the log
* If the transaction aborts, the log can be used to rollback to the original state (or even, recover from crashes)

## Distributed Commit
### Two-Phase Commit Protocol
* The action of committing a transaction must be done *instantaneously* and *indivisibly*
* In a distributed system, the commit requires *cooperation* of multiple processes (which may be) on different machines
* Two-phase commit protocol is the most *widely-used protocol* to implement atomic commit

### Process
* One process acts as the coordinator
* The other participating processes are subordinates (“cohorts”)
* The coordinator writes an **entry “prepare”** in the log on a stable storage and sends the other processes involved (the subordinates) a message telling them to prepare
* When a subordinate receives the message, it checks to see if it is ready to commit, makes a log entry, and sends back its decision
* After collecting all the responses, if all the processes are ready to commit, the transaction is committed (otherwise, aborted)
* The coordinator writes a log entry and sends a message to each subordinate informing it of the decision
* The coordinator’s writing commit log actually means committing the transaction and no rolling back occurs no matter what happens afterward

### Properties
* The protocol is **highly resilient** in the face of crashes because it uses stable storage
* If the coordinator crashes after a “prepare” or a “commit” log entry, it can still continue from sending a “prepare” or “commit” message upon restart
* If a subordinate crashes after writing a “ready” or “commit” log entry, it can still continue from sending a “ready” or “finished” message upon restart

## Three Phase Commit Protocol
### Assumptions
* Each site uses the write-ahead log protocol
* At most one site can fail during the execution of the transaction

### Basic Concept
* Before the commit protocol begins, all the sites are in state q
* If the coordinator fails while in state q1, all the cohorts perform the timeout transition, thus aborting the transition
* Upon recovery, the coordinator performs the failure transition
