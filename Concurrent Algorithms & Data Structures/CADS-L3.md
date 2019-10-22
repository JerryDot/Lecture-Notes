Last Lecture: 2 Mutual Exclusion

Start this lecture on 45 (Lamport's Bakery Algorithm)

Convinced ourselves that it is deadlock free because the labels are increasing. Correct because if there were two threads in the critical section (CSA, CSB), when the processes are in here then the (label<sub>A</sub>, A) << (label<sub>B</sub>, B). This ultimate leads to the sequence of operations occurring in a successful way. (revisit theory for full understanding. Lemmas 2.6.2, 2.6.3 in The Art of Multiprocessor Programming)

Uses lexicographic ordering on pairs of labels and thread ids

Same as post office ticket system intuitively

### Number of Location
It used 2n locations to achieve multiple exclusion with n threads. We can reduce this to n by storing the flags and the labels in the same location (since only thread i writes to both).

Can we achieve deadlock-free mutual exclusion using fewer locations? No! (assuming that each location can be accessed only by atomic _read_ and _write_ operations). If we allow for other atomic operations then we can achieve mutual exclusion for n threads with a _single_ shared location.

We'll prove with n=3; proof for n will be a generalisation of this. (p37-40)

### Multiple locks and deadlock

As we have seen, if we have a system with multiple locks, the system can deadlock, even if each lock is deadlock-free. 

Theorem due to Dijkstra:

Suppose _< is a partial order on the finitely many, dead-lock free locks of a system. Suppose further that whenever a thread tries to acquire l, if it already holds lock l', then l'< l. Then the system is deadlock-free

Proof: suppose we can reach a deadlock then we can obtain an infinite sequence of locks... #!

Therefore this can be used to avoid deadlocks - just pick a partial order over the locks and make sure that threads follow this order when acquiring multiple locks. Eg array `lock` of `n Locks`, then define locks(0) < locks(1) < ... < locks(n-1) and require that you cannot acquire lock i if you already have a lock j with j > i

## Linearizability

Principle 1: Operation calls should appear to happen in a one-at-a-time sequential order

Principle 2: If two operations are concurrent, their effects could occur in either order. But if operation op1 finished before op2 starts, then op1's effect should occur before op2's effect

The combination of these principles is Linearization

A LockBasedQueue is linearizable by using the total order defined by the order in which the threads hold the lock

It tends to be easy to argue for correctness in concurrent datatypes that use exclusive locks. However, it follows from Amdahl's Law that datatypes that use exclusive locks are less desirable than ones that use finer locks or no locks at all. We need ways of specifying datatypes that can allow concurrent usage.

## Histories
Check slide 10 for some definitions (the subscript should be on the call word rather than op). Basically we want to split up processes into events - method invocations and response events. A _history_ is a sequence of such events.

A return event _matches_ an invocation if they have the same object and thread. A method call is represented by its invocation and the next matching return.

A history is _sequential_ if it alternates between invocations and matching returns. We want to say that if any possible history can be equivalent to a sequential history, then this is enough for it to be linearizable.

Slide 13