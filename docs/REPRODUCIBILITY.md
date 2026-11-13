# Reproducibility

These experiments were run in Kaggle notebooks; this repository is not a packaged local training application.

## Runtime setup
1. Open the relevant notebook in Kaggle.
2. Select a GPU accelerator and enable Internet for initial package installation.
3. Attach the required model checkpoints and JSON datasets through Kaggle's Add Input panel.
4. Run cells in order.

The saved outputs report a Tesla T4 GPU with 15.6 GB memory. The notebook guidance also mentions T4 ×2 or P100 as possible accelerator choices.

## Inputs
- Base model: `gemma-2-2b-it` Transformers checkpoint.
- Optional teacher for the main run: `gemma-2-9b-it`.
- SFT JSON files covering areas such as mathematics, coding, summarisation, science and other examples.
- DPO preference JSON files containing chosen/rejected completions.
- Ablation and standalone KTO runs also require the SFT checkpoint produced by the main training notebook.

The original data/model assets are external Kaggle inputs and are not redistributed in this repository. Attach the same revisions to reproduce the saved setup.

## Recorded package versions
| Package | Version in notebook output |
|---|---:|
| PyTorch | 2.10.0+cu128 |
| Transformers | 5.16.1 |
| TRL | 1.12.0 |
| PEFT | 0.20.0 |
| Datasets | 5.0.1 |
| Accelerate | 1.14.0 |

The notebooks also install bitsandbytes. CUDA and driver versions depend on the Kaggle runtime image.

## Notebook sequence
- `staged-sft-dpo-kto.ipynb`: baseline evaluation, SFT, DPO, KTO, stage-wise evaluation and adapter/results export.
- `preference-objective-ablation.ipynb`: attach base model, SFT checkpoint and preference data; compare preference objectives. KTO is optional and may need a separate run if memory is insufficient.
- `standalone-kto.ipynb`: attach base model, SFT checkpoint and preference data; compare SFT with SFT+KTO.

## Notes
The main staged run records approximately 271 minutes for SFT, 165 minutes for DPO and 222 minutes for KTO. Runtime varies. Use the same data, checkpoint, evaluation examples and configuration when comparing runs. A saved notebook output does not guarantee identical results on a fresh execution.
