Dataset Description — Moore–French Parallel Corpus

1\. Overview



The Moore–French Parallel Corpus is a manually curated parallel dataset developed for low-resource machine translation from Mooré to French.



The corpus contains aligned Mooré–French segment pairs collected and prepared from heterogeneous bilingual and multilingual sources. It was developed as part of a research project on language adaptation and machine translation for Mooré.



The final corpus used for model adaptation contains 1,176 parallel segments.



2\. Task and language direction

Source language: Mooré

Target language: French

Primary task: Machine translation

Primary direction: Mooré → French

Corpus type: Parallel text corpus

Annotation level: Segment-level semantic and translation alignment



The corpus is intended primarily for research and experimentation in low-resource machine translation.



3\. Dataset composition



Each principal record consists of two aligned fields:



Field	Description

moore	Source-language segment in Mooré

french	Corresponding French translation



Segments may correspond to individual sentences, short groups of sentences, narration units, or dialogue turns. Segmentation was determined according to semantic and translation alignment rather than a fixed sentence-length rule.



4\. Data sources



The corpus combines several categories of material.



4.1 Educational and community materials



The dataset includes bilingual or manually aligned educational and community materials originating from the Guiè context in Burkina Faso.



The material covers topics such as:



education and schooling;

agriculture;

livestock;

local commerce;

community life;

everyday situations;

practical activities.

4.2 Biblical material



The corpus also contains Mooré–French biblical material, including passages from Genesis. Mooré passages were aligned with their corresponding French passages at segment level.



4.3 Additional parallel examples



The corpus may contain independent Mooré–French examples selected to increase lexical and structural coverage. Such examples were retained when a clear semantic correspondence could be established.



5\. Data preparation



The corpus was manually prepared and quality-controlled before model adaptation.



The preparation process included:



extraction or transcription of source material;

correction and formatting;

semantic alignment of Mooré and French segments;

removal of segments without genuine counterparts;

removal of empty entries;

duplicate removal;

proper-name harmonization where appropriate;

segmentation according to meaningful translation units;

manual quality-control checks.



The corpus was not produced by a fully automated annotation pipeline. Manual linguistic judgment was used throughout the alignment and quality-control process.



Detailed annotation methodology is documented in:



dataset/annotation/DATASET\_ANNOTATION\_MOORE\_FRENCH.md



6\. Dataset statistics



The final corpus used for adaptation contains:



Statistic	Value

Parallel segments	1,176

Mooré tokens	48,781

French tokens	34,654

Total tokens	83,435



Token counts were obtained using the local tokenizer used during corpus analysis.



A separate tokenizer analysis identified six anomalous enhanced\_completion entries. These entries were excluded from the cleaned statistical analysis, while the original 1,176-entry corpus was preserved.



7\. Intended use



The corpus was prepared for:



low-resource Mooré–French machine translation research;

language adaptation experiments;

supervised fine-tuning experiments;

LoRA-based model adaptation;

evaluation and benchmarking of translation systems.



The corpus should be considered a research dataset rather than a comprehensive representation of the Mooré language.



8\. Limitations



The corpus is relatively small and was assembled from heterogeneous sources. Consequently, it may contain variation in:



spelling and orthography;

vocabulary;

translation style;

sentence and segment structure;

register;

source-domain distribution.



The corpus is segment-level annotated. It does not provide systematic:



morphological annotation;

part-of-speech tagging;

syntactic dependency annotation;

named-entity annotation;

phonological annotation;

word-level alignment.



The corpus should therefore not be interpreted as a fully linguistically annotated Mooré resource.



9\. Provenance and acknowledgements



The project acknowledges the contribution and provenance of source materials associated with:



AZN-CIER de Guiè, for educational and community materials originating from the Guiè context;

Alliance Biblique du Burkina Faso, for Mooré biblical material used in the corpus.



The research documentation should distinguish between:



original source materials;

manually extracted, prepared, and aligned material;

annotations and transformations produced during the research project;

model-generated or model-adaptation-related material.

10\. Redistribution and licensing



The presence of third-party source materials means that the dataset should not automatically be considered freely redistributable under the project's software license.



The licensing and redistribution conditions of each source should be verified before publishing the corresponding raw or adapted text publicly.



For this reason, raw and adapted dataset files are excluded from version control by default through the project's .gitignore.



The repository may contain documentation, metadata, processing code, statistics, and other research artifacts without necessarily redistributing the underlying third-party source texts.



11\. Reproducibility



The project aims to document the dataset preparation process sufficiently to support reproducible research.



The repository records the annotation methodology, dataset statistics, provenance information, and subsequent model-adaptation procedures.



Where original source data cannot legally or ethically be redistributed, researchers should obtain the relevant source materials independently and follow the documented preparation methodology.



12\. Related documentation

dataset/annotation/DATASET\_ANNOTATION\_MOORE\_FRENCH.md — detailed annotation methodology and quality criteria.

dataset/raw/ — location reserved for source data; raw files are excluded from Git by default.

dataset/adapted/ — location reserved for adapted dataset files; files are excluded from Git by default.

finetuning/ — model adaptation and training documentation.

benchmark/ — evaluation results.

research/ — research reports and analyses.

