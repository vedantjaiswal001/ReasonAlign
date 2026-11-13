# ReasonAlign

Structured Reasoning Fine-Tuning and Preference Alignment for Small Language Models.

ReasonAlign studies how supervised fine-tuning and preference optimization affect structured explanation-style outputs, answer accuracy, and format reliability for Gemma 2 2B IT.

## Target format
```text
<reasoning>...</reasoning>
<answer>...</answer>
```

> A generated reasoning section is not evidence that the text faithfully represents the model's internal computation. This project measures output format and benchmark answer correctness, not reasoning faithfulness.

## Setup at a glance
- Base model: `google/gemma-2-2b-it`
- Optional teacher: `google/gemma-2-9b-it`
- Training: 4-bit QLoRA with LoRA adapters
- Methods: SFT, DPO, KTO; ablation with IPO, Hinge/SLiC, Robust-DPO and APO-zero
- Stack: PyTorch, Transformers, TRL, PEFT, Datasets, Accelerate, bitsandbytes
- Recorded environment: Kaggle, Tesla T4, 15.6 GB GPU memory

## Results
Experiments use different evaluation sets and must be interpreted separately.

**Staged experiment — 62 questions (42 curated + 20 held-out)**

| Stage | Answer accuracy | Format accuracy |
|---|---:|---:|
| Base Gemma 2 2B IT | 33.9% | 0.0% |
| SFT | 72.6% | 98.4% |
| SFT + DPO | 74.2% | 96.8% |
| SFT + DPO + KTO | 71.0% | 96.8% |

Teacher-judged accuracy: 33.9%, 69.4%, 69.4%, and 66.1%, respectively.

**Alignment ablation — 42 curated questions**

| Method | Answer accuracy | Format accuracy |
|---|---:|---:|
| SFT baseline | 83.3% | 100.0% |
| SFT + DPO | 88.1% | 100.0% |
| SFT + IPO | 85.7% | 100.0% |
| SFT + Hinge / SLiC | **90.5%** | 100.0% |
| SFT + Robust-DPO | 88.1% | 100.0% |
| SFT + APO-zero | 88.1% | 100.0% |

**Standalone KTO — 42 curated questions**

| Method | Answer accuracy | Format accuracy |
|---|---:|---:|
| SFT baseline | 83.3% | 100.0% |
| SFT + KTO | 88.1% | 100.0% |

The standalone KTO run is separate from the KTO stage in the 62-question sequence. Hinge/SLiC's result is exploratory on 42 questions; one item changes accuracy by about 2.38 percentage points.

## Methodology
1. SFT teaches the tagged response format using completion-only loss.
2. DPO learns from chosen/rejected preference pairs; the primary notebook uses the adapter-disabled base as reference.
3. KTO uses unpaired desirable/undesirable labels derived from the preference pairs.
4. A controlled ablation starts objectives from the same SFT checkpoint and compares DPO, IPO, Hinge/SLiC, Robust-DPO and APO-zero.
5. Evaluation reports answer accuracy, format compliance and, in the primary run, Gemma 2 9B teacher-judged accuracy.

## Repository contents
- `notebooks/staged-sft-dpo-kto.ipynb` — full SFT → DPO → KTO experiment and staged evaluation.
- `notebooks/preference-objective-ablation.ipynb` — controlled preference-loss comparison.
- `notebooks/standalone-kto.ipynb` — isolated KTO training and evaluation.
- `docs/METHODOLOGY.md` — methodology and training design.
- `docs/RESULTS.md` — experiment tables and interpretation.
- `docs/REPRODUCIBILITY.md` — Kaggle setup and input requirements.
- `docs/LIMITATIONS.md` — evaluation and claim limitations.

## Reproduce
Experiments were run in Kaggle. Attach the Gemma 2 2B IT model, relevant SFT and DPO JSON datasets, and (optionally) Gemma 2 9B IT for teacher grading. Use a GPU accelerator and run the appropriate notebook top-to-bottom. The recorded main environment includes PyTorch 2.10.0+cu128, Transformers 5.16.1, TRL 1.12.0, PEFT 0.20.0, Datasets 5.0.1 and Accelerate 1.14.0. Exact inputs and notes are in `docs/REPRODUCIBILITY.md`.

## Limitations
The benchmarks are small and cover a limited number of categories. Format correctness does not establish reasoning faithfulness. Teacher grading is model-based. The staged KTO result decreased accuracy relative to SFT+DPO, while standalone KTO improved over its own baseline; these findings should remain distinct. The project does not claim broad reasoning gains or production readiness.

## Author
Vedant Jaiswal · [GitHub](https://github.com/vedantjaiswal001) · [LinkedIn](https://www.linkedin.com/in/vedjais/)

See `CITATION.cff` for citation metadata.
