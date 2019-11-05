Update slides since they have changed

Last lecture ended with multi-tape Turing Machine - which looks fairly trivially like it can be simulated by a single-tape TM. It can. (note that these multi-tape TMs have fixed number of tapes)

We will from now be aiming for the Church-Turing Thesis (and investigate the languages that cannot be decided by TMs)

Sometimes we use <O> (the crinkled brackets that look like greater than/less than) to emphasise that we refer to the string coding of object O (rather than the object itself)

Note that the Church-Turing thesis is a belief - not a theorem. Not possible to prove this because the definition of "physical computer" is not well-defined.

## Decidable and semi-decidable

L = all polynomial equations with integer coefficients that have a solution in the integers. This is CE

If it were decidable then this would mean we had a method of determining whether any equation has an integer solution or not. It was possible to prove that this problem cannot be decided for diophantine equations

L = all C programs that crash on some input. This is CE

If it were decidable then life would be sweet...

Consider L defined by Accept = { <M,x> : M is a Turing Machine that accepts string x }. This is CE

---

Why is "Semi-decidable called CE?

An enumerator for a language L = {w1, w2, w3, ...} is a TM machine that write on a separate output tape:

#w1#w2#w3#w4#...

This output can be infinite. A language is CE iff there exists an enumerator enumerating it.

---

Next goal is to prove that there are CEs that aren't decidable and there are languages that are not CE.

---

Does Cantor's diagonalisation argument assume the AoC?