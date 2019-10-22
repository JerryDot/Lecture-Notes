Concurrent Algorithms & Data Structures
The Art of Multiprocessor Programming - Chapter 1 (revised first edition). Any references are to this textbook either by index or page number)

We want to concentrate where the concurrency is happening quite tightly (specifically in the datatypes)
And then we can be sequential in the result

Some big questions will be:

- What does it mean for a concurrent dataype to be correct? 
- How can we justify that an implementation of a concurrent datatype is correct? 
- How can we avoid a bottleneck in our implementation

Assumed knowledge:
- Techniques for reasoning about sequential programs such sa: loop invariants, data abstraction, abstract specification of datatypes, datatype invariants
- Standard Techniques such as: encapsulation, inheritance, stacks, queues, linked lists, has tables
- Some Concurrency topics such as: shared variables, race conditions, mutual exclusion, locks, deadlocks
- Some Java

## Styles

### Lock-based

Traditional used multiple locks, monitors and semaphores. Threads obtain locks (and could obtain multiple locks at the same time)

Typically doesn't scale well, leads to deadlocks and correctness reasoning must be done at the system level

### Message-passing

Here threads have no shared variables - instead variables are communicated via messages. This makes reasoning easier.

Can also be mixed with shared variables (with appropriate care)

It is good for large programs but there is a performance hit as it's a heavy-weight approach

### Data-type based concurrent programming

All concurrency here is based on a small number of concurrent datatypes. Code outside of these areas looks mostly the same as sequential programming eg operations are called on the datatypes which return results

This could be lock-based but that has a sequential bottleneck. Instead use different synchronisation techniques to allow multiple threads to operate at the same time. Each operation will appear to take place atomically at some point between its invocation and return. (Linearization)

## Example Problems
### _Calculate the primes under 1*10^9_
First way is to split into big blocks and search in parallel. But blocks with harder numbers will take longer.

Second way is to use load balancing: have a shared counter and each worker picks the next number to check. Naively this might not protect the counter from concurrent calls (example of a classical race condition).
We want to execute a line under mutual exclusion. One way to do that is a synchronized block:

`def getAndIncrement: long = synchronized{...}`

Some modern multiprocessor hardware can read and write in a single atomic hardware step. 

`java.util.concurrent.atomic.AtomicInteger` builds on this idea. It encapsulates an integer and provides various operations.
Then run ox.cads.util.ThreadUtil.runSystem(10, worker) etc to solve the problem.

### _Consensus Problem_
Turns out there is no lock-free solution to the consensus problem using only read-write variables

Hence AtomicInteger's special compareAndSet operation is pretty useful!

```
decision.compareAndSet(counter, myValue)
decision.getAndIncrement
```

## Limits of scaling

Ideally `1 processor ----> n processors` would give an n-fold speed-up. This is true if the threads can operate independently.

However assume some proportion p can be done in parallel and 1-p can be done sequentially. Then n processors would take time 1 - p + p/n (assuming it takes time 1 for 1 processor)

Therefore the speed up S = 1/(1-p+p/n)        - Amdahl's Law

Note that as n -> inf, S -> 1/(1-p). Therefore we want to keep p as high as possible to avoid sequential bottlenecks. Recently this is more of a focus area due to an increase in multi-core stuff
