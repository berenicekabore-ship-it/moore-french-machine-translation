\# Moore–French Machine Translation



A low-resource machine translation research project focused on \*\*Mooré → French\*\* translation.



The project explores the preparation of a manually curated Mooré–French parallel corpus, dataset adaptation, LoRA-based fine-tuning, and evaluation of language adaptation approaches for Mooré.



\## Project status



The project is currently under development.



The dataset documentation and annotation methodology have been prepared. Model fine-tuning, benchmarking, and research analysis are being documented as the project progresses.



\## Dataset



The current parallel corpus contains:



| Statistic | Value |

|---|---:|

| Parallel segments | 1,176 |

| Mooré tokens | 48,781 |

| French tokens | 34,654 |

| Total tokens | 83,435 |



The corpus is a \*\*segment-level Mooré–French parallel corpus\*\* designed primarily for low-resource machine translation research.



The primary translation direction is:



\*\*Mooré → French\*\*



\### Data sources



The corpus combines several categories of material, including:



\- educational and community materials from the Guiè context in Burkina Faso;

\- Mooré–French biblical material, including passages from Genesis;

\- additional independent Mooré–French parallel examples used to improve lexical and structural coverage.



The project acknowledges the provenance and contribution of source materials associated with:



\- \*\*AZN-CIER de Guiè\*\*

\- \*\*Alliance Biblique du Burkina Faso\*\*



Detailed information about dataset preparation, annotation, quality control, statistics, and provenance is available in:



\- \[`dataset/dataset\_description.md`](dataset/dataset\_description.md)

\- \[`dataset/annotation/DATASET\_ANNOTATION\_MOORE\_FRENCH.md`](dataset/annotation/DATASET\_ANNOTATION\_MOORE\_FRENCH.md)



\## Dataset methodology



The corpus was manually prepared and quality-controlled.



The preparation process included:



1\. extraction or transcription of source material;

2\. correction and formatting;

3\. semantic alignment of Mooré and French segments;

4\. removal of incomplete or unaligned entries;

5\. duplicate removal;

6\. proper-name harmonization where appropriate;

7\. meaningful segmentation;

8\. manual quality-control checks.



The dataset is annotated at the \*\*segment level\*\*. It does not provide systematic morphological, syntactic, phonological, POS, named-entity, or word-level alignment annotations.



Because the corpus was assembled from heterogeneous sources, residual variation in orthography, vocabulary, register, and translation style may remain.



\## Model adaptation



The project investigates model adaptation for Mooré–French translation using parameter-efficient fine-tuning approaches, including \*\*LoRA\*\*.



The repository is intended to document:



\- dataset preparation;

\- training configuration;

\- fine-tuning procedures;

\- model adaptation experiments;

\- evaluation and benchmarking.



Training documentation is located in:



\- \[`finetuning/training\_recipe.md`](finetuning/training\_recipe.md)

\- \[`finetuning/autoscientist\_config.yaml`](finetuning/autoscientist\_config.yaml)



Model weights are not stored in the repository by default.



\## Evaluation



Translation evaluation and benchmark results will be documented in:



\[`benchmark/benchmark\_results.md`](benchmark/benchmark\_results.md)



The benchmark section will be updated as experiments are completed.



\## Research report



The scientific analysis of the project is being documented separately in:



\[`research/research\_report.md`](research/research\_report.md)



The research report will provide detailed information about the research methodology, experiments, results, discussion, limitations, and references.



\## Repository structure



```text

moore-french-machine-translation/

│

├── README.md

│

├── dataset/

│   ├── raw/

│   ├── adapted/

│   ├── annotation/

│   │   └── DATASET\_ANNOTATION\_MOORE\_FRENCH.md

│   └── dataset\_description.md

│

├── finetuning/

│   ├── autoscientist\_config.yaml

│   ├── training\_recipe.md

│   └── model\_weights/

│

├── benchmark/

│   └── benchmark\_results.md

│

└── research/

&#x20;   └── research\_report.md

Data availability and redistribution

The repository contains documentation and research artifacts related to the corpus.

Some underlying text materials originate from external sources. Their presence in the research corpus does not imply that they are freely redistributable.

Raw and adapted dataset files are therefore excluded from Git by default. Redistribution of third-party source material should only be undertaken after verifying the applicable permissions and licensing conditions.

See dataset/dataset_description.md for further information about provenance and redistribution.

Reproducibility

The project aims to make the dataset preparation and model adaptation process as reproducible as possible.

The repository documents:

dataset construction and annotation;
corpus statistics;
data provenance;
fine-tuning configuration;
training procedures;
benchmark methodology;
research findings.

When source materials cannot legally be redistributed, researchers should obtain the relevant materials independently and follow the documented preparation methodology.

License

The repository's code and documentation are subject to the project's selected license.

Third-party datasets and source materials remain subject to their respective terms and conditions.

The project license should therefore not be interpreted as granting redistribution rights over external source material.

Acknowledgements

The project acknowledges:

AZN-CIER de Guiè, for educational and community materials originating from the Guiè context;
Alliance Biblique du Burkina Faso, for Mooré biblical material used in the corpus;
the contributors and institutions whose materials made the development of this low-resource research resource possible.
Disclaimer

This project is a research effort focused on low-resource machine translation for Mooré.

The corpus is relatively small and heterogeneous and should not be considered a comprehensive representation of the Mooré language.

Results obtained from the corpus should be interpreted in light of its size, source composition, annotation methodology, and documented limitations.