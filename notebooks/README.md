# Experiment Notebooks

The three notebooks below are the executable experiment records included with this repository. They were originally run in Kaggle; model checkpoints and source datasets remain external Kaggle inputs and are not bundled here.

| Notebook | Purpose |
|---|---|
| [staged-sft-dpo-kto.ipynb](staged-sft-dpo-kto.ipynb) | Base evaluation followed by SFT, DPO and KTO, with stage-wise evaluation and optional Gemma 2 9B teacher grading. |
| [preference-objective-ablation.ipynb](preference-objective-ablation.ipynb) | Compares DPO, IPO, Hinge/SLiC, Robust-DPO and APO-zero from a common SFT checkpoint. |
| [standalone-kto.ipynb](standalone-kto.ipynb) | Isolated KTO run comparing the SFT checkpoint with SFT+KTO on the 42-item benchmark. |

See [Reproducibility](../docs/REPRODUCIBILITY.md) before executing the notebooks and [Results](../docs/RESULTS.md) for the saved output tables.