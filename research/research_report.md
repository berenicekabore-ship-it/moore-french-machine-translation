Adaptation of a Large Language Model for

Mooré–French Machine Translation

Research Report



A low-resource language adaptation project combining corpus construction, dataset cleaning, and LoRA fine-tuning of Meta Llama 3.3 70B Instruct for the Mooré → French translation direction.



 

Table of Contents

Abstract

1\. Introduction

2\. Project Objectives

3\. Data Collection

4\. Dataset Construction

5\. Dataset Description

6\. Dataset Adaptation

7\. Model Adaptation

8\. Fine-Tuning with AutoScientist

9\. Verification of the Fine-Tuned Adapter

10\. Local Evaluation Environment

11\. Hardware Limitation

12\. Benchmarking Strategy: From a Dataset Benchmark to a Tokenizer Benchmark

13\. Tokenization and Corpus Benchmark

14\. Dataset Anomalies

15\. Cleaned Corpus Statistics

16\. Results

17\. Discussion

18\. Limitations

19\. Reproducibility

20\. Ethical and Data Attribution Considerations

21\. Deliverables

22\. Conclusion

 

Abstract

This project investigates the adaptation of a large language model for Mooré-to-French machine translation, with a particular focus on a low-resource African language spoken primarily in Burkina Faso and neighboring countries.

The project followed a complete data-to-model workflow: data collection, corpus construction, manual correction and alignment, dataset adaptation, model fine-tuning using AutoScientist, and subsequent benchmarking. The resulting parallel corpus contains 1,176 aligned Mooré–French segments. The corpus combines educational and community-oriented texts produced in Guiè, Burkina Faso, with additional bilingual material and Mooré–French biblical text.

The corpus was manually reviewed to remove duplicates, incomplete segments, empty cells and non-corresponding source-target pairs. Proper names were standardized, and dialogue and narrative segments were reorganized where necessary to improve alignment.

The adapted model is based on Meta Llama 3.3 70B Instruct and was fine-tuned using LoRA. The fine-tuning configuration used three epochs, a LoRA rank of 64, an alpha value of 128, all linear layers as targets, cosine scheduling, a warmup ratio of 0.05, and gradient clipping of 1.

A tokenizer-based corpus benchmark found 541,828 tokens in the original dataset according to the local tokenizer. A subsequent statistical analysis identified six anomalous entries containing extreme repetitive generations. After excluding these entries for statistical analysis, the corpus contained 1,170 entries and 447,868 tokens.

The project demonstrates the feasibility of constructing and adapting a Mooré–French translation resource despite the limited availability of high-quality parallel data. However, a complete generation-based evaluation of the 70B model could not be conducted locally because of hardware limitations. The available computer has approximately 17 GB of RAM and no CUDA-capable GPU. Consequently, BLEU, chrF, inference latency and direct base-model versus adapted-model comparisons could not be reliably obtained locally.

1\. Introduction

1.1 Background

Mooré is a major language of Burkina Faso but remains comparatively underrepresented in contemporary natural language processing resources. The availability of high-quality digital text and, more importantly, parallel Mooré–French data, remains limited.

This creates a significant challenge for machine translation. Although substantial Mooré textual material exists in educational, cultural and religious contexts, much of the available material is monolingual or is not provided in a format directly usable for supervised machine translation.

The objective of this project was therefore not simply to collect Mooré text, but to construct a usable Mooré–French parallel corpus and use it to adapt a large language model to the specific translation direction:

Mooré → French

The project was conducted in the context of the Guiè/AZN-CIER environment in Burkina Faso. The educational material used in the project includes material associated with the CIER (Centre d'Instruction et d'Education Rural) and the AZN (Association villageoise Zoramb Naagtaaba) of Guiè, Burkina Faso. The source material itself identifies the CIER and the AZN of Guiè as its production context.

Biblical material was additionally incorporated using Mooré biblical resources associated with the Alliance Biblique du Burkina Faso, providing a substantially different linguistic and stylistic domain from the educational and community texts.

2\. Project Objectives

The project followed five main objectives:

●	Collect Mooré and French textual resources.

●	Construct a manually reviewed parallel Mooré–French dataset.

●	Adapt the dataset for machine-learning use.

●	Fine-tune a large language model using AutoScientist.

●	Evaluate the resulting resource and document the complete workflow.

The final intended application is a translation system capable of producing French translations from Mooré input.

The project workflow can therefore be summarized as:

Data collection → Data cleaning → Parallel alignment → Dataset adaptation → Model adaptation → Fine-tuning → Benchmarking → Documentation

3\. Data Collection

3.1 Educational and Community Material

One of the principal sources was the bilingual educational material Du Mooré au Français, produced in the context of the CIER and the AZN of Guiè.

The source identifies the publication as a bilingual reading book for young learners who have acquired reading skills in Mooré and attributes its conception to the CIER (Centre d'Instruction et d'Education Rural) and the AZN (Association villageoise Zoramb Naagtaaba) of Guiè, Burkina Faso.

This material was particularly valuable because it contains Mooré and French material in a bilingual pedagogical context. The raw source includes exercises, example sentences, vocabulary and longer textual material in both languages.

Additional educational/community texts included material concerning:

●	Education and school attendance

●	Agriculture

●	Livestock

●	Local commerce

●	Everyday community life

●	Rural development

●	Interactions between children and adults

This diversity was deliberately preserved because the objective was to avoid creating a translation model specialized exclusively in one narrow domain.

3.2 Biblical Material

Biblical text was added as a second major source of parallel data.

The biblical material provides:

●	Longer continuous prose

●	Narrative structures

●	Dialogue

●	Descriptive passages

●	Historical and religious vocabulary

●	A substantially different register from the educational material

This was important because the original educational material alone was relatively small.

The resulting corpus therefore combines educational, conversational, agricultural, community, commercial and biblical language rather than relying exclusively on one genre.

4\. Dataset Construction

4.1 Initial Extraction

The source material was first extracted from PDFs and digital sources.

Mooré texts required substantial manual intervention because OCR and extraction could introduce:

●	Incorrect characters

●	Broken words

●	Missing diacritics

●	Segmentation errors

●	Duplicated text

●	Formatting artefacts

The Mooré material was consequently manually corrected before alignment.

4.2 Parallel Alignment

The central objective was to obtain pairs of the form:

Mooré	French

Mooré source segment	Corresponding French translation

Table 1. Structure of an aligned Mooré–French pair.

Narration and dialogue were reorganized when necessary so that the Mooré and French segments represented equivalent linguistic units.

A particularly important principle was that a segment was not retained merely because it contained valid Mooré or valid French text. It had to have a meaningful counterpart in the other language.

Consequently, segments were removed when they were:

●	Incomplete

●	Duplicated

●	Empty

●	Lacking a genuine counterpart

●	Impossible to align without destroying their meaning

4.3 Manual Quality Control

Several rounds of manual revision were performed.

The final cleaning process included:

●	Correction of Mooré transcription

●	Correction of French text

●	Standardization of proper names

●	Removal of duplicate pairs

●	Removal of empty cells

●	Removal of unmatched Mooré segments

●	Removal of unmatched French segments

●	Restructuring of dialogue

●	Preservation of semantic alignment

●	Verification of the final source-target correspondence

The final parallel corpus contained:

1,176 aligned Mooré–French entries

5\. Dataset Description

The final dataset was designed specifically for Mooré → French machine translation. The dataset contains approximately:

Component	Description

Source language	Mooré

Target language	French

Entries	1,176 aligned segments

Main task	Mooré → French translation

Data type	Parallel corpus

Domains	Education, agriculture, livestock, commerce, community life, biblical text

Alignment	Manually reviewed

Duplicate removal	Yes

Empty-pair removal	Yes

Proper-name normalization	Yes

Dialogue restructuring	Yes

Table 2. Summary description of the final dataset.

The corpus is relatively small in terms of sentence/segment count, but its token-based size substantially exceeds the minimum requirement specified by the project.

6\. Dataset Adaptation

The cleaned parallel dataset was subsequently imported into AdaptionLab. The platform was used to prepare the dataset for model adaptation.

During this stage, the dataset initially received a relatively low automated quality score. The final reported score was:

●	Quality score: 6/10

●	Percentile: 3.3%

This result indicates that the dataset was considered low-quality by the platform's automated language-domain comparison.

However, the dataset had undergone extensive manual cleaning and alignment. The low automated score should therefore be interpreted as a characteristic of the current resource rather than as evidence that the dataset contains no usable parallel information.

The adaptation was nevertheless completed successfully.

7\. Model Adaptation

The target model was based on Meta Llama 3.3 70B Instruct. The adaptation was performed for the specific task of Mooré–French translation.

The resulting trained model was identified as:

adaption\_llama\_3\_3\_70b\_instru\_moore\_french\_parallel\_58863825

The adapted model was subsequently made available as a LoRA/PEFT adapter rather than as a complete standalone 70B model.

8\. Fine-Tuning with AutoScientist

The fine-tuning stage was performed using AutoScientist. The final configuration was:

Parameter	Configuration

Base model	Meta Llama 3.3 70B

Fine-tuning method	LoRA

Dataset	Adapted Mooré–French dataset

Epochs	3

LoRA rank	64

LoRA alpha	128

Target layers	All linear layers

Scheduler	Cosine

Warmup ratio	0.05

Gradient clipping	1

Dataset expansion	Not performed

Table 5. Final AutoScientist fine-tuning configuration.

Dataset expansion was not performed because of the project's 50-credit constraint.

The fine-tuning completed successfully.

9\. Verification of the Fine-Tuned Adapter

The resulting model was verified as a LoRA/PEFT adapter rather than a full model. Its configuration identified:

●	Base model: togethercomputer/Meta-Llama-3.3-70B-Instruct-Reference

●	PEFT type: LoRA

●	Task: CAUSAL\_LM

●	LoRA rank: 64

●	LoRA alpha: 128

The extracted adapter\_model.safetensors file contained 1,120 tensors, confirming that the trained adapter weights were present and structurally consistent with the LoRA configuration.

The trained weights and AutoScientist configuration/script were downloaded as project artefacts.

10\. Local Evaluation Environment

Once the adapter had been trained and verified, a dedicated Python virtual environment was prepared with the intention of running a full generation-based evaluation of the fine-tuned model. The following software was installed:

Software	Version / Status

Python	3.13.14

PyTorch	2.13.0+cpu

Transformers	5.15.0

PEFT	0.20.0

Accelerate	1.14.0

SentencePiece	Installed

SacreBLEU	2.6.0

Table 6. Local evaluation environment configuration.

SacreBLEU was included specifically because the original benchmarking plan called for a generation-based dataset evaluation producing BLEU and chrF scores. The environment itself was successfully configured; the constraint that emerged next was hardware, not software.

11\. Hardware Limitation

Before the generation-based evaluation could be run, it became clear that the local computer used for the evaluation did not meet the requirements for 70B inference. Its approximate specifications were:

●	RAM: 17 GB

●	GPU: Intel UHD Graphics 620

●	CUDA available: False

Because the adapted model is based on a 70-billion-parameter model, loading the complete base model locally was not considered technically appropriate with this hardware.

This was identified at the point where the dataset-level, generation-based benchmark was about to begin — that is, once fine-tuning and adapter verification were already complete. It was therefore a hardware limitation discovered at the benchmarking stage, rather than a failure of the trained adapter itself.

12\. Benchmarking Strategy: From a Dataset Benchmark to a Tokenizer Benchmark

The benchmark originally planned for this project was a dataset-level, generation-based evaluation: running the adapted 70B model on held-out Mooré source segments and comparing its French output against the reference translations, using metrics such as BLEU and chrF.

As described in the previous section, this plan could not be carried out. The available local computer — approximately 17 GB of RAM and no CUDA-capable GPU — was not capable of loading or running inference on a 70-billion-parameter model, even with the adapter attached.

Faced with this constraint, the benchmarking approach was revised. Rather than abandoning evaluation altogether, the project pivoted to a token corpus benchmark (tokenizer benchmark): a benchmark performed directly on the corpus using the model's local tokenizer, without requiring the base model itself to be loaded or run. This benchmark could be executed entirely on the available hardware, since tokenization is far less resource-intensive than generation.

This pivot took place after fine-tuning and adapter verification (Sections 8–9) were already complete, and after the local evaluation environment had been prepared with a generation-based benchmark in mind (Sections 10–11). The tokenizer benchmark described in the following three sections — corpus tokenization, anomaly detection, and cleaned-corpus statistics — was therefore carried out at this later stage of the project, once it was established that a generation-based benchmark was not achievable locally.

The resulting tokenizer benchmark does not measure translation quality. It instead establishes a reproducible quantitative characterization of the corpus itself — its size, structure and composition — which stands in place of the generation-based benchmark that could not be performed.

13\. Tokenization and Corpus Benchmark

The tokenizer benchmark adopted in place of the generation-based evaluation was conducted as follows.

The local tokenizer was loaded using PreTrainedTokenizerFast, and token counts were obtained with the following call:

tokenizer.encode(text, add\_special\_tokens=False)

Therefore, the reported values correspond to tokens generated by the local tokenizer without additional special tokens. The original corpus contained 1,176 entries.

13.1 Original Corpus

Field	Tokens

Mooré	48,781

French	34,654

Mooré + French	83,435

Enhanced completion	458,393

Total	541,828

Table 3. Token counts for the original 1,176-entry corpus.

The average was approximately:

●	41.48 Mooré tokens per entry

●	29.47 French tokens per entry

●	70.95 Mooré + French tokens per entry

Importantly, even the Mooré + French parallel fields alone contain 83,435 tokens, which is substantially above the project's 5,000-token minimum.

14\. Dataset Anomalies

The tokenizer analysis revealed an important issue in the enhanced\_completion field.

Although most sequences were relatively short, six entries contained extremely long repetitive outputs. The six anomalous entries were entry numbers 81, 167, 385, 557, 749 and 964.

Their lengths ranged from 11,139 to 18,626 tokens, whereas the next longest examples were below 1,000 tokens.

Manual inspection showed that these were not naturally long linguistic examples but contained substantial repetition.

For statistical analysis, these six entries were therefore excluded without modifying the original dataset.

15\. Cleaned Corpus Statistics

After excluding the six anomalous entries:

Measure	Original	Statistical corpus

Entries	1,176	1,170

Mooré tokens	48,781	48,476

French tokens	34,654	34,393

Enhanced completion	458,393	364,999

Total	541,828	447,868

Table 4. Corpus statistics before and after excluding the six anomalous entries.

The six entries accounted for 93,960 tokens, approximately 17.34% of the original total.

For the cleaned enhanced\_completion distribution:

●	Mean: 311.96 tokens

●	Median: 303.5 tokens

●	P99: 737 tokens

●	Maximum: 967 tokens

This provides a reproducible statistical characterization of the corpus while preserving the original dataset for traceability. Together with Sections 12–14, this closes out the benchmarking stage of the project: the generation-based evaluation that had originally been planned was not achievable on the available hardware, and the tokenizer benchmark presented here was carried out as the substitute quantitative characterization of the resource.

16\. Results

The project produced three principal outcomes.

16.1 A Manually Curated Mooré–French Parallel Corpus

A corpus of 1,176 aligned entries was constructed and reviewed. The parallel Mooré + French fields contain 83,435 tokens according to the local tokenizer, substantially exceeding the project's minimum 5,000-token requirement.

16.2 A Trained LoRA Adapter

The corpus was successfully adapted and used to fine-tune a Meta Llama 3.3 70B Instruct model through AutoScientist.

16.3 A Reproducible Corpus Benchmark

The tokenizer analysis identified the corpus size and several data-quality anomalies, while preserving the original dataset for reproducibility.

17\. Discussion

The project illustrates several challenges associated with machine translation for low-resource languages.

First, the primary limitation was not the availability of Mooré text itself but the availability of high-quality parallel Mooré–French data. Monolingual Mooré documents can provide valuable linguistic material, but they cannot directly provide supervised translation pairs unless an equivalent French source is available.

The bilingual educational material was therefore particularly valuable because it allowed relatively reliable manual alignment. The biblical material then substantially increased the amount of parallel text and introduced a different linguistic register.

Second, manual data preparation proved essential. OCR errors, inconsistent names, segmentation problems and unmatched segments could significantly reduce the quality of an automatically constructed corpus.

Third, the AdaptionLab quality score suggests that automated dataset-quality metrics may remain challenging for low-resource language pairs. The final score of 6/10 and percentile of 3.3% should therefore be reported transparently rather than hidden.

At the same time, the project demonstrates that a relatively small, manually curated corpus can nevertheless be used successfully to produce a trained LoRA adapter.

18\. Limitations

Several limitations should be explicitly acknowledged.

18.1 Dataset Size

Although the dataset exceeds the required 5,000-token threshold, 1,176 parallel segments remain a relatively small supervised corpus for adapting a 70B model.

18.2 Data-Domain Imbalance

The corpus combines several domains, but the amount of data available from each domain is not necessarily balanced.

18.3 Automated Dataset-Quality Score

AdaptionLab assigned a quality score of 6/10 and a 3.3rd percentile ranking.

18.4 Hardware

The lack of a CUDA-capable GPU and the approximately 17 GB of available RAM prevented local inference of the 70B model.

18.5 Missing Generation-Based Metrics

BLEU, chrF and direct generation-based comparisons between the original and adapted models were not obtained locally. These should therefore be considered future evaluation work, rather than reported as zero or estimated values.

19\. Reproducibility

To ensure reproducibility, the project should preserve the following artefacts:

Dataset

●	Raw dataset

●	Adapted dataset

●	Dataset description

●	Dataset annotation/documentation

●	Source inventory

●	Changelog

Model

●	Fine-tuned LoRA adapter

●	AutoScientist configuration/script

●	Fine-tuning parameters

●	Downloaded model weights

Evaluation

●	Tokenizer benchmark

●	Corpus statistics

●	Anomaly analysis

●	Benchmark scripts

●	Any future BLEU/chrF evaluation results

The original 1,176-entry corpus should remain preserved separately from the 1,170-entry statistical analysis corpus. This ensures that the exclusion of the six anomalous entries does not alter the provenance of the original dataset.

20\. Ethical and Data Attribution Considerations

The project relies on educational and community-oriented materials associated with the CIER and the AZN of Guiè, and these contributions should be explicitly acknowledged in any public release.

The bilingual educational source identifies the CIER (Centre d'Instruction et d'Education Rural) and the AZN (Association villageoise Zoramb Naagtaaba) of Guiè, Burkina Faso, as the production context of the material.

The biblical material should likewise acknowledge the Alliance Biblique du Burkina Faso as requested for the project.

The final publication should clearly distinguish:

●	Original source material

●	Manually corrected/transcribed material

●	Aligned dataset

●	Adapted dataset

●	Generated model outputs

This distinction is particularly important when publishing the dataset or model on Hugging Face.

21\. Deliverables

The project's required deliverables can now be mapped as follows:

Required Deliverable	Status

Raw dataset	Completed

Adapted dataset	Completed

≥5,000 tokens	Completed — 83,435 Mooré+French tokens in the parallel fields

Dataset description	Completed

Dataset annotation/documentation	Completed

AutoScientist fine-tuning	Completed

Fine-tuned model	Completed

Downloaded model weights	Completed

AutoScientist script/configuration	Completed

Loss plots	Not available from platform

Corpus/tokenizer benchmark	Completed

Generation-based BLEU/chrF benchmark	Not completed locally

Hugging Face publication	Completed

GitHub project	Completed

Research paper / long abstract	Current document

Project post	To prepare

Table 7. Status of required project deliverables.

22\. Conclusion

This project developed and tested an end-to-end workflow for adapting a large language model to Mooré–French machine translation in a low-resource setting.

A manually curated parallel corpus of 1,176 entries was constructed from educational, community and biblical sources. The parallel portion alone contains 83,435 tokens, exceeding the project's minimum dataset requirement. The data underwent extensive manual correction, alignment, deduplication and normalization.

The corpus was successfully adapted through AdaptionLab and subsequently used to fine-tune Meta Llama 3.3 70B Instruct with a LoRA configuration using AutoScientist.

The fine-tuning process successfully produced a LoRA adapter with a rank of 64 and alpha of 128. The adapter was extracted and structurally verified.

The tokenizer benchmark provided an additional quantitative characterization of the resource, identifying 541,828 tokens in the original corpus and 447,868 tokens in the cleaned statistical corpus. Six anomalous entries containing highly repetitive generated content were identified and excluded from the statistical analysis while preserving the original corpus.

The main remaining limitation is the absence of a complete generation-based evaluation of the 70B model. The available local computer does not provide sufficient hardware for reliable 70B inference. Consequently, BLEU, chrF and direct translation-quality comparisons cannot currently be reported.

Despite this limitation, the project successfully demonstrates the complete process from low-resource data collection and manual parallel-corpus construction to dataset adaptation and LoRA fine-tuning of a 70B language model.

The resulting resources constitute a foundation for future work on Mooré–French machine translation and, more broadly, for increasing the representation of Mooré in natural language processing.
