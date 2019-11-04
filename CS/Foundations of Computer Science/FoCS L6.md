Last lecture was about NPDAs. But they are limited by their stack-based version of memory.

NPDAs are most useful for membership tests. Programming languages are often described by CFG. Other tests include emptiness and equivalence. If the CFL is decided by a deterministic PDA then these problems are quite simple. for NPDA it is not simple however - not clear how we should do this.

We want to be able to recognise eg a^n * b^n * c^n for all n. We can't do this with a NPDA? What is the simplest alteration that adds general purpose memory to our machine?

# Turing Machine!

New capabilities:
* Infinite tape
* Can read OR write to tape
* Read/write head can move _left_ and right 
(so input is not necessarily "consumed" when read). TMs allow us to calculate anything that is calculatable. The "head" does not know where it is - it starts in initial state and can move but is not able to "read its own position on the tape".

"finite control" = current state of the tape

d takes the current state (that is not alreday in acceptance or rejectance). Then head reads the currently seen letter. Then the state changes given the current state and the letter read by the head, a new letter is written (that may be the same) and then the head is moved Left or Right.

Note you cannot be allowed to move off the left end of the tape.

We can assume that there is a single acceptance state (if not then just make sure the transitions from all possible acceptance states go to a single "final" acceptance state).

A _configuration_ is determined by the contents of the tape (always a finite initial string), the state and the head location.

The next step is completely determined by the current configuration

Shorthand:
string u;q;v with u,v in GAMMA*, q in Q

Tape contents uv followed by blanks, that is in state q with its head on the first letter/symbol of v.

Now we can have word inputs that result in an infinite loop! Note that inputs are written on the left-most squares of tape.

## Some language definitions

So now the distinction between recognises and decides is important

The set of accepted strings L(M) is the language that M recognises

If M rejects every x not in L(M)  then it decides L

The set of languages recognised by a TM is called semi-decidable or computably enumerable or recursively enumerable

The set of languages decided by a TM is called Turing-decidable or computable or recursive

These definitions were required because sometimes it is useful to separate accepting states from those that either reject or loop. Sometimes useful the other way - to separate the rejecting states from states that either loop or accept

See slide 15