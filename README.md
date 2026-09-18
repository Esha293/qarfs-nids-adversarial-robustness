# QARFS: Quality-Aware Robust Feature Selection

Code accompanying the paper *"Adversarial Robustness of Feature-Selected Network Intrusion Detection Systems: A Comparative Analysis of Feature Importance and Quality."*

## Overview

This repository contains the experimental pipeline for QARFS, a feature-selection
framework that combines Random Forest feature importance with an independent,
measurable feature-quality score through a tunable weighting parameter α. The
main script evaluates full-feature, quality-only, importance-only, QARFS-α
(0.00–1.00), random, and mutual-information-based 16-feature representations
under a bounded, model-aware black-box adversarial attack on the
CSE-CIC-IDS2018 dataset.

## Repository contents

- `qarfs_experiment.py` — the full experimental pipeline (data loading,
  feature-quality scoring, RF importance, QARFS α-sweep, mutual-information
  baseline, per-configuration retraining and adversarial attack, results
  export).
- `make_figures.py` — generates the paper's figures directly from the result
  CSVs produced by `qarfs_experiment.py`.
- `requirements.txt` — exact package versions used to produce the results
  reported in the paper.

## Setup

\`\`\`bash
python -m venv venv
source venv/bin/activate   # On Windows: venv\Scripts\activate
pip install -r requirements.txt
\`\`\`

## Data

This repository does **not** include the CSE-CIC-IDS2018 dataset. Download
the 10 official CSV files from the
[Canadian Institute for Cybersecurity](https://www.unb.ca/cic/datasets/ids-2018.html)
and place them in a local `data/CSE-CIC-IDS2018/` folder.

## Running the experiment

Edit the `DATA_DIR` and `RESULTS_DIR` paths near the top of
`qarfs_experiment.py` to point at your local dataset and desired output
folder, then run:

\`\`\`bash
python qarfs_experiment.py
\`\`\`

This produces the following files in `RESULTS_DIR`:

- `step_G34_CSE_CIC_IDS2018_QARFS_feature_quality.csv`
- `step_G34_CSE_CIC_IDS2018_QARFS_feature_selection.csv`
- `step_G34_CSE_CIC_IDS2018_QARFS_clean.csv`
- `step_G34_CSE_CIC_IDS2018_QARFS_adversarial.csv`
- `step_G34_CSE_CIC_IDS2018_QARFS_summary.csv`
- `step_G34_CSE_CIC_IDS2018_QARFS_audit.csv`

## Generating figures

Edit `IN_DIR` and `OUT_DIR` near the top of `make_figures.py` to match your
`RESULTS_DIR` above, then run:

\`\`\`bash
python make_figures.py
\`\`\`

## Notes on reproducibility

Random Forest training is seeded (`random_state=42`) but is not guaranteed
bit-exact across different scikit-learn/numpy versions. The pinned versions
in `requirements.txt` are the exact versions used to produce the results
reported in the paper. Minor (<1%) numerical drift may occur on different
library versions; this does not affect the qualitative conclusions.

## Citation

If you use this code, please cite the associated paper (full citation to be
added upon publication).

## License

MIT License — see `LICENSE`.
