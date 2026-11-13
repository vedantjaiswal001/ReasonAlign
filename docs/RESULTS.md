# Results

All figures are transcribed from saved notebook outputs. The experiments are separate.

## Staged experiment — 62 questions (42 curated + 20 held-out)

| Stage | Correct | Answer accuracy | Format accuracy | Teacher-judged accuracy |
|---|---:|---:|---:|---:|
| Base Gemma 2 2B IT | 21/62 | 33.9% | 0.0% | 33.9% |
| SFT | 45/62 | 72.6% | 98.4% | 69.4% |
| SFT + DPO | 46/62 | 74.2% | 96.8% | 69.4% |
| SFT + DPO + KTO | 44/62 | 71.0% | 96.8% | 66.1% |

SFT produced the largest increase over the base model in this run. DPO added 1.6 percentage points over SFT. Adding KTO reduced answer accuracy by 3.2 points relative to SFT+DPO.

## Alignment ablation — 42 curated questions

| Method | Correct | Answer accuracy | Format accuracy |
|---|---:|---:|---:|
| SFT baseline | 35/42 | 83.3% | 100.0% |
| DPO (sigmoid) | 37/42 | 88.1% | 100.0% |
| IPO | 36/42 | 85.7% | 100.0% |
| Hinge / SLiC | 38/42 | **90.5%** | 100.0% |
| Robust-DPO | 37/42 | 88.1% | 100.0% |
| APO-zero | 37/42 | 88.1% | 100.0% |

Hinge/SLiC was highest in this saved ablation. On 42 questions, one answer changes accuracy by approximately 2.38 percentage points; treat the result as exploratory.

## Standalone KTO — 42 curated questions

| Stage | Correct | Answer accuracy | Format accuracy |
|---|---:|---:|---:|
| SFT baseline | 35/42 | 83.3% | 100.0% |
| SFT + KTO | 37/42 | **88.1%** | 100.0% |

The notebook reports +4.8 percentage points. This is a separate KTO-only run, not the KTO stage in the 62-question sequential run.

## Interpretation and cautions
SFT reliably taught the expected tagged output format on these test sets. Preference optimization effects varied by method and run. The results do not establish generalization to broad reasoning tasks. The teacher metric is model-based rather than human assessment, and the small benchmarks make percentage differences sensitive to individual questions.
