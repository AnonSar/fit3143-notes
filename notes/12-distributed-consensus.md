[← Return to Index](https://github.com/cjmlgrto/fit3143-notes/)

# Distributed Consensus
**Consensus** may be formulated as follows:
**Distributed Consesus Problem**
* A distributed system contains n processes
* Every process has an initial value in a mutually agreed domain
* The challenge is to devise an algorithm, which in spite of the occurrence of failures, allows processes to reach an irrevocable decision that fulfils the following conditions:
	* **Termination** — every (non-faulty) process must eventually come to a decision
	* **Agreement** — the final decision of every (non-fault) process must be identical
	* **Validity** — if every non-faulty process begins with the same initial value V, their final decision must be V

## Consensus in Async
* If there is no failure, then reaching an agreement is trivial
* Reaching consensus however, becomes surprisingly difficult when one or more members fail to execute actions
* Assume that at most K members (K>0) can fail
* In a fully async system, it is impossible to reach consensus even if K = 1

## Bivalent and Univalent States
* **Bivalent** — if there exists at least two distinct executions leading to two distinct decision values
* **Univalent** — a state from which only one decision value can be reached. Univalent state states can be either 0-valent or 1-valent.
* Consider a best-of-five-sets tennis match between A and B. If the score is 6-3, 6-4 in favour of A, the decision state is bivalent, since anyone can win at this point. However, if the score becomes 6-3, 6-4, 7-6 in favour of A, then the state becomes univalent.

## Byzantine General Problem
Lamport’s Proof:

* For a system of n+1 nodes, there cannot be more than n/3 faulty nodes
* Alternatively, “there must be more than 3m troops in an army with up to m traitors to launch a concerted attack”
