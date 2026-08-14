# Training Recipe — Mooré–French Machine Translation

## 1. Objective

This training recipe documents the configuration used for LoRA-based adaptation of a Llama 3.3 70B model for **Mooré → French machine translation**.

The recipe is intended to provide a reproducible record of the model adaptation experiment.

## 2. Base model

- **Model family:** Meta Llama 3.3
- **Model size:** 70B parameters
- **Adaptation method:** LoRA
- **Task:** Mooré → French machine translation

## 3. Dataset

The adaptation experiment used the project's adapted **Mooré–French parallel dataset**.

The documented corpus contains:

- **1,176 parallel segments**
- **48,781 Mooré tokens**
- **34,654 French tokens**
- **83,435 tokens total**

The dataset preparation and annotation methodology are documented in:

- `dataset/dataset_description.md`
- `dataset/annotation/DATASET_ANNOTATION_MOORE_FRENCH.md`

The adapted dataset itself is not stored in the repository.

## 4. Fine-tuning method

The model was adapted using **Low-Rank Adaptation (LoRA)**.

The recorded LoRA configuration is:

| Parameter | Value |
|---|---|
| LoRA rank (`r`) | 64 |
| LoRA alpha | 128 |
| Target layers | All linear layers |

## 5. Training configuration

| Parameter | Value |
|---|---|
| Number of epochs | 3 |
| Learning-rate scheduler | Cosine |
| Warmup ratio | 0.05 |
| Gradient clipping | 1 |

## 6. AutoScientist recipe

The configuration was selected and documented as part of an **AutoScientist** training recipe.

### Recorded configuration

| Parameter | Value |
|---|---|
| Model | Meta Llama 3.3 70B |
| Method | LoRA |
| Dataset | Adapted Mooré–French dataset |
| Epochs | 3 |
| LoRA rank | 64 |
| LoRA alpha | 128 |
| Target layers | All linear layers |
| Scheduler | Cosine |
| Warmup ratio | 0.05 |
| Gradient clipping | 1 |

## 7. Reproducibility notes

This document records the parameters currently available from the training recipe.

Additional parameters should be documented when available, including:

- learning rate;
- effective batch size;
- per-device batch size;
- gradient accumulation;
- sequence length;
- optimizer;
- precision or quantization settings;
- random seed;
- training hardware;
- software and library versions;
- checkpointing strategy;
- evaluation configuration.

These parameters should only be added when they are known from the actual experiment.

## 8. Model weights

Model weights and checkpoints are intentionally excluded from this Git repository.

The repository's `.gitignore` excludes common model-weight formats and the `finetuning/model_weights/` directory.

## 9. Evaluation

Evaluation results are documented separately in:

`benchmark/benchmark_results.md`

The benchmark documentation should distinguish between training configuration, validation results, and final test results where applicable.

## 10. Limitations

The training experiment is based on a relatively small low-resource parallel corpus.

The corpus contains 1,176 aligned Mooré–French segments and was assembled from heterogeneous sources. Consequently, model performance should be interpreted in the context of:

- limited corpus size;
- source-domain heterogeneity;
- variation in orthography and translation style;
- possible domain-specific vocabulary;
- limitations of the available evaluation data.

Further experiments may be required to assess generalization to unseen Mooré text and domains.