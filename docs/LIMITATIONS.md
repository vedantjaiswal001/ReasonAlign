# Limitations

- **Small benchmarks:** reported evaluations contain 42 or 62 questions, covering only a limited set of categories.
- **Different test sets:** the staged run includes 20 held-out items; the ablation and standalone KTO runs use the 42 curated questions only.
- **Reasoning faithfulness:** generating a `<reasoning>` section does not prove it faithfully reflects the model's internal computation. The project tests output formatting and answer correctness, not mechanistic faithfulness.
- **Preference sensitivity:** the main staged run reports lower answer accuracy after KTO than after SFT+DPO, while the separate KTO-only run improves over its own SFT baseline. Report these results independently.
- **Teacher grading:** Gemma 2 9B IT is a model judge; it may make mistakes and is not human evaluation.
- **Compute constraints:** notebooks depend on Kaggle GPU resources and external model/data attachments. A combined ablation execution encountered CUDA out-of-memory during KTO.
- **Claim scope:** these experiments do not establish general-purpose reasoning, robust performance across domains, safety, or production readiness.
