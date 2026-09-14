# Agent Group Alignment

Sources for Artificial Society research blogs on AI agent group alignment,
plus the simulations behind their figures.

## Papers

### Agent Based Modeling for Group Alignment

An agent-based model of a population of fast agents (AI) and slow agents (humans) placed at
random on an n x n grid with a Moore neighbourhood. 

The outcome measure is the C-index: the ratio of slow-origin to fast-origin information at
equilibrium, divided by the ratio of slow to fast agents. 

Three hypotheses are tested against closed-form predictions:

1. Fast agents mainly hear from other fast agents
2. Fast-origin information crowds out slow-origin information
3. Raising P_sf, so fast agents consult slow agents more, restores C = 1 for limited rho.

Files: abm_group_alignment.tex, appendix.tex, abm_group_alignment.pdf,
hypo1+hypo2.ipynb, hypo3.ipynb, Figures/

### AI Agent Group Alignment through the Lens of Principal-Agent Problem Framework

A social norm instillation model where each agent has a hidden latent space norm and a visible output norm. 

Files: Principal-Agent Group Alignment/

## Running the notebooks

```
python3 -m venv .venv
source .venv/bin/activate
pip install numpy matplotlib joblib jupyter
jupyter notebook
```

Every simulation uses a seeded random number generator, so the figures reproduce exactly.
hypo3.ipynb runs a few hundred seeds per parameter point in parallel through joblib and takes
a while.

## Building the papers

```
pdflatex abm_group_alignment.tex
```

Figures are read from Figures/.
