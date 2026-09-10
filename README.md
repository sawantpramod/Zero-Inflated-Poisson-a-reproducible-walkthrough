# Zero-Inflated Poisson: a reproducible walkthrough

Companion code for the article *"When the zeros are doing something else"* —
a step-by-step look at why a plain Poisson fit under-predicts zeros, and
what a Zero-Inflated Poisson (ZIP) model actually buys you.

Three standalone scripts, each runnable on its own, that build from a
real classroom dataset to a full Poisson / ZIP / Negative Binomial
comparison.

## What's here

| # | Script | What it shows |
|---|--------|---------------|
| 1 | `scripts/01_classroom_zero_gap.py` | Observed vs. Poisson-expected late-arrival counts for 100 students — the motivating gap |
| 2 | `scripts/02_zip_simulation.py` | Simulates ZIP data with known π and λ; shows a plain Poisson fit under-predicts zeros |
| 3 | `scripts/03_zip_model_comparison.py` | Fits Poisson, ZIP, and NB to the same simulated data; compares them on log-likelihood, AIC, BIC |

## Setup

```bash
git clone https://github.com/<your-user>/zero-inflated-poisson.git
cd zero-inflated-poisson
python -m venv .venv
source .venv/bin/activate         # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

## Run

Run the scripts **in order** — script 3 reuses the CSV written by script 2.

```bash
python scripts/01_classroom_zero_gap.py
python scripts/02_zip_simulation.py
python scripts/03_zip_model_comparison.py
```

## Outputs

| File | Written by |
|------|------------|
| `figures/classroom_zero_gap.png`   | script 1 |
| `figures/zip_histogram.png`        | script 2 |
| `outputs/data/zip_simulated_y.csv` | script 2 |

`outputs/` is gitignored — every run regenerates it from scratch, and
because the random seed is fixed, the numbers are identical on every
machine.

## A note on honesty

The simulation in script 2 is deliberately constructed so that we
*know* the true zero-generating mechanism. That lets us say
"Poisson missed the mark because of structural zeros" without
overclaiming.

On real data, the same statistical pattern — more zeros than a
Poisson fit predicts — is only ever *evidence consistent with* a
structural-zero story, not proof of one. Script 3 makes that
distinction explicit: AIC and BIC compare relative fit under stated
assumptions; they do not verify that a separate zero process exists.
That case has to be made on domain grounds.

## License

MIT — see `LICENSE`.
