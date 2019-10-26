Recap: Buchi's Theorem proved via a detour with Ramsey's Theorem

The key idea was the *type* of a finite word. This is an edge-coloured bipartite graph over two copiers of the states that says what runs of the automaton are possible on this word and what runs include an accepting state. Full definition is on slide 35

* Slide 36 - lemma before we can show closure under complementation
* Slide 37 - using Ramsey's theorem to lead us to the desired factorisation for the lemma
* Slide 38 - need to revisit

need to get some intuition for types, for runs and how they all interact

Slide 41 now ready to prove Buchi's complementation result. The automaton recognising the complement of a Buchi-recognisable language can be effectively constructed from the automaton recognising L

## Decision Problem 2: Universality

Given a Buchi automaton A over SIGMA, is L(A) = SIGMA^omega?

First attempt, given A construct the complement and then use th nonemptiness algorithm on the complement. PRoblem is that this gives an algorithm that is exponential in space and time

Proposition - the universality problem is PSPACE-hard. We can prove this by reduction from the UP for FSA - Thm Meyer-Stockmeyer 1972. This states that the problem is PSPACE-complete for FSAs roughly - check understanding.

Aim: Transform FSA A to Buchi A' s.t. the languages are each universal iff the other is too.
