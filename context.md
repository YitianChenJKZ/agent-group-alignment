# Agent Based Modeling for Group Alignment

**Author:** Yitian Chen
**Date:** September 2026

## Motivation

AI agents are expected to outnumber humans on the internet in the near future, which makes it important to align the behaviour of *groups* of agents, not just individuals, so that collective behaviour conforms to values humans accept.

The specific problem this project targets: agents that are individually aligned can become misaligned once they start working alongside other agents. Alignment therefore has to be applied at the level of the collective, on a global scale, rather than agent by agent.

## Key goals

The project aims to demonstrate three claims about how information moves through a mixed-speed collective of agents:

1. **Fast agents cluster.** Agents that act quickly interact mainly with each other rather than across the whole population.
2. **Fast information dominates.** Information originating from fast agents propagates rapidly through the collective and drowns out information originating from slow agents.
3. **Intervention restores balance.** When fast agents are encouraged to consult slow agents more often, information from slow agents can propagate and compete with information from fast agents.

Claim 3 is the practical payoff: it suggests a lever for group alignment — adjusting consultation patterns rather than retraining individual agents.

## Modelling approach and assumptions

The model rests on two simplifying assumptions:

- Mixed swarms can be modelled with simple stochastic agents.
- A stochastic agent can be represented as a probability function over actions given a state: `P(action | state)`.

Agent "speed" is the key differentiating variable between agent types, and the quantity of interest is the propagation of information through the population over time.

## Open items

Several claims in the source draft are flagged as needing support:

- Citation for the projection that AI agents will soon outnumber humans online.
- Citation for the OpenAI–HuggingFace incident used as evidence that individually aligned agents become misaligned in groups.
- No metrics or experimental setup are specified yet — the three claims above need operational definitions (e.g. how "drowns out" and "compete with" are measured).
