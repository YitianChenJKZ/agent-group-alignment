# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository state

This is a greenfield research repo with **no commits yet and no code**. It currently holds:

- `context.md` — the research brief (motivation, claims, modelling assumptions, open items). This is the spec; read it before writing any simulation code.
- `main.ipynb` — empty (0 bytes). Intended as the entry point for the model.
- `Anaconda3-2026.07-1-MacOSX-arm64.sh` — an ~880 MB installer sitting untracked in the working tree. Do not commit it; add it to `.gitignore` before the first commit.

Because nothing is established yet, there is no build, lint, or test setup to follow. When adding one, prefer the simplest thing that fits a notebook-driven simulation study rather than importing a full application scaffold.

## What the project is modelling

An agent-based model of how information propagates through a **mixed-speed** population of stochastic agents. The design decisions that follow from `context.md`:

- An agent is a probability function `P(action | state)` — deliberately simple stochastic agents, not LLM agents.
- **Speed** is the single differentiating attribute between agent types (fast vs. slow).
- The observable of interest is the spread of a piece of information through the population over simulation time, tracked by originating agent type.

The model exists to support three claims, which should map onto distinct experiments:

1. Fast agents preferentially interact with each other (clustering).
2. Information originating from fast agents dominates / crowds out slow-origin information.
3. Biasing fast agents toward consulting slow agents restores slow-origin propagation.

Claim 3 is the payoff — the intervention is a change to the *interaction/consultation graph*, not to individual agent policies. Keep the consultation-partner-selection logic a separately tunable component so the intervention is a parameter change rather than a rewrite.

## Unresolved design decisions

`context.md` flags these as open; don't silently invent answers, surface the choice:

- No operational metrics yet for "drowns out" (claim 2) or "compete with" (claim 3). These need concrete definitions (e.g. fraction of population holding each origin's information over time) before results mean anything.
- Two claims in the brief lack citations (agents outnumbering humans online; the OpenAI–HuggingFace incident).

## Environment

Full Anaconda distribution in the **`base`** env at `/opt/anaconda3` (Python 3.14). There is no
project-specific env; packages are installed into `base`. Run the notebook with `jupyter lab main.ipynb`.

Already available, so don't re-install: `numpy` `scipy` `pandas` `matplotlib` `seaborn` `plotly`
`networkx` `numba` `tqdm` `scikit-learn` `statsmodels` `joblib` `xarray` `h5py` `ipywidgets`
`pytest` `ruff` `black`.

Installed for this project from **conda-forge** (not on the default channel):

- `mesa` 3.5.1 — ABM framework. Its scheduler/activation machinery is the natural home for the
  mixed-speed dynamics; `model.agents.shuffle_do("step")` is the Mesa 3.x activation idiom.
- `SALib` 1.5.2 — sensitivity analysis, for parameter sweeps over speed ratios and consultation bias.

Notes for anyone extending the env:

- The default channel's `mesa` is `mesalib`, an unrelated OpenGL library. Always install the ABM
  package with `-c conda-forge`.
- conda-forge outranks `defaults` by priority, so a plain `conda install -c conda-forge ...` will
  also migrate `conda`/`openssl`/`ca-certificates`/`certifi` off `pkgs/main`. Pin them to their
  current versions to keep the solve minimal.
- Mesa 3.5 deprecates `Model(seed=...)` in favour of `Model(rng=...)`. Use `rng=` in new code —
  reproducible seeding matters for these experiments.
