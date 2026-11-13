# Methodology

## Research question
How do SFT and preference-alignment objectives affect structured output compliance and final-answer correctness for Gemma 2 2B IT?

## Model and runtime
- Base checkpoint: `google/gemma-2-2b-it`.
- Optional teacher: `google/gemma-2-9b-it`.
- PyTorch, Transformers, TRL, PEFT, Datasets, Accelerate and bitsandbytes.
- 4-bit model loading with LoRA adapters (QLoRA-style parameter-efficient fine-tuning).
- Recorded Kaggle runtime: Tesla T4 with 15.6 GB reported memory.

## Target format
```text
<reasoning>...</reasoning>
<answer>...</answer>
```
This is a generated output schema. It should not be interpreted as a faithful trace of the model's internal computation.

## SFT
The primary notebook uses TRL `SFTTrainer` and prepares completion-only labels so the prompt is masked from the supervised loss. Its recorded training input contains 3,126 examples.

## DPO
The preference data contains chosen and rejected completions. The main run uses TRL `DPOTrainer` with an adapter-disabled base as the reference policy to avoid a second full model copy. The recorded run uses 1,559 preference pairs.

## KTO
KTO uses unpaired desirability labels. The notebook maps chosen completions to desirable and rejected completions to undesirable, forming 3,118 labels from 1,559 pairs in the primary run. The standalone run uses 1,200 pairs (2,400 labels).

## Ablation
The ablation notebook starts each objective from the same SFT checkpoint and compares DPO (sigmoid), IPO, Hinge/SLiC, Robust-DPO and APO-zero on the same 42-item benchmark. KTO is optional and did not complete in the combined ablation execution because of a CUDA out-of-memory error; a separate notebook isolates KTO.

## Evaluation
The staged run uses 62 questions: 42 curated and 20 held-out. The ablation and standalone KTO runs use 42 curated questions only. Reported measures are final-answer accuracy, tagged-format accuracy, and (in the primary staged experiment) Gemma 2 9B teacher-judged accuracy. Scores across different evaluation sets must not be merged into one leaderboard.
