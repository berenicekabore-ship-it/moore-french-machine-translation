\# Dataset Annotation — Moore–French Parallel Corpus



\## 1. Dataset purpose



This dataset is a parallel corpus designed for \*\*Mooré → French machine translation\*\*.



Each record contains one Mooré segment aligned with its corresponding French segment. The dataset combines manually prepared educational/community texts from Guiè, Burkina Faso, with additional bilingual material including biblical passages.



The corpus was prepared for language adaptation and subsequent LoRA fine-tuning of a Llama 3.3 70B Instruct model.



\## 2. Unit of annotation



The basic annotation unit is a \*\*parallel segment pair\*\*:



| Field | Description |

|---|---|

| `moore` | Source-language segment in Mooré |

| `french` | Corresponding translation in French |



A segment may be a sentence, a short group of sentences, a narration unit, or a dialogue turn when keeping the unit intact is necessary to preserve meaning and alignment.



Segmentation was based on \*\*semantic and translation alignment\*\*, rather than a fixed sentence length.



\## 3. Language direction



\- Source language: Mooré

\- Target language: French

\- Task: machine translation

\- Primary direction: Mooré → French



\## 4. Data sources



The corpus contains material from several source categories.



\### A. Educational and community documents



These include bilingual or manually aligned materials produced in the context of educational and community activities in and around Guiè, Burkina Faso.



Topics include schooling, agriculture, livestock, local commerce, community life, everyday situations, and practical activities.



\### B. Biblical material



The corpus also contains Mooré–French biblical material, including passages from Genesis. The Mooré version was aligned with the corresponding French text at segment level.



\### C. Additional independent parallel examples



The dataset may also contain short independent Mooré–French examples used to increase lexical and structural coverage. These examples were retained only when a clear semantic correspondence existed.



\## 5. Annotation and cleaning procedure



The dataset underwent manual quality control before adaptation:



1\. Mooré and French segments were paired according to meaning.

2\. Segments without a genuine counterpart were removed.

3\. Empty Mooré or French cells were removed.

4\. Exact or obvious duplicate entries were removed.

5\. Proper names were harmonized across corresponding Mooré and French segments where appropriate.

6\. Narration and dialogue were separated when this improved alignment.

7\. Segments were divided only when meaningful one-to-one alignment could be preserved.

8\. Segments were not artificially divided when doing so would break meaning or correspondence.

9\. Final manual checks were performed for semantic correspondence and formatting consistency.



\## 6. Quality criteria



| Criterion | Requirement |

|---|---|

| Language | Mooré on the source side and French on the target side |

| Completeness | Both fields contain text |

| Alignment | The two segments express corresponding content |

| Duplication | No known duplicate pair |

| Names | Proper names standardized where appropriate |

| Segmentation | Boundaries preserve meaning and alignment |

| Direction | Mooré → French |

| Usability | Suitable as a machine-translation example |



This is a low-resource corpus assembled from heterogeneous sources; residual variation in spelling, orthography, style, and translation strategy may therefore remain.



\## 7. Annotation scope and limitations



The dataset is \*\*segment-level annotated\*\*, not morphologically or syntactically annotated.



No systematic POS tagging, morphological annotation, dependency parsing, named-entity classification, word alignment, or phonological annotation was performed.



The annotation documents the information actually established during corpus construction: language, parallel correspondence, segmentation, and quality-control status.



\## 8. Adaptation format



The final adaptation file uses only the two translation fields:



```text

moore,french

```



Project metadata such as IDs, source labels, section labels, and quality-control fields should be preserved separately for reproducibility when available.



\## 9. Dataset statistics



The final corpus used for adaptation contains:



\- \*\*1,176 parallel segments\*\*

\- \*\*Mooré:\*\* 48,781 tokens according to the local tokenizer

\- \*\*French:\*\* 34,654 tokens according to the local tokenizer

\- \*\*Mooré + French:\*\* 83,435 tokens according to the local tokenizer



A separate tokenizer analysis identified six anomalous `enhanced\_completion` entries. They were excluded from the cleaned statistical analysis, while the original 1,176-entry corpus was preserved.



\## 10. Data provenance and acknowledgements



The research project should acknowledge:



\- \*\*AZN-CIER de Guiè\*\*, for educational/community materials originating from the Guiè context;

\- \*\*Alliance Biblique du Burkina Faso\*\*, for the Mooré biblical material used in the corpus.



The research report should distinguish original source material, manually prepared/aligned data, and model-generated or adaptation-related material.



\## 11. Suggested dataset description



> A manually curated Mooré–French parallel corpus for low-resource machine translation. The corpus combines educational and community materials from Guiè, Burkina Faso, with additional bilingual material including Mooré biblical passages. Data preparation involved manual extraction/transcription, correction, semantic alignment, segmentation, duplicate removal, proper-name normalization, and manual quality control. The resulting corpus contains 1,176 aligned Mooré–French segments and was used for model adaptation and subsequent LoRA fine-tuning.



