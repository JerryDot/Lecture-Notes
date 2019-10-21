# Course Details

*This markdown was written using the Markdown All in One VSCode extension*

http://whirl.cs.ox.ac.uk/blog/short-term-ml-research-advice/

Shimon Whiteson

Department of Computer Science, University of Oxford

Based on material from Sutton and Barto.

Summary quote of reinforcement learning scenario:
>How can an intelligent **agent** learn from experience how to make decisions that maximise its **utility** in the face of **uncertainty**

The system receives feedback through the reward system which places this in between the supervised and unsupervised ML approaches in terms of the quality/completeness of feedback.

# Differences from Supervised Learning

* There are no examples of correct behaviour.
* The agent is active in the learning process and thus has partial control over the data obtained for learning.
* Agent must learn on-line
  * It maximises performance during learning (not afterwards). Eg you want to get the optimal winnings from a casino; not work out how to get the optimal winnings the next time you visit.
  * If you were preparing in a simulated environment etc then this might be called Sample-based planning - mostly a semantic difference.

# Sutton's reward hypothesis

See this link for more details: http://incompleteideas.net/rlai.cs.ualberta.ca/RLAI/rewardhypothesis.html

> That all of what we mean by goals and purposes can be well thought of as maximization of the expected value of the cumulative sum of a received scalar signal (reward).

Some uncertainty caused by the word "well".

Humans must decide what the reward function is for any given situation.

Notice this runs into the Reward design problem which is a critical AI safety concern.

# Armed bandit problems

There is no "state" situation in the traditional K-armed bandit problem. Each arm has an unknown stochastic payoff. The goal is to maximise cumulative payoff over some period. This captures some basic challenges in RL

Extends to the Contextual bandit problem where there is some outside state as well and the payoffs depend on the observed outside state at each play.

In principle could be treated as multiple simulatnesous bandit problems and estimate 

>Q(s,a) = E[ R | s, a ]

Here R is the reward of the arm given the state information and the action. Q is the value of the action a in the state s.

# Full problem

For an Agent in an envrionment, at each step an action a<sub>t</sub> is taken. This then affects the reward r<sub>t+1</sub> **and** the state s<sub>t+1</sub>, so that the next state is different given different actions.

Eg with K-armed bandit problem this now means we have to consider looking for a jackpot state.

This leads us to the credit assignment problem. If a long sequence of actions leads to a large positive reward at the end then how can it determine to what degree each preceding action deserves credit?

This was solved by Bellman by formalising Markov Decision Processes and deriving the Bellman equations which is a hugely important idea in AI

# MDP

A formal model of the sequential decision problem. Assume fully-observable, stationary and possibly stochastic.

* Discrete time t = 0, 1, 2, ...
* States are s ∈ S
* Actions are a ∈ A(s) for each s
* Transition function is P<sup>a</sup><sub>ss'</sub> = p( s' | s, a )
* Reward function is R<sup>a</sup><sub>ss'</sub> = E[ r | s, a, s' ]
* There is a planning horizon H or discount factor 0 < ɣ < 1

We also need the Markov Property - that the current state is a sufficient statistic for the agent's history.

As a result we can restrict the search to **reactive policies**.

In every MDP there exists at least one optimal deterministic reactive policy

Return function:
>R<sub>t</sub> = r<sub>t+1</sub> + ɣr<sub>t+2</sub> + ɣ<sup>2</sup>r<sub>t+3</sub> + ...

This is episodic so represent this as transition to an absorbing state

State-Value function of a policy π:
>V<sup>π</sup>( s ) = E<sub>π</sub>[ R<sub>T</sub> | s<sub>t</sub>=s ]

Action-value function of a policy π:
>Q<sup>π</sup>( s, a ) = E<sub>π</sub>[ R<sub>t</sub> | s<sub>t</sub>=s , a<sub>t</sub>=a]

We can then rewrite the State-Value function recursively by using the transition model giving us the Bellman equations. This is a set of linear equations (one for each state). The solutions to these equations define the value of π.