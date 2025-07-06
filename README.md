# BSc Thesis Materials
In this repository, you will find all of the supplementary materials created and used for my Bachelor’s Thesis on Parademo, including high-fidelity prototype mock-ups, the core algorithm implementations with their unit tests, and the full usability-study questionnaire with its results.


## Hi-Fi Prototype Screen Mock-ups
This repository contains a PDF which consists of all 24 screens of the high-fidelity Parademo Prototype. The interactive clickable version can be found here: https://app.uizard.io/p/bea508d1
 

## Core Algorithms & Unit Tests
This repository contains the reference implementations for the three core algorithms of Parademo developed for my Bachelor's thesis. Parademo is a prototype liquid-democracy platform that supports vote delegation, secure tallying, and reputation scoring. In this repository, you’ll find concise, well-tested Python modules for Delegation Routing, Vote Tallying, and Reputation Computation, along with unit tests to validate their correctness and performance.

### Delegation Routing Algorithm
The Delegation Routing algorithm ensures that every token in the system finds its final voter without ever creating cycles. When a user delegates their vote to another, the algorithm walks downstream through the delegation chain to detect if the original user would reappear; if so, the delegation is rejected. Once all delegations are cycle-safe, the final holder of each token is resolved by following the chain to a user with no outgoing delegation, with path compression applied so that subsequent lookups run in linear time relative to the size of the graph.

### Vote Tallying Algorithm
The Vote Tallying algorithm takes the final-holder mapping from Delegation Routing and the ballots cast by those holders and aggregates token weights into four categories: FOR, AGAINST, ABSTAIN, and NOT_VOTED. For each final holder, we calculate how many tokens they represent, then add that weight to the appropriate category based on their vote (or lack thereof). This process touches each token exactly once and runs in O(N) time, making it efficient even for millions of tokens.

### Reputation Computation Algorithm
The Reputation Computation algorithm builds a directed graph of delegations and runs the Random-Surfer PageRank method (teleport probability α = 0.15) to assign each user a reputation score. After convergence (typically ~25 iterations), delegates who fail to vote on tokens entrusted to them are penalised by scaling their PageRank score by `1 - penalty × (unvoted_entrusted_tokens / total_tokens)`. Finally, scores are renormalized to sum to 1, yielding a reputation metric that reflects both direct and indirect trust as well as accountability.  


## Usability-study Questionnaire and Results
This repository includes the full user-study questionnaire PDF, along with its Results Dashboard PDF. 
