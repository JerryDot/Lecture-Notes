A w-automaton is parametrised by Acc

Start from slide 49/73

Remember inf(p) : the set of states that occur infinitely often in run p [p placeholder for ro]

Definitions of Buchi and Muller w-automatons

Rabin: If Acc is a set of pairs of subset of Q, a run is Rabin accepted if the run avoids infinitely visiting a  member of set E<sub>i</sub> and infinitely visits a member of set F<sub>i</sub>

Streett is the negation of Rabin

Parity: Acc is specified by a priority function (can consider it as a finite colouring of states). A run is accepting if the least priority that occurs infinitely often in p is even

Want to be able to create an algorithm that takes a Muller w-automaton as input and outputs an equivalent Buchi automaton

Is there a difference between a Buchi w-automaton and a Buchi automaton?

slide 54 - all these are equivalent. Muller is nice because it is determinisable and closed under complementation. Buchi is simple and easy to understand but not determinisable. 

//What does determinisable mean here?//

Note that Buchi conditions are instances of Rabin - given F, the Rabin condition is {{empty, F}}.