# Foundations of Computer Science

Slides: www.cs.ox.ac.uk/teaching/materials19-20/FOCS

Core of this course is contained within: **Introduction to the Theory of Computation** (2nd edition by Mike Sipser)

>"What can computers do?"

Problems can be defined by f: inputs ---> outputs

First reduce problems down to "decision problems" (loking specifically at language recognition challenge)

Note definitions of:
* language 
* "recognises" (only relevant in cases where it can loop forever - otherwise it is the same as decides)
* "decides"
* machine

Can define FA as a 5-tuple (Q, SIGMA, delta, qNought, F)

* Q is set of states
* SIGMA is the alphabet of the input strings
* delta is the transition function delta: Q x SIGMA -----> Q
* q<sub>0</sub> is the initial state e  Q
* F is the "accept" states so is a subset of Q 

Then we can define the semantics as a DFA (d for deterministic)
where a DFA accepts word = abcdef...xyz e SIGMA STAR (set of strings of the alphabet)
if there is a sequence of states r s.t.:
rNought = qNought
delta(rEye, letterEyePlusOne) = rEyePlusOne
rFinal is in F

FA has small fixed memory (just remembers the state as it moves from letter to letter)
2-state FA has 1 bit of memory
Computers are essentially FAs but with massive memory to the point where it can basically be considered infinite
Markov Chains are based on FSA but much more complex
Some models can solve many problems; others very few
eg Turing Machine can solve many problems but can be slow
We are happy if we can solve a problem with a simple model. It shows the problem is easy